---
id: full-node-binaries
title: Führe einen vollständigen Knoten mit Binärdateien aus
description: Bereitstellung eines Full Polygon Knotens mit Binärdateien
keywords:
  - docs
  - matic
  - polygon
  - node
  - binaries
  - deploy
  - run full node
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

Dieses Tutorial führt dich durch das Starten und Ausführen eines vollständigen Knotens mit Binärdaten. Für die Systemanforderungen findest du im Leitfaden [Minimum Technical Requirements](technical-requirements.md).

:::tip

Die Schritte in dieser Anleitung beinhalten das Warten auf eine vollständige Synchronisierung der Dienste Heimdall und Bor. Dieser Vorgang dauert mehrere Tage.

Alternativ kannst du einen gewarteten Snapshot verwenden, wodurch die Synchronisierungszeit auf wenige Stunden verkürzt wird. Ausführliche Anweisungen finden Sie unter [<ins>Snapshot Instructions für Heimdall und Bor</ins>](/docs/develop/network-details/snapshot-instructions-heimdall-bor).

Für Snapshot Download-Links findest du auf der Seite [<ins>Polygon Chains Snapshots</ins>](https://snapshots.polygon.technology/) auf.

:::

## Übersicht {#overview}

- Bereite die Maschine vor
- Installiere Heimdall und Bor Binärdateien auf dem vollen node
- Richte Heimdall und Bor Services auf dem vollen node ein.
- Konfiguriere den vollen node
- Starte den vollen node
- Den Knotenstatus in der Community überprüfen

:::note

Du musst die exakt skizzierte Sequenz von Aktionen befolgen, sonst wirst du in Probleme laufen.

:::

### Installieren`build-essential`

Dies ist für deinen vollen Knoten **erforderlich.** Um die Installation zu installieren, führe den folgenden Befehl aus:

```bash
sudo apt-get update
sudo apt-get install build-essential
```

### Installiere GO {#install-go}

Dies ist auch **erforderlich,** um deinen vollen Knoten auszuführen. Die Installation **von v1.18 oder höher** wird empfohlen.

```bash
wget https://raw.githubusercontent.com/maticnetwork/node-ansible/master/go-install.sh
bash go-install.sh
sudo ln -nfs ~/.go/bin/go /usr/bin/go
```

## Binärdateien installieren {#install-binaries}

Polygon node besteht aus 2 Ebenen: Heimdall und Bor. Heimdall ist eine tendermint die Verträge parallel zum Ethereum-Netzwerk überwacht. Bor ist im Grunde eine Geth Fork, die Blöcke generiert, die von Heimdall-Knoten gemischt werden.

Beide Binärdateien müssen installiert und in der richtigen Reihenfolge ausgeführt werden, um richtig zu funktionieren.

### Heimdall {#heimdall}

Installiere die neueste Version von Heimdall und verwandten Services. Vergewissere dich, dass du dich auf die richtige [Release-Version](https://github.com/maticnetwork/heimdall/releases) austauscht. Beachten Sie, dass die neueste Version, [Heimdall v.0.3.0](https://github.com/maticnetwork/heimdall/releases/tag/v0.3.0), Verbesserungen enthält, wie:
1. Einschränkung der Datengröße in der state sync txs auf:
    * **30 kB** bei Darstellung in **Byte**
    * **60Kb** wenn als **String** dargestellt
2. Erhöhung der **Verzögerungszeit** zwischen den Vertragsereignissen verschiedener Validatoren, um sicherzustellen, dass der Speicherpool im Falle einer Häufung von Ereignissen nicht sehr schnell gefüllt wird, was den Fortschritt der Chain behindern könnte.

Im folgenden Beispiel wird gezeigt, wie die Datengröße eingeschränkt ist:

```
Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4
```

Um **Heimdall** zu installieren, führe die folgenden Befehle aus:

```bash
cd ~/
git clone https://github.com/maticnetwork/heimdall
cd heimdall

# Checkout to a proper version, for example
git checkout v0.3.0
git checkout <TAG OR BRANCH>
make install
source ~/.profile
```

Damit werden die Binärdateien `heimdalld` und `heimdallcli` installiert. Überprüfe die Installation, indem du die Heimdall-Version auf deinem Rechner überprüfst:

```bash
heimdalld version --long
```

### Bor {#bor}

Installiere die neueste Version von Bor. Vergewissere dich, dass du den Checkout auf die richtige [freigegebene Version](https://github.com/maticnetwork/bor/releases) git hast.

```bash
cd ~/
git clone https://github.com/maticnetwork/bor
cd bor

# Checkout to a proper version
# For e.g: git checkout 0.3.3
git checkout <TAG OR BRANCH>
make bor
sudo ln -nfs ~/bor/build/bin/bor /usr/bin/bor
sudo ln -nfs ~/bor/build/bin/bootnode /usr/bin/bootnode
```

Damit werden die Binärdateien `bor` und `bootnode` installiert. Überprüfe die Installation, indem du die Bor Version auf deinem Rechner überprüfst:

```bash
bor version
```

## Knotendateien konfigurieren {#configure-node-files}

### Start-Repo abrufen {#fetch-launch-repo}

```bash
cd ~/
git clone https://github.com/maticnetwork/launch
```

### Startverzeichnis konfigurieren {#configure-launch-directory}

Um das Netzwerkverzeichnis einzurichten, sind der Netzwerkname und die Art des Knotens erforderlich.

**Verfügbare Netzwerke**: `mainnet-v1`und`testnet-v4`

**Knotentyp**:`sentry`

:::tip

Für die Mainnet und Testnet verwenden Sie entsprechend `<network-name>`. Verwenden Sie `mainnet-v1`für Polygon mainnet und `testnet-v4`für Mumbai Testnet.
:::

```bash
cd ~/
mkdir -p node
cp -rf launch/<network-name>/sentry/<node-type>/* ~/node
```

### Netzwerkverzeichnisse konfigurieren {#configure-network-directories}

**Heimdall Dateneinrichtung**

```bash
cd ~/node/heimdall
bash setup.sh
```

**Bor Dateneinrichtung**

```bash
cd ~/node/bor
bash setup.sh
```

## Servicedateien konfigurieren {#configure-service-files}

Datei mit entsprechender `service.sh`herunterladen.`<network-name>` Verwenden Sie `mainnet-v1`für Polygon mainnet und `testnet-v4`für Mumbai Testnet.

```bash
cd ~/node
wget https://raw.githubusercontent.com/maticnetwork/launch/master/<network-name>/service.sh
```

Erstelle die **Metadaten-Datei:**

```bash
sudo mkdir -p /etc/matic
sudo chmod -R 777 /etc/matic/
touch /etc/matic/metadata
```

Generiere `.service`Dateien und kopiere sie in das Systemverzeichnis:

```bash
cd ~/node
bash service.sh
sudo cp *.service /etc/systemd/system/
```


## Konfigurationsdateien einrichten {#setup-config-files}

- Melde dich beim Remoteserver/VM an
- Du musst ein paar Details in der `config.toml`-Datei hinzufügen. Um die Datei zu öffnen und zu bearbeiten, `config.toml`führe den folgenden Befehl aus: .`vi ~/.heimdalld/config/config.toml`

In der Konfigurationsdatei musst du Informationen ändern und `Moniker``seeds`hinzufügen:

    ```bash
    moniker=<enter unique identifier>
    # For example, moniker=my-sentry-node

    # Mainnet:
    seeds="f4f605d60b8ffaaf15240564e58a81103510631c@159.203.9.164:26656,4fb1bc820088764a564d4f66bba1963d47d82329@44.232.55.71:26656"

    # Testnet:
    seeds="4cd60c1d76e44b05f7dfd8bab3f447b119e87042@54.147.31.250:26656,b18bbe1f3d8576f4b73d9b18976e71c65e839149@34.226.134.117:26656"
    ```

    - Ändere den Wert von **Pex** auf `true`
    - Ändere den Wert von **Prometheus** auf `true`
    - Lege den `max_open_connections`-Wert auf `100` fest

Vergewissere dich, dass du **die richtige Formatierung behältst, wenn** du die oben genannten Änderungen vornimmst.

- Konfiguriere Folgendes in `~/.heimdalld/config/heimdall-config.toml`:

    ```jsx
    eth_rpc_url=<insert Infura or any full node RPC URL to Goerli>
    ```

- Öffne die `start.sh`Datei für Bor mit diesem Befehl: .`vi ~/node/bor/start.sh` Füge die folgenden Flaggen hinzu, um Params zu starten:

  ```bash
  # Mainnet:
  --bootnodes "enode://0cb82b395094ee4a2915e9714894627de9ed8498fb881cec6db7c65e8b9a5bd7f2f25cc84e71e89d0947e51c76e85d0847de848c7782b13c0255247a6758178c@44.232.55.71:30303,enode://88116f4295f5a31538ae409e4d44ad40d22e44ee9342869e7d68bdec55b0f83c1530355ce8b41fbec0928a7d75a5745d528450d30aec92066ab6ba1ee351d710@159.203.9.164:30303"

  # Testnet:
  --bootnodes "enode://320553cda00dfc003f499a3ce9598029f364fbb3ed1222fdc20a94d97dcc4d8ba0cd0bfa996579dcc6d17a534741fb0a5da303a90579431259150de66b597251@54.147.31.250:30303"
  ```

- Um **den** Archiv-Modus zu aktivieren, kannst du die folgenden Flags in der Datei `start.sh`hinzufügen:

  ```jsx
  --gcmode 'archive' \
  --ws --ws.port 8546 --ws.addr 0.0.0.0 --ws.origins '*' \
  ```

## Starte die Dienste {#start-services}

Führe den vollständigen Heimdall-Knoten mit diesen Befehlen auf deinem Sentry Node aus:

```bash
sudo service heimdalld start
sudo service heimdalld-rest-server start
```

Du musst nun sicherstellen, dass **Heimdall** vollständig synchronisiert ist, und dann nur Bor starten. Wenn du Bor ohne vollständige Synchronisierung von Heimdall startest, werden häufig Probleme auftreten.

**Um zu überprüfen, ob Heimdall synchronisiert ist**
  1. Führe `curl localhost:26657/status` auf dem Remoteserver/VM aus
  2. In der Ausgabe sollte der `catching_up`-Wert `false` sein

Sobald Heimdall synchronisiert ist, führe den folgenden Befehl aus:

```bash
sudo service bor start
```

## Logs {#logs}

Protokolle können vom `journalctl`linux-Tool verwaltet werden. Hier ist ein Tutorial für fortgeschrittene Nutzung: [Wie man Journalctl zum Anzeigen und Manipulieren von Systemd verwendet](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs).

**Prüfe die Heimdall-Knotenprotokolle**

```bash
journalctl -u heimdalld.service -f
```

**Überprüfe Heimdall Rest-server**

```bash
journalctl -u heimdalld-rest-server.service -f
```

**Überprüfe Bor Rest-server**

```bash
journalctl -u bor.service -f
```

## Einrichtung von Ports und Firewall {#ports-and-firewall-setup}

Öffne die Ports 22, 26656 und 30303 für die Welt (0.0.0.0/0) auf der Sentry-Knoten-Firewall.

Du kannst VPN verwenden, um den Zugriff auf Port 22 gemäß deiner Anforderung und Sicherheitsrichtlinien zu beschränken.
