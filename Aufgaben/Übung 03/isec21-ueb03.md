Informationssicherheit, 3. Übung
================================
Wir sind in Gruppe "**G35**". <br />
Philias Borrmann borrmann@uni-bremen.de <br />
Adrian Lindloff lindloff@uni-bremen.de <br />
Timo Schuchmann timo5@uni-bremen.de <br />

* * * * *

Aufgabe 1, 5 Punkte, Gruppe
-----------------------------------

* * * * *
Nennt mindestens drei Rollen, die bezüglich des Zugriffs auf die
Krankenakte zu unterscheiden sind.
-------------



- Ärzte 
- Medizinisches Personal 
- Verwaltungsmitarbeiter <br />
<br />

 - _Admin(alle Rechte: hätte zu viele Rechte und könnte ggf. Patienten löschen. Könnte auf Anfrage des Patienten seine Akte löschen)_ 


* * * * *

Welche Aktionen können auf der Krankenakte ausgeführt werden,
d.h. welche Berechtigungen sind zu vergeben?
-----------


Berechtigungen auf unterschiedlichen Ebenen (höhere Berechtigungen haben alle tieferen Berechtigungen):

- Medikamente zur Behandlung hinzufügen oder entfernen
- Diagnosen stellen oder ändern 
- Therapien verordnen (hinzufügen) <br />
<br />

- Patientendaten aufnehmen oder ändern (Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse, Blutgruppe)
- Bisherige Befunde und Therapien bearbeiten oder hinzufügen
- Allergien und Unverträglichkeiten einsehen/ bearbeiten oder hinzufügen
- Zusätzliche Dokumentation und Verwaltungshistorie <br />
<br />

- Patientendaten aufnehmen oder ändern (Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse)
- Bisherige Befunde und Therapien einsehen
- Medikamente zur Behandlung einsehen
- Abrechnungen erstellen (Sonderfall: nur für diese Rolle) <br />
<br />

- Patientendaten anzeigen (Eindeutige Kennung, Name, Geburtsdatum, Station, Zimmer) <br />

Ausnahmen: Die eindeutige Kennnummer wird einmalig erstellt (bspw. automatisch oder durch einen Admin) und danach nicht mehr verändert.





* * * * *

Erstellt eine geeignete Relation entsprechend des RBAC-Modells,
die die von Euch genannten Rollen mit den Aktionen verknüpft. Wo
kann hier vielleicht Vererbung helfen?
-------------



Rolle: lesen(l), schreiben(s) 

| Rollen/Rechte                                 | Ärzte  | Medizinisches Personal | Verwaltungsmitarbeiter |
| --------                                      | ------ | ------                 |------                  |
|eindeutige Kennung (id)                        | l      | l                      | l                      |
|Patientendaten (name, Krankenkasse, ...)       | l,s    | l,s                    | l(begrenzt)            |
|Allergien und Unverträglichkeiten              | l,s    | l,s                    | -                      |
|bisherige Befunde                              | l,s    | l,s                    | l                      |
|verordnete Therapien                           | l,s    | l                      | l                      |
|verschriebene Medikamente                      | l,s    | l                      | l                      |
|Diagnosen                                      | l,s    | l                      | l                      |
|Abrechnungen                                   | -      | -                      | l,s                    |
|Dokumentation                                  | l,s    | l,s                    | -                      |
|Verwaltungs -und Änderungshistorie             | l      | l                      | -                      |


_Eine Änderung der eindeutigen Kennung sei nicht möglich, um Fehler in der Datenbank zu vermeiden._

Da die Anzahl der Rechte mit jeder Rolle steigen und (bis auf Ausnahmen) keine weggnommen werden, können diese Rollen in der gelisteten Reihenfolge vererbt werden. Wenn wir die Rolle des Arztes in einzelnen Fachbereiche unterteilen, könnte die Rolle des Aztes an diese vererbt werden.

**Verwaltungsmitarbeiter:** 
Der Verwaltungsmitarbeiter hat nur lesenden Zugriff auf die Aktionen, die für die Abrechnungen wichtig sind. Wenn es möglich ist die Abrechnungen direkt am Terminal durchzuführen, dann steht diese Funktionalität nur den Verwaltungsmitarbeitern zu (geht aus der Aufgabenstellung nicht klar hervor).
Die Kennung und Patientendaten sind erforderlich um eine Rechnung an die Krankenkasse des Patienten zu stellen. Die verbundenen Kosten sind hierzu in der Therapie, Medikamenten und Diagnose zu finden. Nach unserer Meinung ist hierzu ein Zugriff auf Alergien und Befunde oder die Blutgruppe nicht erforderlich.


**Medizinisches Personal:**
Das medizinische Personal hat lesenden Zugriff auf alle Daten und kann zudem die Daten eines Patienten aufnehmen/aufschreiben. Zusätzlich können sie Vorgänge oder weitere wichtige Informationen dokumentieren und auf die automatisch generierte Verwaltungs -und Änderungshistorie zugreifen, um zusehen, wer für welche Änderungen verantwortlich ist und dort gegebenenfalls nachfragen zu können.

**Arzt:**
Der Arzt hat die selben Rechte, wie das medizinischen Personal und kann zusätzlich Therapien verodnen, Medikamente verschreiben und Diagnosen erstellen. 





* * * * *

Ihr übernehmt Eure Berechtigungen in die Praxis. Mit welchen
menschlichen und organisatorischen Problemen rechnet Ihr?
-------------


Es könnte zu Missverständnissen bei der Kommunikation zwischen Ärzten und medizinischem Personal kommen. Vor allem zur Einführung der Terminals sind alle involvierten Mitarbeiter noch nicht vertraut mit dem System der digitalen Krankenakte und machen möglicherweise Fehler. Was würde passieren, wenn das System der digitalen Krankenakten nicht funktioniert? Gibt es im Falle von Ausfällen oder systemgefährdeten Fehlfunktionen eine spontane Alternative? <br />
<br /> Ein weiteres Problem ist die Digitalisierung der analogen Patientenakten. Bisherige Therapien oder Diagnosen müssten nach den aktuellen Berechtigungen unseres RBAC-Modells von einem Arzt eingetragen werden. Jedoch haben Ärzte wichtigere Aufgaben zu erledigen, als alte schriftliche Daten zu digitalisieren. Wenn die Akten von anderen Mitarbeitern in das neue System übernommen werden ist die Vertraulichkeit der Patientendaten gefährdet.<br />
<br />
Hinzu kommt das Problem der Konfliktklassen der Ärzte und deren Patienten. Inwiefern kann ein Arzt die Diagnose oder verschriebenen Medikamente eines Patienten beeinflussen,
für welchen er gar nicht zuständig ist. Dies betrifft zwei Ebenen. Einerseits könnten Fehler entstehen, wenn ein neuer Arzt einen Patienten behandelt und anhand der vorhandenen Eintragungen fehlgeleitet wird. Andererseits beziehen sich die Konfliktklassen auch auf die Vertraulichkeit der Patienten. Soll jeder Arzt auf die privaten Daten eines jeden Patienten zugreifen können? Die persönliche Informationen könnten an einen zu großen Adressatenkreis gelangen. Dem gegenüber steht die Behandlung im Falle eines Arztwechsels, denn dann muss der neue Arzt auf jene Informationen zugreifen können, um die bestmögliche Behandlung gewährleisten zu können. 

So eine Konfliktklasse könnte auch vorkommen, wenn ein Arzt selbst Patient in dem Krankenhaus wird. Hierbei könnte der Arzt sich selbst Medikamente verschreiben, für welche er als Patient normalerweise kein Zugriff hat.<br />
<br />

Inwiefern kann ein Arzt aus einer gewissen Distanz auf die Krankenakte zugreifen? Falls der Arzt immer vor Ort sein muss, gestalten sich Ferndiagnosen (bspw. per Telefon) sehr schwierig. Bei einer solchen Ferndiagose durch den Arzt, kann das medizinische Personal keine Änderungen bezüglich der Diagnose oder der verschriebenen Medikamente vornehmen. Ein Arzt muss für diese Änderungen immer vor Ort am Terminal sein.

Es fehlt eine geignete Rolle, welche Krankenakten wieder entfernen kann, da ein Patient normalerweise das Recht hat seine eigene Daten löschen zu lassen.

* * * * *

Welche Gegenmaßnahmen würdet Ihr für diese Probleme vorschlagen?
-------------



Mögliche Gegenmaßnahmen wären z.B. das alle Mitarbeiter des medizinischen Personals und alle Ärzte eine Schulung erhalten, in der der Umgang mit der digitalen Krankenakte erklärt wird. Dadurch könnten mögliche Fehler bei der Verwaltung von Patientendaten vermieden werden. Damit der Verwaltungsmitarbeiter Abrechnungen erstellen kann wird es nötig sein, das dieser Zugriff auf die Krankenakten bekommt. Es ist aber ausreichend, das der Verwaltungsmitarbeiter nur lesenden Zugriff bekommt und Einträge in den Akten nicht verändern kann. Bisherige Befunde von anderen Ärzten sollten vom medizinischen Personal in die Krankenakte aufgenommen werden und zur Sicherheit einmal mit dem Patienten kommuniziert werden. 

Die Digitalisierung der analogen Patientenakten sollte von einer neuen zuständigen Rolle übernommen werden, sodass sich die Ärzte um diese nicht auch noch kümmern müssen.

Für die Lösungen des Problems mit der An-/Abmeldung und der Ferndiagose, könnte jeder Arzt und medizinisches Personal ein eigenes Terminal (Smartphone) mit sich rumtragen.

Mögliche Gegenmaßnahmen wären z.B. das alle Mitarbeiter des medizinischen Personals und alle Ärzte eine Schulung erhalten, in der der Umgang mit der digitalen Krankenakte erklärt wird. Dadurch könnten mögliche Fehler bei der Verwaltung von Patientendaten vermieden werden. Damit der Verwaltungsmitarbeiter Abrechnungen erstellen kann wird es nötig sein, das dieser Zugriff auf die Krankenakten bekommt. Es ist aber ausreichend, das der Verwaltungsmitarbeiter nur lesenden Zugriff bekommt und Einträge in den Akten nicht verändern kann. Bisherige Befunde von anderen Ärzten sollten vom medizinischen Personal in die Krankenakte aufgenommen werden und zur Sicherheit einmal mit dem Patienten kommuniziert werden. 

Die Digitalisierung der analogen Patientenakten sollte von einer neuen zuständigen Rolle übernommen werden, sodass sich die Ärzte um diese nicht auch noch kümmern müssen.

Für die Lösungen des Problems mit der An-/Abmeldung und der Ferndiagose, könnte jeder Arzt und medizinisches Personal ein eigenes Terminal(Smartphone) mit sich rumtragen.

Um die Konfliktklassen bestehend aus den Ärzten mit meist unterschiedlichen Patienten anzugehen, muss es möglich sein, die erstellten Diagnosen oder Verschreibungen so deutlich mit notwendigen Informationen auszuschmücken, dass nicht involvierte Ärzte die Behandlung ohne Probleme fortsetzten können. Hinzu kommt die Historie, mit welcher die Verantwortungsfrage einer Änderung immer geklärt ist und nachgefragt werden kann. Die Vertraulichkeit der Patientendaten muss sorgfältig abgewogen werden. Ein Arzt sollte nicht in der Lage auf sämtliche Patientendaten zuzugreifen, sondern nur auf seinen Fachbereich oder seine Station. 

Eine Löschung der Daten könnte nach einer gesetzlichen vorgeschriebenen Zeit automatisch passieren. Eine neue Rollen einzuführen die Daten löschen darf, würde zu viele andere Probleme bezüglich der Berechtigungen mit sich ziehen, dass wir uns aus Konfiktgründen dagegen entschieden haben.
* * * * *

Abgabe
------

bis 2021-11-11 23:59 UTC, digital in Stud.IP (und im
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
