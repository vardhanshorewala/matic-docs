---
id: delegation
title: Delegation (Validator-Anteile)
description: "Delegation über Validator-Anteile."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Polygon unterstützt Delegation über Validator-Anteile. Mithilfe dieses Modells ist es einfacher, auf Ethereum-Contracts Prämien ohne große Rechenleistung auszuschütten und im Rahmen des Slashing in großem Umfang abzustrafen (Tausende von Delegierende).

Die Delegierenden delegieren, indem sie von den Validatoren-Anteile eines begrenzten Pools erwerben. Jeder Validator wird seinen eigenen Validator-Anteils-Token haben. Nennen wir diese Fungible Token `VATIC` für einen Validator `A`. Sobald ein Benutzer `A` an einen Validator delegiert, werden diese `VATIC` auf Basis des Wechselkurses eines `MATIC/VATIC`-Paares ausgestellt. Solange Benutzer Beträge anhäufen lassen, zeigt der Wechselkurs an, dass sie jetzt mehr `MATIC` pro `VATIC` abheben können; werden Benutzer hingegen abgestraft, können diese weniger `MATIC` für ihre `VATIC` abheben.

Beachte, dass `MATIC` ein Staking-Token ist. Ein Delegierender muss über `MATIC`-Token verfügen, um an der Delegation teilzunehmen.

Zunächst kauft ein Delegierender `D` Token vom Validator `A` aus einem bestimmten Pool, wenn `1 MATIC per 1 VATIC`.

Wenn ein Validator mit mehr `MATIC`-Token belohnt wird, werden dem Pool neue Token hinzugefügt. Nehmen wir an, bei dem aktuellen Pool mit `100 MATIC`-Token  werden `10 MATIC` Prämien dem Pool hinzugefügt. Doch da sich die Gesamtversorgung der `VATIC`-Token aufgrund der Prämien nicht verändert, fällt der Wechselkurs dann folgendermaßen aus: `1 MATIC per 0.9 VATIC`. Nun erhält der Delegierende `D` mehr `MATIC` für die gleichen Anteile. Ähnlich läuft es auch beim Slashing ab, wenn `10 MATIC` aus dem Pool abgestraft werden, wird der neue Wechselkurs folgendermaßen ausfallen: `1 Matic per 1.1 VATIC`.

`VATIC`: Validatoren-spezifische gemintete Validator-Anteils-Token (ERC20-Token)

## Technische Spezifikation {#technical-specification}

```java
uint256 public validatorId; // Delegation contract for validator
uint256 public validatorRewards; // accumulated rewards for validator
uint256 public commissionRate; // validator's cut %
uint256 public validatorDelegatorRatio = 10; // to be implemented/used

uint256 public totalStake;
uint256 public rewards; // rewards for pool of delegation stake
uint256 public activeAmount; // # of tokens delegated which are part of active stake
```

Der Wechselkurs wir wie folgt berechnet:

```js
ExchangeRate = (totalDelegatedPower + delegatorRewardPool) / totalDelegatorShares
```

### buyVoucher {#buyvoucher}

```js
function buyVoucher(uint256 _amount) public;
```

- Übertrage die `_amount` an den stakeManager und aktualisiere die Timeline-Datenstruktur für den aktiven Stake.
- `updateValidatorState` wird verwendet, um die Timeline-DS zu aktualisieren.
- `Mint` Delegationsanteile, die die aktuellen `exchangeRate` für `_amount` verwenden.
- `amountStaked` wird verwendet, um den aktiven Stake eines jeden Delegierenden zu verfolgen, um liquide Prämien zu berechnen.

### sellVoucher {#sellvoucher}

```js
function sellVoucher() public;
```

- Mithilfe des aktuellen  `exchangeRate` und # an Anteilen Gesamtbetrag berechnen (aktiver Stake+ Prämien).
- Den aktiven Stake vom Validator entbinden und Prämien an den Delegierenden übertragen, falls vorhanden.
- Du musst den aktiven Stake von der Timeline entfernen, indem du `updateValidatorState` im stakeManger nutzt.
- Verschiebe den aktiven Stake des Delegierenden in die Abhebungsperiode, damit du beim Slashing nicht abgestraft wirst.
- Das `delegators`-Mapping wird verwendet, um den Stake in der Abhebungsperiode im Blick zu behalten.

### withdrawRewards {#withdrawrewards}

```js
function withdrawRewards() public;
```

- Damit ein Delegierender die Prämien berechnen und diese übertragen kann je nach `exchangeRate` Verbrennung # von Anteilen.
- d. h. der Delegierende besitzt 100 Anteile und der Wechselkurs steht bei 200, dann sind die Prämien 100 Token wert, werden 100 Token an den Delegierenden übertragen, ist der verbleibende Stake 100; wird nun der Wechselkurs angewendet, liegen 200 nun bei 50 Anteilen und 50 Anteile werden verbrannt. Der Delegierende verfügt nun über 50 Anteile im Wert von 100 Token (welche er anfänglich gestaket/delegiert hatte).

### reStake {#restake}

- Um Gelder wieder ins Staking zu legen (Restake), gibt es zwei Vorgehensweisen: Der Delegierende kann weitere Anteile kaufen, indem er `buyVoucher` verwendet oder er legt seine Prämien wieder zurück ins Staking.

```js
function reStake() public;
```

- Die oben genannte Funktion wird verwendet, um Prämien zu restaken.
- Die Anzahl an Anteilen ist nicht davon betroffen, weil `exchangeRate` dasselbe ist; also werden nur die Prämien in den aktiven Stake verschoben, sowohl für den Validator-Anteils-Contract als auch für die stakeManager-Timeline.
- `getLiquidRewards` wird verwendet, um angesammelte Prämien zu berechnen.
- D. h., der Delegierende besitzt 100 Anteile und der Wechselkurs liegt bei 200, demnach sind die Prämien 100 Token wert; werden 100 Token in den aktiven Stake verschoben, verfügt der Wechselkurs demnach weiterhin über dieselbe Anzahl von Anteilen und bleibt dementsprechend gleich. Der einzige Unterschied ist, dass nun 200 Token als im aktiven Stake-liegend betrachtet werden und nicht sofort abgehoben werden können (da sie nicht Teil der liquiden Prämien sind).
- Der Zweck des ReStaking ist, dass der Validator des Delegierenden nun über einen höheren aktiven Stake verfügt und mehr Prämien dafür verdienen wird, gleichermaßen wie der Delegierende.

### unStakeClaimTokens {#unstakeclaimtokens}

```js
function unStakeClaimTokens()
```

- Sobald die Abhebungsperiode vorüber ist, können Delegierende, die ihre Anteile verkauft haben, Matic-Token beanspruchen.
- Es müssen Token an den Benutzer übertragen werden.
- Sobald das Slashing vor Ort durchgeführt wurde, muss überprüft werden, ob das gesamte Slashing in der Abhebungsperiode stattgefunden hat und als gültig betrachtet werden kann.

### updateCommissionRate {#updatecommissionrate}

```js
function updateCommissionRate(uint256 newCommissionRate)
        external
        onlyValidator
```

- Aktualisierungs-Provision % für den Validator.

### updateRewards {#updaterewards}

```js
function updateRewards(uint256 reward, uint256 checkpointStakePower, uint256 validatorStake)
        external
        onlyOwner
        returns (uint256)
```

- Wenn ein Validator Prämien für die Einreichung von Checkpoints erhält, wird diese Funktion für Prämienauszahlungen zwischen dem Validator und dem Delegierenden aufgerufen.

Für weitere Details findest du hier ein Video, das den gesamten Mechanismus detailliert erklärt:

<!-- [https://www.youtube.com/watch?v=8nODLU9C3mw](https://www.youtube.com/watch?v=8nODLU9C3mw) -->

[![Liquide Staking-Assets anlegen – Video](https://img.youtube.com/vi/8nODLU9C3mw/0.jpg)](https://www.youtube.com/watch?v=8nODLU9C3mw)
