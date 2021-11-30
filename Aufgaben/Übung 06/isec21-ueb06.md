Informationssicherheit, 6. Übung
================================

*******************

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Das folgende Programm ist ziemlich kaputt:

~~~
#include <stdio.h>
#include <stdlib.h>

int get_first_char(char *p) {
  int c = p[0];
  if(c<50){
    free(p);
  }
  return c;
}

int main() {
  char *buf = malloc(32);
  fgets(buf, 64, stdin);
  char c = get_first_char(buf);
  if(c != '0'){
    printf("%d %d\n", c, buf[0]);
  }
  free(buf);
}
~~~

(Die Probleme sind bei diesem kurzen Programm recht offensichtlich,
aber ein langes Programm wäre für diese Übungsaufgabe zu aufwendig.)

----

Probiert dieses Programm zunächst ohne weitere Benutzung von Analysewerkzeugen
aus; benutzt dabei auch verschiedene Eingabelängen und Zeichen (z.B. auch mal
100 Zeichen und verschiedene Anfangszeichen).

Mit `gcc (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0` ohne Optionen

```
$ ./a.out
a
97 97

$ ./a.out
!
33 0
free(): double free detected in tcache 2
Aborted

$ ./a.out
1
49 0
free(): double free detected in tcache 2
Aborted

$ ./a.out
0
free(): double free detected in tcache 2
Aborted
```
- Bei einer Eingabe von a ist die Ausgabe 97 97, bei einer Eingabe von b 98 98 und bei der Eingabe von z ist die Ausgabe 122 122. Mit dem Fortschreiten im Alphabet wird die Ausgabe um 1 erhöht. Bei der Eingabe eines großen A ist die Ausgabe 65 65. Bei der Eingabe von Z ist die Ausgabe 90 90. Auch hier wird die Ausgabe jeweils um 1 erhöht. Die Länge und die Anordnung der Zeichenkette ändert an diesen Ausgaben nichts. Entscheidend für die Ausgabe ist der erste Buchstabe in der Zeichenkette. 
Bei der Eingabe von 1 erscheint die oben genannte Fehlermeldung und die Ausgabe 49 0. Bei der Eingabe von 2 ist die Ausgabe 50 50. Bei der Eingabe von 9 ist die Ausgabe 57 57. Auch bei der Eingabe von Zahlen ist die Länge der Zahl nicht von Bedeutung. Entscheidend ist die erste Zahl. Ist die Zahl 1, wird eine Fehlermeldung ausgegeben. Ist die erste Zahl 0, gibt es keine Ausgabe. 


- mit der Eingabe `0` gibt es keine Ausgabe (siehe Zeile 16)

- Nach der ASCII value Tabelle führt eine Eingabe wie `!` dazu, dass 
in Zeile 6 `if(c<50){` zu `true` auswertet. Somit wird der Speicher zwei
mal wieder freigegeben. (in Zeile 7 und in Zeile 19)

- auch mal 100 Zeichen. Gab bei mir keine Auffälligkeiten.

---

Was hat der *clang analyzer* dazu zu sagen?  (Aufruf mit einer
modernen llvm/clang-Installation, z.B. auf den x-Rechnern
in der Ebene 0: `scan-build -V ` *...compiler-aufruf...*)

```
$ scan-build -V gcc prog.c
scan-build: Using '/usr/lib/llvm-10/bin/clang' for static analysis
prog.c:17:29: warning: Use of memory after it is freed
                            printf("%d %d\n", c, buf[0]);
                                                 ^~~~~~
prog.c:19:5: warning: Attempt to free released memory
                  free(buf);
                  ^~~~~~~~~
2 warnings generated.
scan-build: 2 bugs found.
...

```

  Stimmt Ihr mit der
Analyse überein, oder seht Ihr ein *false positive*?

- Die warning: `Use of memory after it is freed` konnte ich nicht nachstellen. (vlt mit langen Eingaben??
 oder dies ist der false positive)

---

Kompiliert dann das Programm mit dem *Address Sanitizer* (gcc auf
x-Rechnern, clang auf m-Rechnern), und probiert das Ergebnis wieder
mit verschiedenen Eingabelängen.  

Was sagt uns das Ergebnis?

- Ausführung auf dem Rechner x01 mit gcc
- Eingabe: !
- Fehler: ```heap-use-after-free``` 

```
SUMMARY: AddressSanitizer: heap-use-after-free (/home/timo5/isec-ueb6/runme+0xba3) in main
Shadow bytes around the buggy address:
  0x0c067fff7fb0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c067fff7fc0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c067fff7fd0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c067fff7fe0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c067fff7ff0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c067fff8000: fa fa[fd]fd fd fd fa fa fa fa fa fa fa fa fa fa
  0x0c067fff8010: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff8020: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff8030: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff8040: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff8050: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
==1509==ABORTING









```




Welche Probleme findet der einfache manuelle Test?

-

Welche die statische Analyse, welche die Laufzeit-Überprüfung?

-

Welche Unterschiede gibt es daher in der Erkennungsfähigkeit?

-

* * *

Abgabe
------

bis 2021-12-02 23:59 UTC, digital in Stud.IP als Markdown-Datei mit dem
Dateinamen `isec21_ueb06_grpYY.(md|zip|tgz)` (das `YY` mit eurer Gruppennummer ersetzen).
Dabei bitte in der Datei die Nummer Eurer Gruppe in Stud.IP sowie alle
an der Abgabe beteiligten Gruppenmitglieder nennen.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen aus dem Netz bedient (Anleitungen,
Howtos, etc), gebt diese bitte als URI mit an.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
