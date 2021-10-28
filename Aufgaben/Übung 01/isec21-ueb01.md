Informationssicherheit, 1. Übung
================================

von _G35 Philias Borrmann, Adrian Lindloff, Timo Schuchmann_

* * * * *

Aufgabe 1, 6 Punkte, Gruppe
---------------------------

Das Studierendenwerk gibt für das bargeldlose Bezahlen in der Mensa
und den Cafeterien die *Mensacard* aus
([www.stw-bremen.de/de/mensa/mensacard](https://www.stw-bremen.de/de/mensa/mensacard)). Die Karte wird an
Studierende gegen Vorlage des Studierendenausweises und Zahlung eines Pfands
ausgegeben und hat dann eine Gültigkeitsdauer von einem Jahr. Für
das Aufladen der Karte gibt es auf dem Universitätsgelände mehrere
Automaten, unter anderem in der Mensa. Die Bezahlung der Aufladung ist
mit Bargeld oder EC-Karte möglich.
Auch für Mitarbeitende (gegen Vorlage des Mitarbeitendenausweises)
gibt es Mensacards, die sich auf interessante Weise von den
Studi-Karten unterscheiden (wie?).

Schaut Euch die vorgenannte Website an und betrachtet, wenn es Euch
möglich ist, die Anlage vor Ort: die Mensacard-Ausgabe, die
Auflade-Automaten.

Wendet dabei die in der Vorlesung verwendeten Begriffe an.
Beschreibt auch die Vor- und Nachteile gegenüber einer Bezahlung mit
PBargeld an den Kassen der Essensausgabe.

Wir gehen von zumindest einer Seite Text aus. Lieber in die Breite
(welche Möglichkeiten gibt es für wen) als in die Tiefe (wie führe
ich einen bestimmten Angriff am effektivsten aus) denken.


* * * * *

Lösung Aufgabe 1
-------

Die Mensacard ist eine Alternative zum Bargeld, welche gegen einen Pfand sowohl Studierenden, als auch Mitarbeitern zur Verfügung gestellt wird. Der Unterschied liegt hierbei, dass bei der Studentenkarte die Matrikelnummer verwendet wird und dadurch die Daten nicht mehr vollständig anonymisiert vorliegen. Auf sie lässt sich an verschiedenen Orten ein Guthaben aufladen, welches dann zum Bezahlen verwendet wird. Die Karte enthält nur die Matrikelnummer bzw. die persönliche Kennnummer und das aktuelle Guthaben der auf sie angemeldeten Person.

Sie ermöglicht einen gegenüber dem Bargeld effektiveren Zahlungsvorgang. In der Theorie sorgt die für einen individuell schnelleres Bezahlen und somit insgesamt für kürzere Wartezeiten. Damit dieses Konzept jedoch wirklich funktioniert, muss es genug Auflademöglichkeiten geben, da sich ansonsten dort lange Wartezeiten ergeben. 



**Wer könnte der/die Angreifende sein?**

Durch die geringe Informationsdichte sind bereits einige Sicherheitsrisiken ausgeschlossen. 
Einem Hacker/Cracker wäre es möglich das Guthaben auf dem Chipsatz der Karte ändern.
Weiterhin möglich ist ein klassischer Raubüberfall auf eine der Auflademöglichkeiten, denn dort befindet sich viel zum Kartenguthaben konvertiertes Bargeld und das Verlorengehen bzw. Beklauen der Karte. Bei letzterem kann eine weitere Person das Guthaben im Namen des Besitzers ausgeben. Da die Aufladung jedoch immer manuell erfolgt, könnte diese zweite Person, wie beim Bargeld, nur das vorhandene Guthaben kostenfrei verwenden. 
An dieser Stelle bietet die Mensacard einen weiteren Vorteil, welcher in der unkomplizierten Neuausstellung einer Karte liegt, falls diese abhanden kommt. Gegen eine Kaution kann die verlorene Karte gesperrt werden und das Guthaben der alten auf diese neue Karte übertragen werden. Somit lässt sich im Gegensatz zum Bargeld auch Verlorenes wiederverwenden.



**Welche Funktionen hat die Mensacard aus Sicht der
(Geschäfts-)Abläufe, die verteidigt werden müssen?**


Dazu zählt die Lehre, denn lange Wartezeiten innerhalb der Mensa können eine kettenartige Auswirkungen auf diese haben und dort zu Verspätungen führen. Wenn weitere Funktionalitäten (bspw. die Bedienung von Waschmaschinen) der Mensacard wegfallen, würde dies zu viel Ärger bei Studierenden/ Mitarbeiter*innen führen und es müsste eventuell Zeit und Geld für eine Techniker*in aufgewendet werden. 


**Welche anderen Abläufe (außerhalb der Mensa) könnten durch das
hantieren mit der Mensacard betroffen sein?**


Damit die Mensacard ihren Zweck erfüllt, müssen alle Funktionalitäten (für Drucker, Snackautomaten, Waschmaschinen) einwandfrei von den Kunden verwendet werden können, damit ein reibungsloser Ablauf gewährleistet wird. Ansonsten können auch Abläufe jenseits der Mensa betroffen sein. 


**Welche Gegenstände bzw. Abläufe müssen
geschützt werden, welche der in der Vorlesung vorgestellten Sicherheitsziele sind
betroffen: wo geht es um Integrität, wo um Verfügbarkeit usw.?**


Vertraulichkeit: Die personenbezogenen Daten und das Guthaben auf der Karte müssen geschützt werden. Der Zugriff muss geschützt werden, damit kein anderer die Karte nutzen kann. 
Integrität: Die Daten auf der Mensacard müssen vor Veränderungen geschützt sein. 
Verfügbarkeit: Alle zur Mensacard gehörenden Dienste sollten einwandfrei funktionieren. 
Der Ablauf des Bezahlens muss gewährleistet werden (ansonsten ist die Mensacard unnötig bzw. Geldverschwendung).
Zurechenbarkeit/Verbindlichkeit: Dies ist nur beim Ausstellen der Karte gewährleistet, da hier die Personalien abgeglichen werden. Beim Zahlen mit einer geklauten Karte erfolgt keine Autorisierung mit dem Eigentümer der Karte.

**Was haltet Ihr allgemein von der Vorgehensweise?**

Wir finden diese Vorgehensweise ziemlich praktisch, da das Bezahlen aus eigener Erfahrung durchschnittlich deutlich schneller funktioniert und sich Schlangen möglichst „klein” halten (zumindest im Vergleich zum Bezahlen mit Bargeld). Die Mensacard ist im Vergleich zum Bargeld ausreichend geschützt, da es die Möglichkeit gibt, sein Guthaben nach einem Verlust der Karte wiederzuerlangen und keine sensiblen Informationen gespeichert werden. Des Weiteren muss sich an Snackautomaten oder Druckern kein Behälter für Kleingeld befinden, was ebenfalls praktisch ist und das Risiko von einem  Diebstahl verringert.


**Was würdet Ihr als Betreiber anders machen?**

Eine Möglichkeit wäre, die Mensacard zu digitalisieren und auf dem Smartphone zugänglich zu machen. Die birgt allerdings viele neue potenzielle Risiken und Herausforderungen, weswegen die Wirtschaftlichkeit überprüft werden muss. Eine Online-Aufladung der Mensacard kann ebenfalls sinnvoll sein und (verbunden mit der ersten Möglichkeit) Aufladeautomaten entlasten oder sogar überflüssig machen. Um den Fremdzugriff weiter einzuschränken, könnte (optional ab einer gewissen Summe) z.B. die Eingabe einer Pin verlangt werden. Dadurch müssten jedoch weitere Daten auf der Karte gespeichert werden und die Wartezeiten könnten sich verlängern.



* * * * *

Aufgabe 2, 0 Punkte, Einzeln
----------------------------

**Jeder** Teilnehmer trägt sich in das
[Stud.IP-System](https://elearning.uni-bremen.de/) ein. Macht Euch mit
dem Stud.IP-System und seinen verschiedenen Funktionen vertraut.

Sorgt dafür, dass Eure Arbeitsgruppe in Stud.IP als solche eingetragen
ist.

(Für diese Aufgabe gibt's zwar keine Punkte, aber ohne sie ist das
Übungsblatt nicht bearbeitet.)

* * * * *

Lösung Aufgabe 2
-------
Wir sind in Gruppe "**G35**".

Philias Borrmann borrmann@uni-bremen.de


Adrian Lindloff lindloff@uni-bremen.de

Timo Schuchmann timo5@uni-bremen.de


* * * * *

Abgabe
------

bis 2021-10-28 23:59 UTC, digital in Stud.IP als Markdown-Datei mit dem
Dateinamen `isec21_ueb01_grpYY.(md|zip|tgz)` (Das `YY` mit eurer Gruppennummer ersetzen).
Dabei bitte in der Datei alle Gruppenmitglieder namentlich nennen. Ebenso
die Nummer Eurer Gruppe in Stud.IP.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten nachvollziehbar sein.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22


<!--  LocalWords:  Mensacard
 -->

