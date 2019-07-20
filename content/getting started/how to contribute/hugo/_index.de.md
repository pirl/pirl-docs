---
title: hugo
weight: 5
pre: "<b>5. </b>"
disableToc: true
---

Hallo und Willkommen!

Dieses Handbuch zeigt dir, wie du Hugo und den Hugo-Server direkt von der Kommandozeile aus starten kannst.

Mit Hilfe von Hugo kannst Du Artikel für die Knowledge Base erstellen, anzeigen, verbessern und etwas zur PIRL-Community beitragen.

## Überblick

In diesem Handbuch wird erklärt wie Hugo und der Hugo-Server heruntergeladen, eingerichtet und ausgeführt wird:

{{< imagesurlsheaders "cloud/Hugo.JPG" >}}

## Voraussetzungen

Um den Erfolg dieser Operation zu gewährleisten benötigst du folgende Voraussetzungen:

* Eine funktionierende Internetverbindung
* [Download der letzten Version der Hugo Startdatei (> 0.25) für dein Betriebsystem](https://github.com/gohugoio/hugo/releases)
* Lade das pirl-docs Repo von hier herunter: [Pirl-docs](https://git.pirl.io/community/pirl-docs)
* Den Web-Browser deiner Wahl und ein wenig Willenskraft

## Und los

### 1) Mac iOS

Wenn du ein Mac Benutzer bist installiere Hugo mit einem einzigen einfachen Befehl.

Kommando:

```shell
brew install Hugo
```

Folge der Installationsanleitung [hier](https://gohugo.io/getting-started/quick-start/)

### 2) Windows OS

* Wenn du Windows verwendest, lade einfach die neueste Version von [Hugo](https://github.com/gohugoio/hugo/releases) für Windows herunter, wenn du es noch nicht getan hast.
* Ebenso musst du das neueste [PIRL docs file depository](https://git.pirl.io/community/pirl-docs) Repo herunterladen, wenn du es noch nicht getan hast. Entpacke und extrahiere diese beiden Ordner.
* Dann gehe in den Hugo-Ordner und kopiere alles, was du dort finden kannst.
* Wechsele in den Ordner pirl-docs und füge dort alle HUGO Dateien ein und überschreibe alte Dateien mit den aktuelleren.
* Drücke dann die Suchtaste in der Nähe der Windows-Startleiste, meistens in der linken unteren Ecke (normalerweise ist sie hier :)).
* Schreibe *cmd* in die leere Zeile und drücke die Eingabetaste.
* Jetzt kannst du genau sehen was ich jedes Mal schreiben muss, um den Hugo Server auszuführen und um einen KnowledgeBase(KB) Artikel zu schreiben.
* Zuerst muss ich meinen Ziel Ordner finden (In diesem Fall ist es Laufwerk D:\ und einige weitere Ordner). Dann gehe ich zum Hauptverzeichnis des Repositorys wo auch die Hugo Startdatei liegt.

Kommandos im CMD:

1. C:\Users\YourComputername>D:
2. D:\>cd D:\PIRL\HUGO\pirl-docs-master\pirl-docs-master
3. Dir
4. Hugo.exe
5. Hugo.exe server
6. For shutting Hugo server down press: CTRL+C

### 3) Linux OS

Wir haben zwei Möglichkeiten zum Herunterladen, Installieren und Ausführen von Hugo erstellt. Wählen aus, was für dich in Ordnung ist.

#### a) Installation durch den Paketmanager

* Gebe die Befehl ein:

```shell
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-32bit.deb
sudo dpkg -i hugo_0.49_Linux-32bit.deb
```

#### b) Alternativ kannst du die Installation über ein Shell-Skript durchführen und anschließend ein anderes Skript für einen komfortablen, wiederholten Start verwenden

* Installationsskript

```shell
#!/bin/bash
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-64bit.tar.gz
tar -xf hugo_0.49_Linux-64bit.tar.gz
```

* Wiederholtes Startskript

```shell
#!/bin/bash
cd /path/to/hugo
ls -la
./hugo.sh &
pkill -f hugo.sh
./hugo.sh server
```

********************

## Im Web-Browser überprüfen

Starte nach Abschluss der Installation den Webbrowser und gebe folgendes ein:

```shell
http://localhost:1313
```

* Willkommen in der Matrix. Jetzt kannst du Indexdateien bearbeiten oder Neue erstellen und uns dabei helfen, weitere wissensbasierte Artikel zu erstellen.
* Wähle dazu den Texteditor der deinen Anforderungen am besten entspricht. Ich bevorzuge [Visual Studio Code] (https://code.visualstudio.com/). Es ist sehr einfach zu bedienen und bringt auch eine Git Intergration mit sich neben vielen anderen brauchbaren Plugins.

********************

---

Author(s):

@Dptelecom

Contributor(s):

@packetflow
