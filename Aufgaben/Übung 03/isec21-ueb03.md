Informationssicherheit, 3. Übung
================================
Wir sind in Gruppe "**G35**". <br />
Philias Borrmann borrmann@uni-bremen.de <br />
Adrian Lindloff lindloff@uni-bremen.de <br />
Timo Schuchmann timo5@uni-bremen.de <br />

* * * * *

Aufgabe 1, 5 Punkte, Gruppe
-----------------------------------

- Nennt mindestens drei Rollen, die bezüglich des Zugriffs auf die
Krankenakte zu unterscheiden sind.


<details><summary>Lösung</summary>

- Ärzte 
- Medizinisches Personal 
- Verwaltungsmitarbeiter 
- _Admin(alle Rechte: hätte zu viele Rechte und könnte ggf. Patienten löschen. Könnte auf Anfrage des Patienten seine Akte löschen)_ 
</details>

-------------

- Welche Aktionen können auf der Krankenakte ausgeführt werden,
d.h. welche Berechtigungen sind zu vergeben?

<details><summary>Lösung</summary>

Berechtigungen auf unterschiedlichen Ebenen (höhere Berechtigungen haben alle tieferen Berechtigungen):

- Medikamente zur Behandlung hinzufügen oder entfernen
- Diagnosen stellen oder ändern <br />
<br />

- Patientendaten aufnehmen oder ändern (Eindeutige Kennung, Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse, Blutgruppe)
- Bisherige Befunde und Therapien bearbeiten oder hinzufügen
- Allergien und Unverträglichkeiten einsehen/ bearbeiten oder hinzufügen
- Zusätzliche Dokumentation und Verwaltungshistorie <br />
<br />

- Patientendaten aufnehmen oder ändern (Eindeutige Kennung, Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse)
- Bisherige Befunde und Therapien einsehen
- Medikamente zur Behandlung einsehen
- Abrechnungen erstellen (Ausnahme: nur für diese Rolle) <br />
<br />

- Patientendaten anzeigen (Eindeutige Kennung, Name, Geburtsdatum, Station, Zimmer) <br />

</details>

-------------


- Erstellt eine geeignete Relation entsprechend des RBAC-Modells,
die die von Euch genannten Rollen mit den Aktionen verknüpft. Wo
kann hier vielleicht Vererbung helfen?

<details><summary>Lösung</summary>

Rolle: lesen(l), schreiben(s) 

| Rollen/Rechte                                 | Ärzte  | Medizinisches Personal | Verwaltungsmitarbeiter |
| --------                                      | ------ | ------                 |------                  |
|eindeutige Kennung (id)                        | l      | l                      | l                      |
|Patientendaten (name, Krankenkasse, ...)       | l,s    | l,s                    | l                      |
|Allergien und Unverträglichkeiten              | l,s    | l,s                    | -                      |
|bisherige Befunde                              | l,s    | l,s                    | -                      |
|verordnete Therapien                           | l,s    | l                      | l                      |
|verschriebene Medikamente                      | l,s    | l                      | l                      |
|Diagnosen                                      | l,s    | l                      | l                      |


_eine Änderung der eindeutigen Kennung sei nicht möglich, um Fehler in der Datenbank zu vermeiden._

Da die Anzahl der Rechte mit jeder Rolle steigen und keine weggnommen werden, können diese Rollen in der gelisteten Reihenfolge vererbt werden.

**Verwaltungsmitarbeiter:** 
Der Verwaltungsmitarbeiter hat nur lesenden Zugriff auf die Aktionen, die für die Abrechnungen wichtig sind.
Die Kennung und Patientendaten sind erforderlich um eine Rechnung an die Krankenkasse des Patienten zu stellen. Die verbundenen Kosten sind hierzu in der Therapie, Medikamenten und Diagnose zu finden. Nach unserer Meinung ist hierzu ein Zugriff auf Alergien und Befunde nicht erforderlich.


**Medizinisches Personal:**
Das medizinische Personal hat lesenden Zugriff auf alle Daten und kann zudem die Daten eines Patienten aufnehmen/aufschreiben.

**Arzt:**
Der Arzt hat die selben Rechte, wie das medizinischen Personal und kann zusätzlich Therapien verodnen, Medikamente verschreiben und Diagnosen erstellen. 


</details>

-------------

- Ihr übernehmt Eure Berechtigungen in die Praxis. Mit welchen
menschlichen und organisatorischen Problemen rechnet Ihr?


<details><summary>Lösung</summary>

Es könnte zu Missverständnissen bei der Kommunikation zwischen Ärzten und medizinischem Personal kommen. Oder Mtarbeiter vom medizinischen Personal sind noch unsicher oder nicht vertraut mit dem System der digitalen Krankenakte und machen möglicherweise Fehler. Daneben stellt sich die Frage, welchen Zugriff der Verwaltungsmitarbeiter auf die Krankenakte hat. Was passiert wenn das System für die digitalen Krankenakten nicht funktioniert? Darf er die Krankenakten einsehen? Wie werden bisherige Befunde und Therapien eines anderen Arztes übernommen, der möglicherweise analoge Patientenakten hat? 

- Problem der Konfliktklassen: Inwiefern kann ein Arzt die Diagnose oder verschriebenen Medikamente eines Patienten beeinflussen,
  für welchen er gar nicht zuständig ist; ist bspw. die Diagnose nachvollziehbar und ausreichend dokumentiert --> können dort Fehler      entstehen, wenn ein anderer Arzt den Patienten behandelt. 

- an/abmelden von medizinischem Personal am Terminal, damit der Arzt eine Diagnose stellen kann, da nur ein Terminal im Zimmer vorhanden ist. (umständlich)


</details>

-------------

- Welche Gegenmaßnahmen würdet Ihr für diese Probleme vorschlagen?

<details><summary>Lösung</summary>


Mögliche Gegenmaßnahmen wären z.B. das alle Mitarbeiter des medizinischen Personals und alle Ärzte eine Schulung erhalten, in der der Umgang mit der digitalen Krankenakte erklärt wird. Dadurch könnten mögliche Fehler bei der Verwaltung von Patientendaten vermieden werden. Damit der Verwaltungsmitarbeiter Abrechnungen erstellen kann wird es nötig sein, das dieser Zugriff auf die Krankenakten bekommt. Es ist aber ausreichend, das der Verwaltungsmitarbeiter nur lesenden Zugriff bekommt und Einträge in den Akten nicht verändern kann. Bisherige Befunde von anderen Ärzten sollten vom medizinischen Personal in die Krankenakte aufgenommen werden und zur Sicherheit einmal mit dem Patienten kommuniziert werden. 

</details>

------

Hinweis: Wenn wir den Patienten ebenfalls (begrenzten) Zugriff auf ihre
Krankenakte geben wollen, stoßen wir unvermeidlich auf eine Beschränkung des grundlegenden RBAC-Mechanismus.  Dieses Problem müsst Ihr in dieser Aufgabe nicht lösen, aber es schadet sicher nicht, auch darüber einmal nachzudenken.

<details><summary>Gedanken</summary>
 Seperation of Duty
</details>

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
