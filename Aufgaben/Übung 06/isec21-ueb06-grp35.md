Informationssicherheit, 6. Übung
================================

von Gruppe **G35**
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

*******************

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Das folgende Programm ist ziemlich kaputt:

~~~
1 #include <stdio.h>
2 #include <stdlib.h>
3
4 int get_first_char(char *p) {
5   int c = p[0];
6   if(c<50){
7     free(p);
8   }
9   return c;
10 }
11 
12 int main() {
13   char *buf = malloc(32);
14   fgets(buf, 64, stdin);
15   char c = get_first_char(buf);
16   if(c != '0'){
17     printf("%d %d\n", c, buf[0]);
18   }
19   free(buf);
20 }
~~~

----

**Ausführung mit `gcc (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0` ohne Optionen**

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

$ ./a.out
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
97 97
```
- Bei einer Eingabe von `a` ist die Ausgabe `97 97`, bei einer Eingabe von`b` `98 98` und bei der Eingabe von`z` ist die Ausgabe `122 122`. Mit dem Fortschreiten im Alphabet wird die Ausgabe um 1 erhöht. Bei der Eingabe eines großen`A`ist die Ausgabe `65 65`. Bei der Eingabe von `Z` ist die Ausgabe `90 90`. Auch hier wird die Ausgabe jeweils um 1 erhöht (siehe ASCII-Tabelle). Die Länge und die Anordnung der Zeichenkette ändert an diesen Ausgaben nichts. Entscheidend für die Ausgabe ist der erste Buchstabe in der Zeichenkette. 
Bei der Eingabe von `1` erscheint die oben genannte Fehlermeldung und die Ausgabe `49 0`. Bei der Eingabe von `2` ist die Ausgabe `50 50`. Bei der Eingabe von `9` ist die Ausgabe `57 57`. Auch bei der Eingabe von Zahlen ist die Länge der Zahl nicht von Bedeutung. Entscheidend ist die erste Zahl. Ist die Zahl 1, wird eine Fehlermeldung ausgegeben. Ist die erste Zahl 0, gibt es keine Ausgabe. 


- Mit der Eingabe `0` gibt es keine Ausgabe. In Zeile 16 wird der print-Befehl übersprungen.

- Nach den Werten der ASCII-Tabelle führt eine Eingabe wie `!` dazu, dass 
in Zeile 6 `if(c<50){` zu `true` auswertet und daraufhin in Zeile 7 der Speicher von dem char-Pointer freigegeben wird. Der Print-Aufruf in Zeile 17 kann nur die erste Zahl(`%d`) mit der Variable `c` ausgeben. In dem Fall mit `!` als Eingabe ist dies die Zahl `33`. Die zweite Zahl, auf die über `buf[0]` zugegriffen wird, wird jedoch als eine `0` ausgegeben, da hier ein Speicherzugriff passiert, nachdem dieser Speicher freigegeben wurde.
Nach dem Ausführen des `printf` wird in Zeile 19 nun erneut der Speicher von dem Char-Pointer freigegeben, weswegen wir auch folgende Fehlermeldung erhalten: `free(): double free detected in tcache 2`

- Bei einer Eingabe mit einer langen Zeichenkette gab es keine Auffälligkeiten.

---

**Aufruf mit dem clang-analyzer**
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

 

- Mit den beiden genannten `warnings` der Analyse stimmen wir überein. Die beiden Fälle haben wir oben schon beschrieben.

- Die warning: `Use of memory after it is freed` konnte nicht direkt nachgestellt werden. Diese Fehlermeldung ist dennoch bei der Ausgabe zu erkennen. Es wird in diesem Fall immer eine `0` ausgegeben.
Siehe folgende Eingabe: 
```
$ ./a.out
!
33 0
free(): double free detected in tcache 2
Aborted
```

- Uns ist noch zusätzlich aufgefallen, dass keine Warnung erstellt wurde, die im Zusammenhang mit `malloc(32)` und `fgets(buf, 64, stdin)` steht. 

---

**Aufruf mit dem Adress Sanitizer (Ausführung auf dem Rechner x01 mit gcc)**  


`gcc -fsanitize=address prog.c`


Eingabe: ! (c<50 nach ASCII-Tabelle)

Fehler: ```heap-use-after-free``` 

```
$ ./progSan
!
=================================================================
==303==ERROR: AddressSanitizer: heap-use-after-free on address 0x603000000010 at pc 0x0000004c3258 bp 0x7ffc297f0230 sp 0x7ffc297f0228
READ of size 1 at 0x603000000010 thread T0
    #0 0x4c3257 in main (/home/phibo/isec/ueb6/progSan+0x4c3257)
    #1 0x7f200bda90b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16
    #2 0x41b2dd in _start (/home/phibo/isec/ueb6/progSan+0x41b2dd)

0x603000000010 is located 0 bytes inside of 32-byte region [0x603000000010,0x603000000030)
freed by thread T0 here:
    #0 0x49379d in free (/home/phibo/isec/ueb6/progSan+0x49379d)
    #1 0x4c3177 in get_first_char (/home/phibo/isec/ueb6/progSan+0x4c3177)
    #2 0x4c3201 in main (/home/phibo/isec/ueb6/progSan+0x4c3201)
    #3 0x7f200bda90b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16

previously allocated by thread T0 here:
    #0 0x493a1d in malloc (/home/phibo/isec/ueb6/progSan+0x493a1d)
    #1 0x4c31a8 in main (/home/phibo/isec/ueb6/progSan+0x4c31a8)
    #2 0x7f200bda90b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16

SUMMARY: AddressSanitizer: heap-use-after-free (/home/phibo/isec/ueb6/progSan+0x4c3257) in main
...
==1509==ABORTING

```

- Es wird versucht ein Speicherbereich der Größe von 1 Byte von `0x603000000010` zu lesen. Der Speicherbereich, in dem diese Zelle erhalten ist, wurde aber schon freigegeben.
- Es wird zusätzlich angeben, wann der Speicher zugewiesen, freigegeben und zugegriffen wurde.

---


Eingabe: 0

Fehler: ```double-free```  

```
$ ./progSan
0
=================================================================
==305==ERROR: AddressSanitizer: attempting double-free on 0x603000000010 in thread T0:
    #0 0x49379d in free (/home/phibo/isec/ueb6/progSan+0x49379d)
    #1 0x4c327b in main (/home/phibo/isec/ueb6/progSan+0x4c327b)
    #2 0x7f1a1696d0b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16
    #3 0x41b2dd in _start (/home/phibo/isec/ueb6/progSan+0x41b2dd)

0x603000000010 is located 0 bytes inside of 32-byte region [0x603000000010,0x603000000030)
freed by thread T0 here:
    #0 0x49379d in free (/home/phibo/isec/ueb6/progSan+0x49379d)
    #1 0x4c3177 in get_first_char (/home/phibo/isec/ueb6/progSan+0x4c3177)
    #2 0x4c3201 in main (/home/phibo/isec/ueb6/progSan+0x4c3201)
    #3 0x7f1a1696d0b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16

previously allocated by thread T0 here:
    #0 0x493a1d in malloc (/home/phibo/isec/ueb6/progSan+0x493a1d)
    #1 0x4c31a8 in main (/home/phibo/isec/ueb6/progSan+0x4c31a8)
    #2 0x7f1a1696d0b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16

SUMMARY: AddressSanitizer: double-free (/home/phibo/isec/ueb6/progSan+0x49379d) in free
==305==ABORTING
```

- Es wird versucht ein Speicherbereich freizugeben, der vorher schon freigegeben wurde.

---

Eingabe: 31 mal a (oder Länger)

Fehler: ```heap-buffer-overflow``` 

``` 
$ ./progSan
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
=================================================================
==307==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x603000000030 at pc 0x000000434d74 bp 0x7fff9fd20960 sp 0x7fff9fd20128
WRITE of size 42 at 0x603000000030 thread T0
    #0 0x434d73 in fgets (/home/phibo/isec/ueb6/progSan+0x434d73)
    #1 0x4c31f4 in main (/home/phibo/isec/ueb6/progSan+0x4c31f4)
    #2 0x7f1b85a230b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16
    #3 0x41b2dd in _start (/home/phibo/isec/ueb6/progSan+0x41b2dd)

0x603000000030 is located 0 bytes to the right of 32-byte region [0x603000000010,0x603000000030)
allocated by thread T0 here:
    #0 0x493a1d in malloc (/home/phibo/isec/ueb6/progSan+0x493a1d)
    #1 0x4c31a8 in main (/home/phibo/isec/ueb6/progSan+0x4c31a8)
    #2 0x7f1b85a230b2 in __libc_start_main /build/glibc-eX1tMB/glibc-2.31/csu/../csu/libc-start.c:308:16

SUMMARY: AddressSanitizer: heap-buffer-overflow (/home/phibo/isec/ueb6/progSan+0x434d73) in fgets
...
==2299==ABORTING

```  
- Ab einer Eingabelänge von 31 wird das Programm nicht mehr fehlerfrei ausgeführt. Befinden sich am Anfang der Eingabe ```0 ,1 oder !``` kommt es schon vorher zu den beiden oben beschriebenen Fehlermeldungen. 

- Es wird auf eine Speicheradresse zugegriffen, welche nicht zugewiesen wurde. Über `malloc` wurden nur diese 32 Bytes zugewiesen `[0x603000000010,0x603000000030)`, aber durch `fgets` sollen 42 Bytes geschrieben werden. Da aber `fgets` als Parameter mitgegben wird, dass 64 Bytes geschrieben werden können, wird versucht auf nicht zugewiesenen Speicher zu schreiben `0x603000000030`.

---


Welche Probleme findet der einfache manuelle Test?


- Der einfach manuelle Test findet, wie oben beschrieben, den Fehler `double-free`. Dieser Fehler wird auch ausgegben und fällt dadurch als erstes auf: `free(): double free detected in tcache 2`

- Auch der Fehler `use-after-free` kann erkannt werden, wird aber nicht von der Konsole als Fehler ausgegeben. Dieser Fehler ist nur zu erkennen, wenn man den Sourcecode liest und diesen mit der Ausgabe vergleicht. Bei einer Eingabe von `!` bekommen wir folgende Ausgabe `33 0`. Hier ist die ausgegbene `0` ein Indiz dafür, dass es sich hierbei um den Fehler `use-after-free` handeln kann.

---
Welche die statische Analyse, welche die Laufzeit-Überprüfung?

- Die statische Analyse des *clang analyizer*  erkennt auch die beiden Fehler `double-free` und `use-after-free`. Es wird zusätzlich angeben, in welcher Zeile des Sourcecodes diese Fehler hervorgerufen werden. Eine Detailansicht wird als HTML-Datei im temp-Verzeichnis erstellt, die das Hervorrufen des Fehlers in einzelnen Schritten beschreibt.

- Die Laufzeit-Überprüfung erkennt auch die Fehler `double-free` und `use-after-free` und zusätlich einen `heap-buffer-overflow` Fehler. Der Fehler `use-after-free` wird hier als `heap-use-after-free` ausgegeben. Auch hier wird in der Ausgabe ersichtlich, wie dieser Fehler zustande kommt, auch wenn dies nicht so schön dargestellt wird, wie beim HTML-Dokument vom *clang analyzer*.

---
Welche Unterschiede gibt es daher in der Erkennungsfähigkeit?

- Die statische Analyse mit dem *clang analyzer* ist ein gutes Tool, um überhaupt herauszufinden, ob es Fehler im Code gibt. Bei diesem Tool ist keine Eingabe notwendig, die ein Fehler verursachen könnte. So kann man sich im nachhinein eine Eingabe überlegen, welche diesen Fehler hervorrufen könnte. Es kann sich dabei aber auch um ein *false positive* handeln, wobei dieser Fehler gar nicht reproduzierbar ist. 
Die Laufzeit-Überprüfung und auch die manellen Tests erfordern eine Eingabe, welche einen Fehler verursachen. Dabei ist die Laufzeit-Überprüfung das eindeutig bessere Tool, da hier genau beschrieben wird, wie es zu diesem Fehler kommt und es wird z.B. der `heap-buffer-overflow` bei einer langen Eingabe erkannt.


Quellen:
--

https://www.cs.cmu.edu/~pattis/15-1XX/common/handouts/ascii.html
