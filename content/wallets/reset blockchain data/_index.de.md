---
title: Zurücksetzen Blockchain Daten
weight: 3
pre: "<b>3. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/wallet.png"  >}}

## Einleitung

Dieses Handbuch behandelt das Zurücksetzen der Blockchain Daten, bedeutet löschen und das erneute Synchronisieren des PIRL Nautilus Wallet.
Die wahrscheinlichste Situation in der dies erforderlich ist besteht darin, dass dein Pirl Wallet nicht mehr richtig geladen wird oder nicht synchronisiert werden kann.
Befolge in diesem Fall die folgenden Anweisungen, um das Problem zu beheben.

## Wichtiger Hinweis

{{% notice warning %}}

Bevor dieser Vorgang ausführt wird, sollte ein Backup der Keystore Daten des PIRL Wallets erstellt werden. Eine Anleitung dazu findest du hier:
[Wie man ein Backup des Pirl Wallets erstellt]({{< ref "/wallets/backup pirl wallets" >}})

{{% /notice %}}

## Löschen der Blockchain Daten

Nachdem sichergestellt ist, dass die Keystore Wallet-Daten gesichert sind, ist der Rest des Vorgangs unkompliziert und läuft wie folgt ab:

 * **Schließe das Pirl Nautilus Wallet**
 * **Lokalisiere & Lösche im Pirl Ordner den chaindata folder**
 * **Öffnen des Pirl Wallet**

### Lokalisierung der Daten

Unter Windows sind die Daten hier:

`C:\Users\*YourUsername*\AppData\Roaming\Pirl\pirl`

Bei Linux findest du sie hier:

`~/.pirl`

Und auf MacOS X ist es hier:

`~/Library/Pirl`

## Zusammenfassung

Die Blockchain Daten sollten jetzt zurückgesetzt sein, wodurch in der Regel die meisten Probleme im Zusammenhang mit dem Wallet behoben werden.
Beachte beim erneuten Öffnen des Wallets, dass die Blockchain Daten erneut heruntergeladen werden müssen, was einige Zeit in Anspruch nehmen kann.

---
Author(s):

@dptelecom

Contributor(s):

@packetflow
