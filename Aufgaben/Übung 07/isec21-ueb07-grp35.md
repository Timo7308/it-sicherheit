Informationssicherheit, 7. Übung
================================

von Gruppe **G35** 
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

* * * * *

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

**Entschlüsselter Text:**

Fuer diese Aufgabe haben wir den Text ein wenig verschluesselt, damit es nicht zu einfach wird. Wie nennt man die Art der Verschluesselung die wir hier angewendet haben? Wieso ist sie so einfach zu knacken? Welches Vorgehen ist zum Entschlüsseln solcher Nachrichten am besten? Wie seid ihr vorgegangen, um auf den Klartext zu kommen? Gebt den kompletten unverschluesselten Text in eurer Abgabe an. Verwendet dafür eine Markdown-Code-Umgebung.

Modernere Verfahren sind meist nicht so leicht zu brechen. Welche wichtige Rolle spielt dabei die Laenge des Schluessels? Welche Schluessellaenge empfehlt ihr fuer den Einsatz mit AES, fuer welche Arten von Anwendungen sind welche Schluessellaengen empfehlenswert? Berechnet, wie lange euer Rechner in etwa brauchen würde, um bei Verwendung dieses Verfahrens einen Schluessel der empfohlenen Laenge zu brechen.

***

**Beantwortung der Fragen:**

Beim Verschlüsselungsverfahren des Textes handelt es sich um die Monoalphabetische Substitution. Bei dieser Verschlüsselung wird jeder Buchstabe im Alphabet durch einen anderen vertauscht. Das Verfahren kann aufgrund der Häufigkeitsverteilung von Buchstaben sehr leicht gebrochen werden. Die häufigsten Buchstaben im Deutschen sind beispielsweise E, I und N. Man kann nun schauen, welche Buchstaben im verschlüsselten Text am häufigsten vorkommen. Diese vertauscht man dann mit E, I und N. Die weiteren Buchstaben werden basierend auf ihrer Häufigkeit in der deutschen Sprache und ihrer Häufigkeit im Text miteinander vertauscht. Umso mehr Buchstaben scheinbar korrekt zugeteilt worden, desto leichter lässt sich der Text aus dem sprachlichen Kontext erschließen. Wir haben für die Entschlüsselung des Textes einen Online-Cryptogram-Solver zur Hilfe genommen. Dieser nutzt den Ansatz der Vertauschung von Buchstaben. Im Unterschied zur Entschlüsselung per Hand werden dort tausende Möglichkeiten ausprobiert. 

Die Schlüssellänge modernerer Verfahren beschreibt die Anzahl verschiedener möglicher Schlüssel. Je größer die Schlüssellänge ist, desto schwieriger wird es ein Verfahren zu brechen. Für die Verwendung von AES wäre eine Schlüssellänge von mindestens 128 Bit sinnvoll, wie es im Allgemeinen auch von Behörden empfohlen wird. Bei einem Brute-Force-Angriff bräuchte man 2^128 Versuche um die Verschlüsselung zu brechen. Dies würde auf einem normalen, aktuellen Computer extrem lange dauern. 

Der Laptop(MacBook Pro 2020)von Timo soll nach Angaben von Apple eine Rechenleistung von 2,6 Teraflops(2,6*10^12) haben. Das entspricht 2,6 Billionen Rechenoperationen pro Sekunde. Um eine AES 128 Bit Verschlüsselung zu knacken bräuchte es 2^128 Versuche. Dies entspricht etwa 340 Sextillionen Rechenoperationen pro Sekunde. Der Laptop bräuchte also etwa 4e18 Jahre, um die Verschlüsselung zu knacken.

Berechnung: 

`((2^128)/(2,6*(10^12)))/60/60/24/365)`


Eine noch größere Schlüssellänge von 192 oder 256 Bit ist aber dennoch sehr sinnvoll, da große Organisationen oder Geheimdienste eine beachtliche Rechenleistung zur Verfügung haben.




* * * * *

Aufgabe 2, 4 Punkte, Gruppe
----------------------------

Der Eintrag "2000Euro" wird beim Einlesen als `2000Euro\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0` dargestellt. Als Hash wird für diese Eingabe folgender Wert gespeichert:`LWWWRNKHAAAAAAA`.
Der neue Eintrag mit "20Euro" muss also auch mit der Hashfunktion diesen selben Hashwert berechnen.

Betrachten wir nun also den Hash von "20Euro": `LWRNKHAAAAAAAAA`. Der Hash sieht schon sehr ähnlich zu dem von "2000Euro" aus. Dies liegt an der definierten Hashfunktion. Die Funktion nimmt eine 32 Zeichen langen String entgegen und gibt dann am Ende einen 16 Zeichen langen Hash aus. Der ASCII-Wert jedes Zeichens ist dabei ausschlaggebend zu welchem Hash-Zeichen (zwischen A-Z) dieser umgerechnet wird. Es wird aus einem 32 Byte langen String ein 16Byte langer Hash. Hierbei wird durch die Verwendung von `%15` jedes Hash-Byte zweimal berechnet. Somit ist das erste Zeichen des Hashes von dem ersten und 17. (0 und 16, wenn wir von 0 an zählen) Zeichen der Eingabe abhängig. Hierbei ist zu beachten, dass `\0` einen ASCII-Wert von `0` hat und somit beim doppelten Berechnen des Hash-Zeichens keine Änderung vornimmt.

Nun lassen sich auch die zwei fehlenden `WW` in den beiden Hashes erklären. Dies liegt bei der Eingabe an den fehlenden zwei `00` bei "20Euro" und "2000Euro". 
Um den gleichen Hash-Wert nun zu berechnen, müssen wir also die Eingabe `20Euro\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0` anpassen. Wir wissen, dass die ersten zwei Zeichen des Hashes gleich sind, müssen also erst ab dem  18. Byte Änderungen vornehmen. Zur Erinnerung: Byte 3 und Byte 18 sind für das 3.Zeichen im Hash verantwortlich. 

Folgende Eingabe führt dann zu dem selben Hash-Wert `LWWWRNKHAAAAAAA`: `20Euro\0\0\0\0\0\0\0\0\0\0\0SWUTXU\0\0\0\0\0\0\0\0\0`.

Bei dem Anzeigen eines Strings wird alles ausgegeben, bis ein Null-Char `\0` gelesen wird. Somit sollte in dem Text-Dokument auch nur "20Euro" angezeigt werden, obwohl noch weiter Chars nach dem NUL-Char folgen.


Gegenmaßnahmen: 
Durch Verwendung einer standardisierten Hashfunktion kann das Manipulieren der Einträge gehindert werden.


Wir haben für die Aufgabe 2 ein Hinweis von der Gruppe g11 erhalten, dass wir Byte 18 und folgende durch `SWUTXU` ersetzen sollen. Die erste Idee von uns war es mit `%` und einem Latex-Kommentar den selben Hash-Wert zu erzeugen, was aber zu keinem erfolgreichen Ergebnis führte.







* * * * *

**Quellen:**

- Gruppe g11
- https://www.duden.de/sprachwissen/sprachratgeber/Die-haufigsten-Buchstaben-deutschen-Wortern
- https://www.apple.com/de/newsroom/2020/11/apple-unleashes-m1/
- https://www.boxentriq.com/code-breaking/cryptogram
