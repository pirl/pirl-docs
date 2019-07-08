---
title: Wie man ein Backup des Pirl Wallets erstellt
weight: 2
pre: "<b>2. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/wallet.png"  >}}


## Überblick
Dies ist ein Leitfaden für Best Practices (bewährte Methoden) zum Sichern deines Pirl Wallets und zur sicheren Aufbewahrung von Pirl.


## Einleitung
Also, du hast dir gerade einige Pirl geholt, vielleicht für eine Langzeitinvestition und möchtest diese für eine gewisse Zeit halten. Wie kannst du nun sicherstellen, auf diese nicht durch Feuer/Diebstahl/Systemabsturz den Zugriff zu verlieren?
Es ist wichtig eine Sicherheitskopie deines Pirl Wallets zu haben, um dafür zu sorgen dass bei einem Problem deine Pirl nicht verloren gehen. In diesem Handbuch werden bewährte Verfahren für Backups erläutert und drei Plattformen/Optionen dafür beschrieben.

## Wichtig zu verstehen: Was *ist* ein Wallet?
Im Kern sind die Teile des Wallets, über den du Zugriff auf dein Guthaben bekommst und was dir erlaubt Pirl zu senden, deine privaten Schlüssel (Private Keys). Dein Pirl ist in der Blockchain gespeichert, und die privaten Schlüssel dienen dazu, dein Guthaben freizuschalten und Transaktionen durchzuführen. Diese privaten Schlüssel können in verschiedenen Arten angezeigt werden, wobei die *raw*-Form eine Zeichenfolge aus 64 hexadezimalen Zeichen ist, die ungefähr so aussieht:
```c6cbd7d76bc5baca530c875663711b947efa6a86a900a9e8645ce32e5821484e```

Die Sicherheit des privaten Schlüssels ist mehrfach wichtig. Sie ermöglichen den Zugang zu deinem Guthaben, aber sie gewähren auch jedem der über den Schlüssel verfügt Zugang zu deinem Guthaben. Aus diesem Grund ist es WICHTIG, dass Schritte unternommen werden um diese privaten Schlüssel zu schützen und Sicherheitskopien zu erstellen.
Im folgenden Abschnitt werden allgemeine Methoden zum Speichern dieser privaten Schlüssel, sowie die jeweils empfohlenen Vorgehensweisen beschrieben.

## Wallet Typen und Best Practices
Damit eine Transaktion ausgeführt werden kann, muss sie immer mit deinem privaten Schlüssel signiert sein. Für zusätzliche Funktionen, wie das Schützen des privaten Schlüssels mit einem Kennwort, stehen verschiedene Formate zum Speichern des privaten Schlüssels zur Verfügung.

Die am meisten verwendeten Wallet Typen sind:

 * **Private Key in Klartext (unverschlüsselt)**
 * **Keystore (UTC/JSON) als Datei (Passwort verschlüsselt)**
 * **Hardware Wallets (z.B. Ledger/Trezor) (Passwort verschlüsselt)**

### Private Key in Klartext (unverschlüsselt)
Dies ist eine unverschlüsselte Textversion des privaten Schlüssels. Es wird kein Passwort benötigt.
Wenn eine andere Person diesen Schlüssel hat, kann diese Person ohne Kennwort auf das Wallet zugreifen.
Das macht diese Speichermethode zur einfachsten, zugleich auch zur unsichersten Variante.

#### Speichern des privaten Schlüssels als Paper Wallet oder Keystore Datei
Es wird normalerweise empfohlen eine verschlüsselte Datei (keystore) zu verwenden. Du solltst jedoch ein Paper Wallet ausdrucken und diesen Schlüssel Offline an einem sicheren Ort aufbewahren.

Auf https://wallet.pirl.io gibt es eine nützliche Funktionen, mit denen du deine Wallet Informationen entweder als Keystore-Datei (JSON/UTC) speichern kannst, oder die Möglichkeit dein Paper Wallet als PDF zu speichern, sowie es direkt auf Papier zu drucken.

Clicke einfach auf das "View Wallet Info" Tab:
{{< imagesurlsheaders "cloud/main_pirl_wallet_page_view_wallet_highlight.png" >}}

Gebe deine Wallet Daten in dem Format ein, in dem sie vorliegen:
{{< imagesurlsheaders "cloud/view_wallet_details_landing_page.png" >}}


Deine Wallet Details werden dann als öffentlicher/privater Schlüssel angezeigt, mit den Optionen sowohl eine Keystore-Datei (JSON/UTC) zu generieren als auch ein Wallet aus Papier zu drucken.
{{< imagesurlsheaders "cloud/view_wallet_details.png" >}}

Die Wallet aus Papier sieht dann so aus:
{{< imagesurlsheaders "cloud/paper_wallet_example.png" >}}

Du solltest das Wallet zweimal ausdrucken und an zwei sicheren Orten aufbewahren. Behandele es wie Bargeld. 
Du solltest auch die Keystore-Datei herunterladen und auf einem externen Medium wie einem USB-Laufwerk oder einer externen Festplatte speichern. Im besten Fall empfiehlt es sich, ein Backup an mehreren physischen Standorten zu haben.
Denke immer an die goldene Regel für Sicherungen: "Zwei Sicherungen sind eine und eine keine."

### Keystore (UTC/JSON) als Datei (Passwort verschlüsselt)
Dies ist die empfohlene Version zum Speichern und auch das Format, in dem die Wallet Software Nautilus (Desktop) die Wallet Datei speichert.
Da das Keystore-Format mit dem Wallet unter https://wallet.pirl.io verwendeten Format übereinstimmt, kann man es problemlos in beide Richtungen importieren.


Diese Wallet Datei wird mit dem Kennwort verschlüsselt, was beim Erstellen der Datei festgelegt wurde.


Du solltest die Keystore-Datei auf einem externen Medium wie einem USB-Laufwerk oder einer Festplatte speichern. Im besten Fall empfiehlt es sich, ein Backup an mehreren physischen Standorten zu haben.

#### Sichere das Nautilus Wallet

Um dein Nautilus Wallet zu sichern, klicke auf **File** > **Backup** > **Accounts**

{{< imagesurlsheaders "cloud/nautilus_backup.png" >}}


Dadurch wird der AppData Ordner geöffnet, der deine Wallet Dateien enthält:
{{< imagesurlsheaders "cloud/nautilus_backup_folder.png" >}}



### Hardware Wallets (z.B. Ledger/Trezor) (Passwort verschlüsselt)
Hardware Wallet Support für Pirl ist sowohl für Ledger wie auch für Trezor Geräte verfügbar.
Diese Geräte bieten eine sichere Möglichkeit zum Speichern und Zugreifen auf dein Guthaben. Die privaten Schlüssel werden in einem geschützten Bereich des Geräts gespeichert, so dass sie nicht im Klartextformat (Plaintext) aus dem Gerät übertragen werden können.
Diese Methode bedeutet, dass du in der Lage sein solltest Transaktionen auf sichere Weise zu signieren, auch wenn dein Computer kompromittiert ist.
Wie bei allen Technologien gibt es Mittel und Wege um diese Geräte anzugreifen, die potenziell dein Geld gefährden könnten. Dies geht jedoch über den Rahmen dieses Artikels hinaus und ist nichts, mit dem sich der durchschnittliche Benutzer befassen muss.

Eine besondere Sicherheitsvorkehrung die getroffen werden sollte besteht darin, diese Geräte nur in Geschäften von Erstanbietern oder vertrauenswürdigen Anbietern zu erwerben und sicherzustellen, dass das Gerät beim Empfang nicht geöffnet oder anderweitig manipuliert wurde.


## Zusammenfassung
Zusammenfassend die wichtigsten Maßnahmen zur Sicherung deines Pirl:

 * Verwende nach Möglichkeit eine Hardware-Wallet, wobei der kennwortgeschützte Keystore (UTC/JSON) die nächstbeste Option ist.

 * Verwende das Pirl Web Wallet um ein Wallet auf Papier aufzubewahren und drucke es zweimal aus. Bewahre es an zwei verschiedenen sicheren Orten auf.

 * Unabhängig davon welches Wallet-Format verwendet wird, erstelle mehrere Backups an mehreren Orten.
 * Gebe einen privaten Schlüssel niemals nicht vertrauenswürdigen Dritten, da diese dadurch uneingeschränkten Zugriff auf das Konto erhalten.


---
Author(s):

@packetflow
