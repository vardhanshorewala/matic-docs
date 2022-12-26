---
id: stakingmanager
title: Staking-Manager
description: "Der Main-Contract zur Abwicklung sämtlicher validatorbezogenen Aktivitäten."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Alle Prämien werden auf Grundlage von Polygons Proof-of Security-basiertem Konsens, der gesamten ⅔+1- Proof-Verfizierung und der Abwicklung des Stakings auf dem Ethereum Smart Contract durchgeführt.

Der gesamte Aufbau folgt dieser Philosophie, den Datenverkehr auf dem Mainnet-Contract möglichst gering zu halten. Er übernimmt die Verifizierung von Informationen und verschiebt alle Operationen mit größerem Rechenaufwand auf die L2 (Lies mehr darüber auf Heimdall für dieses Dok.).

Staking-Akteure (Staker) werden in Validatoren, Delegierende und Aufseher (zur Betrugsmeldung) eingeteilt.

StakeManager ist der Main Contract zur Abwicklung von validatorbezogenen Aktivitäten, darunter `checkPoint` Unterschriftsverifizierung, Prämienauschüttung, Slashing und Stake-Management.

Beachte, dass ein Staker nur von einer Ethereum-Adresse Validator oder Delegierender sein kann (Es handelt sich hier um eine Frage des Designs und hat keine tiefere Bedeutung).

Da der Contract die NFT-ID als Quelle für die Zuordnung des Inhabers verwendet, würde sich ein Wechsel des Inhabers und des Unterzeichnenden nicht auf das System auswirken.

`validatorThreshold`: Zeigt die maximale Anzahl von vom System akzeptierten Validatoren, die auch Slots genannt werden, an.

### AccountStateRoot {#accountstateroot}

- Für die unterschiedlichen Abrechnungen, die auf Heimdall für Validatoren und Delegierende durchgeführt werden, wird die Account-Root eingereicht, während gleichzeitig die übermittelt `checkpoint` wird.
- accRoot wird während `claimRewards` und `unStakeClaim` verwendet.

## Stake/stakeFor {#stake-stakefor}

```cpp
function stake(
    uint256 amount,
    uint256 heimdallFee,
    bool acceptDelegation,
    bytes calldata signerPubkey
) public;

function stakeFor(
    address user,
    uint256 amount,
    uint256 heimdallFee,
    bool acceptDelegation,
    bytes memory signerPubkey
) public;
```

- Ermöglicht es jedem mit einem (Matic-Token)-Betrag höher als `minDeposit`, dann wenn `currentValidatorSetSize` weniger ist, dann `validatorThreshold` .
- Es MÜSSEN `amount+heimdallFee` übertragen werden, setzt den Validator auf die Auktionsperiode für ein auctionInterval aus. (mehr unter Auktion im Abschnitt Auktion)
- `updateTimeLine` aktualisiert die spezielle Datenstruktur der Timeline, die die aktiven Validatoren und den aktiven Stake für eine bestimmte Epoche/Checkpoint-Zähler verfolgt.
- Ein eindeutiges `NFT` wird auf jedem neuen stake/stakeFor-Aufruf gemintet, welcher an beliebige Benutzer übertragen werden, aber auch 1:1 auf der Ethereum-Adresse verbleiben kann.
- Sobald `acceptDelegation` bestätigt hat, dass ein Validator die Delegation akzeptieren möchte, wird der `ValidatorShare`-Contract für den Validator bereitgestellt.

## unstake {#unstake}

- Entferne Validator von der Validator-Auswahl in der nächsten Epoche (nur gültig für den aktuellen Checkpoint, sobald `unstake` aufgerufen wurde)
- Entferne den Stake des Validators von der Datenstruktur der Timeline, aktualisiere den Zähler für den Austritt des Validators am Ende der Epoche.
- Wenn der Validator seine Delegation auf „Alle Prämien einsammeln“ und „Contract für neue Delegationen sperren“ eingestellt hatte.

## unstakeClaim {#unstakeclaim}

```cpp
function unstakeClaim(uint256 validatorId) public;
```

- Nachdem die `unstaking`-Validatoren in die Abhebungsperiode eingegangen sind, sodass sie abgestraft werden können, wenn irgendeine Art von Betrug nach dem  `unstaking`für Pas-Frauds gefunden wurde.
- Sobald die `WITHDRAWAL_DELAY`-Periode bedient wird, können Validatoren diese Funktion aufrufen und mit dem stakeManager Geschäfte abwickeln (Prämien abholen, falls vorhanden, gestakte Token zurückholen, NFTs verbrennen, etc.)

## Restaken {#restake}

```cpp
function restake(uint256 validatorId, uint256 amount, bool stakeRewards)
        public;
```

- Erlaubt es Validatoren, ihren Stake zu erhöhen, indem sie neue Beträge oder Prämien oder beides einlegen.
- Die timeline(amount) MUSS für den aktiven Stake aktualisiert werden.

## withdrawRewards {#withdrawrewards}

```cpp
function withdrawRewards(uint256 validatorId)
        public;
```

- Erlaubt es Validatoren, akkumulierte Prämien abzuheben, muss damit rechnen, Prämien vom Delegations-Contract zu erhalten, wenn der Validator die Delegation akzeptiert.

## updateSigner {#updatesigner}

```cpp
function updateSigner(uint256 validatorId, bytes memory signerPubkey)
        public
```

- Erlaubt es Validatoren, die Signer-Adresse zu aktualisieren (die verwendet wird, um Blöcke auf der Polygon-Chain und Checkpoint-Signaturen im stakeManager zu validieren)
- Sobald das Slashing implementiert ist, wird gedeckelt, wie oft ein Validator den Signer-Key ändern kann.

### topUpForFee {#topupforfee}

```cpp
function topUpForFee(uint256 validatorId, uint256 heimdallFee) public
```

- Validatoren können ihr Saldo für Heimdall-Gebühren auftoppen.

## claimFee {#claimfee}

```cpp
function claimFee(
        uint256 validatorId,
        uint256 accumSlashedAmount,
        uint256 accumFeeAmount,
        uint256 index,
        bytes memory proof
    ) public
```

- Wird verwendet, um Gebühren von Heimdall abzuheben.
- `accountStateRoot` wird auf jedem Checkpoint aktualisiert, damit Validatoren in dieser Root einen Proof-of-Inclusion für den Heimdall-Account und die Abhebungsgebühr vorweisen können.
- Beachte, dass `accountStateRoot` neu geschrieben wird, um Exits auf mehreren Checkpoints zu verhindern (für alte Root und zum Abspeichern der Abrechnung im stakeManager)
- `accumSlashedAmount` ist ein nicht verwendeter Geldautomat, der, wenn erforderlich, für das Slashing auf Heimdall eingesetzt werden wird.

### StakingNFT {#stakingnft}

- Standard-ERC721 mit wenigen Einschränkungen wie ein Token pro Benutzer und Minting in Abfolgen.

## Ersetzen von Validatoren {#validator-replacement}

- Um schlecht performende Validatoren zu ersetzen, finden regelmäßige Auktionen für jeden Validator-Slot statt.
- Für einzelne Validatoren gibt es ein Auktionsfenster, in welchem Benutzer, die sich als Validatoren aufstellen möchten, ihren Betrag bieten und eine Aktion starten können, indem sie die `startAuction`-Funktion verwenden.
- Sobald `auctionInterval` vorbei ist, muss der letzte Bieter die Auktion schließen, um sie zu bestätigen und Validator werden zu können. Hierfür muss er/sie den `confirmAuctionBid` aufrufen, welcher wiederum annimmt und sich für den werdenden Validator ähnlich zur neuen `stake`-Funktion und `unStake` für den alten Validator verhält.
- Der aktuelle Validator kann für sich selbst bieten und versuchen, seinen Platz zu halten.
- Der gesamte Mechanismus balanciert den Stake-Wert und die allgemeine Sicherheit je nach Marktbedingungen und dem Einsatz der Polygon-Chain auf dynamische Weise aus.

### startAuction {#startauction}

    ```jsx
    function startAuction(
    	uint256 validatorId, /**  auction for validator */
      uint256 amount /**  amount greater then old validator's stake */
    	) external;
    ```

    - Diese Funktion wird verwendet, um ein Gebot zu veranlassen oder in bereits laufenden Auktionen höher zu bieten.
    - Die Auktionszeit läuft in Zyklen wie `(auctionPeriod--dynasty)--(auctionPeriod--dynasty)--(auctionPeriod--dynasty)` , also MUSS es die richtige Auktionszeit abpassen.
    - `perceivedStakeFactor` wird verwendet, um den genauen factor*old stake zu berechnen (Beachte, dass der Standard derzeit bei 1 WIP liegt, um die Funktion auszuwählen).
    - Es MUSS die Auktion der letzten Auktionsperiode überprüft werden, wenn diese immer noch läuft (man hat die Option, `confirmAuction` nicht aufzurufen, um sein Kapital in der nächsten Auktion herauszuholen).
    - Normalerweise läuft die englische Auktion ohne Unterbrechung in einer `auctionPeriod` .

### confirmAuctionBid {#confirmauctionbid}

    ```jsx
    function confirmAuctionBid(
            uint256 validatorId,
            uint256 heimdallFee, /** for new validator */
            bool acceptDelegation,
            bytes calldata signerPubkey
        ) external
    ```

    - Es MUSS sichergestellt werden, das es sich nicht um eine auctionPeriod handelt.
    - Wenn der letzte Bieter der Inhaber des `validatorId` ist, sollte das Verhalten ähnlich sein wie bei einem Restake.
    - Im zweiten Fall, nimm einen unStake vor `validatorId`und füge einen neuen Benutzer als Validator vom nächsten Checkpoint hinzu, da das Verhalten für den neuen Benutzer ähnlich sein sollte, wie stake/stakeFor.

## checkSignatures {#checksignatures}

```cpp
function checkSignatures(
        uint256 blockInterval,
        bytes32 voteHash,
        bytes32 stateRoot,
        bytes memory sigs
    ) public
```

- Die Writes sind nur für den Root-Chain-Contract gedacht, wenn Checkpoints eingereicht werden.
- `voteHash`, auf welchem alle Validatoren unterschreiben (BFT ⅔+1-Vereinbarung)
- Diese Funktion validiert nur die eindeutigen Signaturen und Kontrollen, da die ⅔+1-Bemächtigung auf der Checkpoint-Root unterschrieben wurde (Miteinbeziehung in `voteHash`-Verifizierung im RootChain-Contract für alle Daten) `currentValidatorSetTotalStake` stellt den aktuellen aktiven Stake zur Verfügung.
- Prämien werden proportional zum Stake des Validators ausgeschüttet, mehr zu Prämien im nachstehenden Dok.

Prämien-Ausschüttung

### isValidator {#isvalidator}

- Überprüft, ob der gegebene Validator der aktive Validator für die aktuelle Epoche ist.

### Datenstruktur der Timeline {#timeline-data-structure}

```cpp
struct State {
        int256 amount;
        int256 stakerCount;
    }
mapping(uint256 => State) public validatorState;
```

<img src={useBaseUrl("img/staking_manager/staking_manager.png")} />

Diagramm, dass die Datenstruktur der Timeline erklärt werden soll

---

# StakingInfo {#stakinginfo}

Quelle: [StakingInfo.sol](https://github.com/maticnetwork/contracts/blob/develop/contracts/staking/StakingInfo.sol)

Der zentralisierte Logging-Contract sowohl für den Validator als auch für Delegationsereignisse enthält nur wenige „Read Only“-Funktionen.

# ValidatorShareFactory {#validatorsharefactory}

Der Factory-Contract, um den `ValidatorShare`-Contract für jeden Validator, der sich dazu für die Delegation entscheidet, bereitzustellen.

---

HINWEIS: `jail`, `unJail` und -`slash`Funktion werden derzeit nicht verwendet (Teil des Slashings)