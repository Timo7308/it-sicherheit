Informationssicherheit, 4. Übung
================================

* * * * *

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Das folgende C-Programm ist
offensichtlich anfällig gegen Stack-basierte Buffer-Overflows.

``` c
#include <stdio.h>

void foo(int attempt) {
    int number = attempt + 1;
    char input[8];

    printf("Type a string: ");
    gets(input);
    printf("Your input number %d was '%s'.\n", number, input);
}

int main() {
  int i;
  for (i = 0; i < 3; ++i) foo(i);
  return 0;
}
```

Probiert dieses Programm mit verschiedenen Compilern (z.B. gcc, clang)
und gern auch mit verschiedenen Compiler-Versionen und -Optionen aus;
dazu können auch die Rechner in E0 (m01, x01, ...) zum Einsatz kommen.
Legt Euch dazu am besten Eingabedateien mit verschieden langen Zeilen
zurecht oder erzeugt den Input per Kommandozeile wie in

``` ruby
ruby -e 'puts "x"*99'
```

(Passt auch gern die 3 oben an die Anzahl der Beispiele in Eurer
Eingabedatei an.)

Dokumentiert, was passiert, wenn Ihr die vorgesehene Eingabelänge
erst vorsichtig und dann immer mehr überschreitet.

Nennt in eurer Abgabe auch das benutzte Betriebssystem, den Compiler
(inklusive Versionsnummern) und die Compiler-Optionen.

Erklärt das bei verschiedenen Eingabelängen und verschiedenen
Plattformen/Compilern zu beobachtende Verhalten.

Benutzt statt `gets` eine geeignetere Bibliotheksfunktion, und
überzeugt Euch, dass das Programm sich sinnvoller verhält. <br />
<br />
Lösung: `fgets(input, 8, stdin)`

1. Parameter: Zeiger auf das Char-Array, welches die Zeichenkette speichert.
2. Parameter: Maximale Anzahl an Chars (inklusive Null-Terminierung); verhindert Buffer-Overflow.
3. Parameter: Zeiger auf das FILE-Objekt, aus welchem gelesen wird.


* * * * *

Abgabe
------

bis 2021-11-18 23:59 UTC, digital in Stud.IP (und im
Fachbereichsnetz). Dabei bitte in der Markdown-Datei alle
Gruppenmitglieder namentlich (und mit FB3-Login) nennen. Ebenso die
Nummer Eurer Gruppe in Stud.IP.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen bedient (Anleitungen, Howtos,
andere Gruppe, etc), gebt diese bitte an (Quellen aus dem Netz bitte
gleich als URI).

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
