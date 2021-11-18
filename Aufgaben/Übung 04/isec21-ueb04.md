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

**Dokumentation:**
Alle folgenden Beobachtungen wurden auf dem Apple m0-Rechner durchgeführt. <br />

Ausführung: gcc | version ... | option standard (gcc -o standard buffer.c)

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet (siehe Beispielausgabe)
- Bei Eingaben mit einer längeren Zeichenkette wird ein: `abort trap: 6` ausgegeben.

  Beispielausgabe: <br />
       "Your input number %d was '%s'.\n", 1, 'xxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 3, 'xxxxxxxx'. <br />
  Die ersten beiden Eingaben wurden ohne Probleme kompiliert wie es vom Code erwartet wird. Nach der letzten Eingabe wird der Fehler `abort trap: 6` geworfen, da die Eingabe länger als das Char-Array ist. In diesem Fall wird versucht auf unautorisierten Speicher zu schreiben. Es ist zu beachten, dass immer ein Character als Nullterminierung hinzugefügt wird, weswegen die Eingabe aus acht Charactern und der Nullterminierung nicht mehr in das Array mit der Größe Acht passt. 
Alle noch längeren Eingaben mit einigen Dutzend Chars führen zum selben Ergebnis.
<br />


Ausführung: gcc | version 7.4.0

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet
- Bei Eingaben mit einer längeren Zeichenkette wird ein: `*** buffer overflow detected ***: 43517400/a.out terminated Abort signal from abort(3) (SIGABRT)` ausgegeben.

  Beispielausgabe: <br />
       "Your input number %d was '%s'.\n", 1, 'xxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 3, 'xxxxxxxx'. <br />
  Für dieses Beispiel wurden die selben Zeichenketten verwendet wie in der oberen Version. Die dritte Eingabe führt dies mal zu dem anderen Fehler.     
<br />


Ausführung: clang | version 6.0.0

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet
- Bei Eingaben mit einer längeren Zeichenkette wird **kein** Fehler geworfen.

  Beispielausgabe: <br />
       "Your input number %d was '%s'.\n", 1, 'xxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 3, 'xxxxxxxx'. <br />
  In diesem Beispiel wird keine Fehlermeldung geworfen. Es ist sehr anfällig für Buffer-Overflows, weil anliegender Speicher mit den Chars überschrieben wird, welche die Größe des Arrays überschreiten. Umso länger der Eingabestring ist, desto mehr Speicher wird überschrieben und dementsprechend fataler können die Folgen sein.   
<br />


Ausführung: clang | version 8.0

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet
- Bei Eingaben mit einer längeren Zeichenkette wird **kein** Fehler geworfen.

  Beispielausgabe: <br />
       "Your input number %d was '%s'.\n", 1, 'xxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 3, 'xxxxxxxx'. <br />
  Es liegt das gleiche Verhalten vor, wie schon bei dem Test mit clang version 6.0.0
<br />


Ausführung: vc | version 



Rechner: x01 | Betriebssystem: Ubuntu | Ausführung: gcc | version 10.3.0 | option standard 

- Bei einer Eingabe von acht chars oder weniger terminiert das Programm wie im Code erwartet. 
- Bei Eingaben mit einer längeren Zeichenkette wird: `*** stack smashing detected ***: <unknown> terminated Aborted (core dumped)` ausgegeben. 







. <br />
<br />

* * * * *

Benutzt statt `gets` eine geeignetere Bibliotheksfunktion, und
überzeugt Euch, dass das Programm sich sinnvoller verhält. <br />
<br />
Lösung: `fgets(input, 8, stdin)`

1. Parameter: Zeiger auf das Char-Array, welches die Zeichenkette speichert.
2. Parameter: Maximale Anzahl an Chars (inklusive Null-Terminierung); verhindert Buffer-Overflow.
3. Parameter: Zeiger auf das FILE-Objekt, aus welchem gelesen wird.

Nach dieser Änderung terminiert das Programm immer. Es werden pro Schleifendurchlauf (pro Einleisung in das Char-Array) nur maximal sieben Chars + Nullterminierung dafür verwendet, weil ansonsten nicht nur im Speicherbereich des Char-Arrays geschrieben werden würde. Außerdem wird immer nur bis zu einem '\n' (newline) eingelesen.

Datei: 'xxxxxxxxxxxf
       ffffffffffffw'
Beispielausgabe mit i < 3: <br />
       "Your input number %d was '%s'.\n", 1, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxf'. <br />
       "Your input number %d was '%s'.\n", 3, 'fffffff'. <br />

* * * * *
