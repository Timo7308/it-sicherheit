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

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet
- Bei Eingaben mit einer längeren Zeichenkette wird ein: `abort trap: 6` ausgegeben

  Beispielausgabe: <br />
       "Your input number %d was '%s'.\n", 1, 'xxx'. <br />
       "Your input number %d was '%s'.\n", 2, 'xxxxxxx'. <br />
       "Your input number %d was '%s'.\n", 3, 'xxxxxxxx'. <br />
  Die ersten beiden Eingaben wurden ohne Probleme kompiliert. Nach der letzten Eingabe wird der Fehler `abort trap: 6` geworfen, da die Eingabe länger als das   Char-Array ist. In diesem Fall wird versucht auf unautorisierten Speicher zu schreiben. Es ist zu beachten, dass immer ein Character als Nullterminierung hinzugefügt wird, weswegen die Eingabe aus acht Charactern nicht mehr in das Array mit der Größe Acht passt. 
<br />

Ausführung: gcc | version ... | option standard



Ausführung: clang | version 12.0.0 | option


. <br />
<br />

Benutzt statt `gets` eine geeignetere Bibliotheksfunktion, und
überzeugt Euch, dass das Programm sich sinnvoller verhält. <br />
<br />
Lösung: `fgets(input, 8, stdin)`

1. Parameter: Zeiger auf das Char-Array, welches die Zeichenkette speichert.
2. Parameter: Maximale Anzahl an Chars (inklusive Null-Terminierung); verhindert Buffer-Overflow.
3. Parameter: Zeiger auf das FILE-Objekt, aus welchem gelesen wird.


* * * * *
