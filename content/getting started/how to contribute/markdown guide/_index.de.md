---
title: Markdown Anleitung
weight: 3
pre: "<b>3. </b>"
disableToc: true
---

## Einleitung

Um etwas für die PIRL Dokumentation beizutragen must du ["markdown"](https://daringfireball.net/projects/markdown/syntax) benutzen. Markdown ist eine von vielen Möglichkeiten um Dokumentationen zu erstellen. Es ist wahrscheinlich nicht das Beste aber auch nicht das Schlimmste. Der Einstieg in einen konsistenten Dokumentationszyklus ist einfach.

Im Folgenden findest du einige Beispiele für die Verwendung von Markdown, sowie unsere Empfehlungen und Best Practices (bewährte Methoden). Bitte verwende unsere Empfehlungen wenn du eine PIRL Dokumentation erstellst, damit es gut mit dem Rest des Inhalts zusammenpasst. Also schaue dir auf jeden Fall den [Style Guide]({{< ref "/getting started/how to contribute/style guide" >}}) an für zusätzliche Richtlinien zur Formatierung von Inhalten.

## Beispiel Markdown Dokument

Unten findest du ein Beispieldokument mit Markdown. Dieses Dokument wird von der Software so übersetzt, dass es wie beschrieben angezeigt wird.

{{< imagesurlsheaders "cloud/sample.jpg" >}}

## Basis Markdown Anleitung

### Haupttitel

Der Titel des Hauptdokumentes wird am oberen Rand des Dokuments mit der größten Schriftart angezeigt. Beim Markdown steht der Titel ganz oben im Dokument zwischen den Abschnitten ** `---` **, wie unten für dieses Dokument gezeigt.

```
---
title: Markdown Anleitung
weight: 5
---
```

### Überschriften

Überschriften haben in der Regel eine größe von H1 (größte) bis H6 (kleinste). Markdown ist da ähnlich wie HTML. Die Zahl welche die Größe der Überschrift darstellt wird durch ein **`#`** dargestellt. Ein einfaches **`#`** ist gleich zu **H1**, zwei **`##`** ist das Gleiche wie **H2** usw.

```
# Dies ist eine H1 Überschrift
## Dies ist eine H2 Überschrift
### Dies ist eine H3 Überschrift
#### Dies ist eine H4 Überschrift
##### Dies ist eine H5 Überschrift
###### Dies ist eine H6 Überschrift
```

> **PIRL TIP:** Die Hauptabschnitte eines Dokuments beginnen mit **##** oder H2

### Betonung

Schreibe ein Wort in Sternchen um Text *kursiv* zu schreiben. Um Text **fett** zu markieren, nutze doppelte Sternchen. Verwende zwei Tilden **~~** um Text durchzustreichen.

```
*Dieser Text wird kursiv gedruckt*
**Dieser Text wird fett gedruckt**
_**Was ist mit fett kursiv**_
~~Habe ich etwas falsches gesagt?~~
<center>Ich bin zentrierter Text</center>
```

*Dieser Text wird kursiv gedruckt*

**Dieser Text wird fett gedruckt**

_**Was ist mit fett kursiv**_

~~Habe ich etwas falsches gesagt?~~

<center>Ich bin zentrierter Text</center>

### Zitate

Um etwas zu zitieren verwende das Größer-als-Zeichen > und mache dein Zitat!
```
>**Handbuch zu diesem Artikel**: Sie müssen diesen Artikel von vorne nach hinten lesen um eine Offenbarung zu erhalten. So funktioniert doch die Literatur, oder?
(Es sei denn es ist eine Bedienungsanleitung. In diesem Fall liest sie niemand)
```
>**Handbuch zu diesem Artikel**: Sie müssen diesen Artikel von vorne nach hinten lesen um eine Offenbarung zu erhalten. So funktioniert doch die Literatur, oder?
(Es sei denn es ist eine Bedienungsanleitung. In diesem Fall liest sie niemand)

### Tabelle

Mit ein paar Markdown Anweisungen kannst du ganz einfach eine Tabelle mit verschiedener Anzahl Zeilen oder Spalten erstellen. Im Grunde werden die Spalten einfach durch eine Pipe ```|``` getrennt.

Diese ```| :-------------   | :-------------   |``` Zeile pro Spalte, nach der Überschrift, darf nicht fehlen.

Die aktuell am meisten benutzen Editoren besitzen auch Features oder Plugins um die Arbeit mit Tabellen zu erleichertern.

Hier sind zwei Beispiele:


```
| Überschrift Eins | Überschrift Zwei |
| :-------------   | :-------------   |
| Erstes Element   | Zweites Element  |
| Erstes Element   | Zweites Element  |
| Helfer Link      | Helfer Link  |
```
| Überschrift Eins | Überschrift Zwei |
| :-------------   | :-------------   |
| Erstes Element   | Zweites Element  |
| Erstes Element   | Zweites Element  |
[Wie erstelle ich Markdown Tabellen mit Atom](http://lmgtfy.com/?q=Wie%20erstelle%20ich%20Markdown%20Tabellen%20mit%20Atom&s=g)|[Wie erstelle ich Markdown Tabellen mit VS Code](http://lmgtfy.com/?q=Wie%20erstelle%20ich%20Markdown%20Tabellen%20mit%20VS%20Code&s=g)

```
|[Homepage](https://pirl.io/){:target="_blank"}|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|

```
|[Homepage](https://pirl.io/)|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|

### Listen

Sortierte Listen werden erstellt indem **1.** für das Suchelement verwendet wird und dann mit jeder folgenden Zeile erhöht wird. Ungeordnete Listen werden mit **+** erstellt.

```
1. Erstes
2. Zweites
3. Drittes

+ Satoshi
+ Vitalik
+ PIRL

1. Dies ist das Erste
  + Erste Sache
2. Das ist der Zweite
  + Zweite Sache
3. Das ist der Dritte
  + Dritte Sache

+ Dies ist das Erste
  + Erste Sache
+ Das ist der Zweite
  + Zweite Sache
+ Das ist der Dritte
    + Dritte Sache
```

1. Erstes
2. Zweites
3. Drittes

+ Satoshi
+ Vitalik
+ PIRL

1. Dies ist das Erste
  + Erste Sache
2. Das ist der Zweite
  + Zweite Sache
3. Das ist der Dritte
    + Dritte Sache

+ Dies ist das Erste
  + Erste Sache
+ Das ist der Zweite
  + Zweite Sache
+ Das ist der Dritte
  + Dritte Sache

### Links

Um Links zu erstellen füge einfach eine URL in die Klammern **()** ein. Es gibt auch ein paar zusätzliche Optionen.

```
Dies ist ein [Beispiel Link](http://example.com/ "Mit einem Titel"). Es wird auch funktionieren wenn der Link das einzige ist was eingeklammert wird.
```

Dies ist ein [Beispiel Link](http://example.com/ "Mit einem Titel"). Es wird auch funktionieren wenn der Link das einzige ist was eingeklammert wird.

### Bilder

Das Verknüpfen von Bildern ist wie das Verknüpfen mit einem Kurzcode {{< imagesurlsheaders "cloud/magic.gif" >}}

```link
* {{< imagesurlsheaders "cloud/magic.gif" >}}
```

+ {{< imagesurlsheaders "cloud/magic.gif" >}}

### Code

Es gibt zwei Möglichkeiten Code von Text zu unterscheiden. Eine für die Inline-Funktion und eine für Codeblöcke. Um den Code `inline` zu unterscheiden, setze 3 Backticks um den Code. Um dies als Textblock darzustellen, setze 3 Backticks oben und unten.

{{< imagesurlsheaders "cloud/code.jpg" >}}

```
Dies wird als Codeblock angezeigt.
Beachte vor allem die Backticks oben und unten.
```

---
Author:
@packetflow

Contributor(s):
