Informationssicherheit, 4. Übung
================================

von Gruppe **G35** 
Adrian Lindloff, Timo Schuchmann und Philias Borrmann

* * * * *

Aufgabe 1, 4 Punkte, Gruppe 
---------------------------


**Dokumentation:**
Alle folgenden Beobachtungen wurden auf dem Apple m0-Rechner durchgeführt. <br />

Ausführung: mit gcc version 12.0.0 ohne Optionen. 
```gcc -o standard buffer.c```

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet.
- Bei Eingaben mit einer längeren Zeichenkette wird ein: `abort trap: 6` ausgegeben.

  Beispielausgabe:
  ``` 
   "Your input number 1 was 'xxx'.
   "Your input number 2 was 'xxxxxxx'.
   "Your input number 3 was 'xxxxxxxx'.
  ``` 
  <br />
  Die ersten beiden Eingaben wurden ohne Probleme ausgeführt. Nach der letzten Eingabe wird der Fehler `abort trap: 6` geworfen, da die Eingabe länger als das Char-Array ist. In diesem Fall wird versucht auf unautorisierten Speicher zu schreiben. Es ist zu beachten, dass immer ein Character als Nullterminierung hinzugefügt wird, weswegen die Eingabe aus acht Charactern nicht mehr in das Array mit der Größe Acht passt. 
<br />

---

Ausführung: gcc version 12.0.0  option -fno-stack-protector

Aus der Dokumentation geht hervor, dass der `fno-stack-protector` den Stack Schutz aufhebt und somit einen Buffer-Overflow ermöglicht. 

```gcc -o noProtector buffer.c -fno-stack-protector```

- Bei Eingaben mit einer Zeichenkette von sieben Chars oder weniger terminiert das Programm wie im Code erwartet.
- Bei Eingaben mit einer längeren Zeichenkette wird folgendes ausgegeben.

  Beispielausgabe: 
       "Your input number 1 was 'xxx'.
       "Your input number 2 was 'xxxxxxx'.
       "Your input number 0 was 'xxxxxxxx'.
       "Your input number 4 was 'a'.<br />
  Die ersten beiden Eingaben wurden ohne Probleme ausgeführt. Auch bei der vorletzten Eingabe mit einer      Zeichenkette der Länge 8 läuft das Programm weiter, aber der Zähler wurde nicht wie erwartet auf 3 gesetzt, sondern gibt eine 0 aus. Hier kam es also vermutlich zu einem Buffer-Overflow und der letzte Char, der nicht mehr in das input-Array passte, wurde in den Speicherbereich von `number` geschrieben. Dieser Zugriff auf eine andere lokale Variable in dem Call-Stack wurde durch die Compiler-Option freigegben. Bei weiteren Eingaben mit einer Länge < 8 wird der Zähler wie erwartet erhöht und zeigt bei der 4. Eingabe eine 4. 

- Ist die Eingabelänge sogar viel größer, wird das Program durch ein Segmentation Fault beendet. Hierbei wird auf ein Speicherbereich zugegriffen der nun sogar außerhalb des Program-Stacks liegt. 

    ```Your input number 1953789044 was 'tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt'. Segmentation fault: 11```
    
- Bei langen Eingaben ist die Nummer des Zählers dabei abhängig von der Eingabelänge und der Verwendung von Buchstaben oder Zahlen. Die Bytes, die von dem `input` in `number` überschrieben wurden, werden bei der Ausgabe der Variable `number` wieder als Zahlen interpretiert. 
 ```
 Your input number 875770417 was '123456781234567'.
 Your input number 1633771873 was 'aaaaaaaaaaaaaaa'.
 Your input number 1650614882 was 'bbbbbbbbbbbbbbb'.
 ```
- Bei einer Eingabelänge von genau 16 terminiert das Program sofort, obwohl die Schleife nicht vollständig durchlaufen wurde. (Hierfür haben wir leider keine Erklärung gefunden.)
```
->./no_stack_protector
warning: this program uses gets(), which is unsafe.
Type a string: 1234567812345678
Your input number 875770417 was '1234567812345678'.
borrmann@m01 /home/borrmann/isec-ueb4
``` 


---

Benutzt statt `gets` eine geeignetere Bibliotheksfunktion, und
überzeugt Euch, dass das Programm sich sinnvoller verhält.
<br />
Lösung: `char *fgets(char *s, int size, FILE *stream)`

1. Parameter: Zeiger auf das Char-Array, welches die Zeichenkette speichert.
2. Parameter: Maximale Anzahl an Chars (inklusive Null-Terminierung); verhindert Buffer-Overflow.
3. Parameter: Zeiger auf das FILE-Objekt, aus welchem gelesen wird.


Im folgendem haben wir die Funktion `gets(input)` durch `fgets(input, sizeof(input), stdin)` ersetzt.

``` 
#include <stdio.h>

void foo(int attempt) {
    int number = attempt + 1;
    char input[8];

    printf("Type a string: ");
    fgets(input, sizeof(input), stdin);
    printf("Your input number %d was '%s'.\n", number, input);
}

int main() {
  int i;
  for (i = 0; i < 7; ++i) foo(i);
  return 0;
}

```

Ausführung: gcc version 12.0.0 ohne option
`gcc -o fstandard buffer.c`
 
- Eingaben der Länge < 7 geben eine fast erwartete Ausgabe. Am Ende der Eingabe wird ein Zeilenumbruch `\n` angehängt. (Wir haben keine Ahnung, warum hinter jeder Eingabe nun ein `\n` eingefügt wird.)
```
Your input number 1 was '1
'.
Your input number 1 was '123456
'.
```

- Bei einer länge von > 7 wird die Eingabe auf die Länge 7 begrenzt und weitere Zeichen werden in der nächsten Schleifen an das Progam übergeben. Der Zähler wird aber dennoch wie erwartet erhöht. 
```
Type a string: 1234567
Your input number 2 was '1234567'.
Type a string: Your input number 3 was '
'.
Type a string: 12345678
Your input number 4 was '1234567'.
Type a string: Your input number 5 was '8
'.

Type a string: 12345671234567123
Your input number 1 was '1234567'.
Type a string: Your input number 2 was '1234567'.
Type a string: Your input number 3 was '123
'.
```

- Das Program terminiert wie erwartet und stürtzt nicht mehr ab. Das Kompilieren mit `gcc -o fstandard buffer.c -fno-stack-protector` hat keine Unterschiede gezeigt.
- Mit der Verwendung von `fgets()` findet kein Buffer-Overflow mehr statt.



Quellen: 
--
https://stackoverflow.com/questions/44469372/exploiting-buffer-overflow-using-gets-in-a-simple-c-program
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
