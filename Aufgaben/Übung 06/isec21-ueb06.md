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

Probiert dieses Programm zunächst ohne weitere Benutzung von Analysewerkzeugen
aus; benutzt dabei auch verschiedene Eingabelängen und Zeichen (z.B. auch mal
100 Zeichen und verschiedene Anfangszeichen).

Was hat der *clang analyzer* dazu zu sagen?  (Aufruf mit einer
modernen llvm/clang-Installation, z.B. auf den x-Rechnern
in der Ebene 0: `scan-build -V ` *...compiler-aufruf...*)  Stimmt Ihr mit der
Analyse überein, oder seht Ihr ein *false positive*?

Kompiliert dann das Programm mit dem *Address Sanitizer* (gcc auf
x-Rechnern, clang auf m-Rechnern), und probiert das Ergebnis wieder
mit verschiedenen Eingabelängen.  Was sagt uns das Ergebnis?

Welche Probleme findet der einfache manuelle Test?
Welche die statische Analyse, welche die Laufzeit-Überprüfung?
Welche Unterschiede gibt es daher in der Erkennungsfähigkeit?


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
