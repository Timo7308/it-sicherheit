Informationssicherheit, 5. Übung
================================

* * * * *

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Untersucht mit `nmap` oder einem vergleichbaren Tool die Rechner der
Universität mit den IPv4-Adressen 134.102.50.15 und 134.102.201.110
darauf, welche Netzdienste angeboten werden.
Führt diese
Untersuchung im Bearbeitungszeitraum **von netztechnisch verschiedenen
Standorten** (z.B. daheim, von einem Rechner der E0) aus.
Gebt jeweils an, wann (Uhrzeit!), von wo (topologisch, d.h., welchen
Weg nehmen Eure Pakete), wie (u.a. mit welchen Parametern) und
welche Auswirkungen das jeweils auf das Ergebnis hatte.

Nutzt bei `nmap`, sofern es Euch sinnvoll erscheint, die Optionen
`-sV`, `-O` und `-p`. Wie arbeiten diese intern ungefähr? Welche
zusätzlichen Erkenntnisse gewinnt Ihr, wenn Ihr `-p 5000-8000` angebt?

Fasst Eure Beobachtungen zusammen und nennt
ggf. Auffälligkeiten. Wichtig ist uns weniger eine vollständige (und
erstmal nichtssagende) Auflistung aller Dienste, sondern vielmehr, dass Ihr
Euch darin übt, die betrachteten Hosts einzuschätzen: Welche primäre
Funktion könnten sie haben (Webserver, Arbeitsplatz, Drucker,
Smartphone, ...) und welche Dienste "passen nicht dazu" bzw. sind
potentiell überflüssig (oder ein mögliches Einfallstor)?

Könnt Ihr dabei Dienste identifizieren, die eher nur innerhalb der
Universität angeboten werden sollten? Gibt es Dienste, die überhaupt
nicht im Netz zu sehen sein sollten? Welche grundsätzlichen
(Sicherheits-)Überlegungen führten Euch zu diesen Einschätzungen?

Achtung: Ihr scannt zentrale Elemente der IT-Infrastruktur dieser
Universität. Scannen ist okay. Aber *keine* Angriffe. Falls Ihr
meint, ein klaffendes Loch gefunden zu haben, dann meldet Euch
gern noch vor der Abgabe bei uns, probiert es aber nicht "um sicher zu
gehen" vorher aus.

* * * * *

Abgabe
------

bis 2021-11-25 23:59 UTC, digital in Stud.IP als Markdown-Datei mit dem
Dateinamen `isec21_ueb05_grpYY.(md|zip|tgz)` (das `YY` mit eurer Gruppennummer ersetzen).
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
