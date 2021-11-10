Informationssicherheit, 3. Übung
================================

* * * * *

Aufgabe 1, 5 Punkte, Gruppe
-----------------------------------

Ein Krankenhaus hat eine digitale Krankenakte eingeführt. Diese
enthält folgende Informationen: eindeutige Kennung, Name, Adresse,
Geburtsdatum, Station, Zimmer, Krankenkasse, Blutgruppe,
Allergien/Unverträglichkeiten, verschriebene Medikamente, bisherige
Befunde und verordnete Therapien.

Nur Ärzte dürfen Diagnosen stellen oder verändern. Alle vorgenommenen
Maßnahmen müssen vom medizinischen Personal in der Akte dokumentiert
werden. Ein entsprechendes Terminal steht in jedem Zimmer. Die
digitale Akte wird auch vom zuständigen Verwaltungsmitarbeiter
herangezogen, um Abrechnungen zu erstellen.

- Nennt mindestens drei Rollen, die bezüglich des Zugriffs auf die
Krankenakte zu unterscheiden sind.


<details><summary>Lösung</summary>

- Ärzte 
- Medizinisches Personal 
- Verwaltungsmitarbeiter 
- Mitarbeiter für technische Wartung 

</details>


- Welche Aktionen können auf der Krankenakte ausgeführt werden,
d.h. welche Berechtigungen sind zu vergeben?

<details><summary>Lösung</summary>

Berechtigungen auf unterschiedlichen Ebenen (höhere Berechtigungen haben alle tieferen Berechtigungen):

- Medikamente zur Behandlung hinzufügen oder entfernen
- Diagnosen stellen oder ändern 

- Patientendaten aufnehmen oder ändern (Eindeutige Kennung, Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse, Blutgruppe)
- Bisherige Befunde und Therapien bearbeiten oder hinzufügen
- Allergien und Unverträglichkeiten einsehen/ bearbeiten oder hinzufügen
- Zusätzliche Dokumentation

- Patientendaten aufnehmen oder ändern (Eindeutige Kennung, Name, Adresse, Geburtsdatum, Station, Zimmer, Krankenkasse)
- Bisherige Befunde und Therapien einsehen
- Medikamente zur Behandlung einsehen
- Abrechnungen erstellen 

- Patientendaten anzeigen (Eindeutige Kennung, Name, Geburtsdatum, Station, Zimmer)

</details>



- Erstellt eine geeignete Relation entsprechend des RBAC-Modells,
die die von Euch genannten Rollen mit den Aktionen verknüpft. Wo
kann hier vielleicht Vererbung helfen?



- Ihr übernehmt Eure Berechtigungen in die Praxis. Mit welchen
menschlichen und organisatorischen Problemen rechnet Ihr?


<details><summary>Lösung</summary>

Es könnte zu Missverständnissen bei der Kommunikation zwischen Ärzten und medizinischem Personal kommen. Oder Mtarbeiter vom medizinischen Personal sind noch unsicher oder nicht vertraut mit dem System der digitalen Krankenakte und machen möglicherweise Fehler. Daneben stellt sich die Frage, welchen Zugriff der Verwaltungsmitarbeiter auf die Krankenakte hat. Was passiert wenn das System für die digitalen Krankenakten nicht funktioniert? Worauf bekommt der Techniker Zugriff? Darf er die Krankenakten einsehen? Wie werden bisherige Befunde und Therapien eines anderen Arztes übernommen, der möglicherweise analoge Patientenakten hat? 

- Problem der Konfliktklassen: Inwiefern kann ein Arzt die Diagnose oder verschriebenen Medikamente eines Patienten beeinflussen,
  für welchen er gar nicht zuständig ist; ist bspw. die Diagnose nachvollziehbar und ausreichend dokumentiert --> können dort Fehler      entstehen, wenn ein anderer Arzt den Patienten behandelt. 

- 


</details>


- Welche Gegenmaßnahmen würdet Ihr für diese Probleme vorschlagen?

<details><summary>Lösung</summary>


Mögliche Gegenmaßnahmen wären z.B. das alle Mitarbeiter des medizinischen Personals und alle Ärzte eine Schulung erhalten, in der der Umgang mit der digitalen Krankenakte erklärt wird. Dadurch könnten mögliche Fehler bei der Verwaltung von Patientendaten vermieden werden. Damit der Verwaltungsmitarbeiter Abrechnungen erstellen kann wird es nötig sein, das dieser Zugriff auf die Krankenakten bekommt. Es ist aber ausreichend, das der Verwaltungsmitarbeiter nur lesenden Zugriff bekommt und Einträge in den Akten nicht verändern kann. Für die technische Wartung würde es Sinn machen, einen Mitarbeiter des Karankenhauses heranzuziehen. Das könnte jemand sein, der bereits für weitere Technik im Krankenhaus zuständig ist. Wenn es nötig ist, kann der Techniker wie der Verwaltungsmitarbeiter die Krankenakten einsehen aber nicht verändern. Bisherige Befunde von anderen Ärzten sollten vom medizinischen Personal in die Krankenakte aufgenommen werden und zur Sicherheit einmal mit dem Patienten kommuniziert werden. 

</details>


Hinweis: Wenn wir den Patienten ebenfalls (begrenzten) Zugriff auf ihre
Krankenakte geben wollen, stoßen wir unvermeidlich auf eine Beschränkung des grundlegenden RBAC-Mechanismus.  Dieses Problem müsst Ihr in dieser Aufgabe nicht lösen, aber es schadet sicher nicht, auch darüber einmal nachzudenken.


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
