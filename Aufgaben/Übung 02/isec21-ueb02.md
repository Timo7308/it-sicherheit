Informationssicherheit, 2. Übung
================================

* * * * *

Vorbereitung, Gruppe/einzeln
----------------------------

Jeder von Euch hat einen Zugang zu der FB3-Rechner-Infrastruktur.
Ihr habt hier ein persönliches Verzeichnis für Eure Daten. Zusätzlich
habt Ihr auch die Möglichkeit ein Verzeichnis auf einem zentralen
Webserver zu erhalten.
Sorgt zunächst dafür, dass Ihr per SSH auf die Rechner in der Ebene 0
zugreifen könnt.
Falls Ihr noch keinen SSH-Key hinterlegt habt, könnt Ihr das auf
<https://www.fb3.uni-bremen.de/ssh-pubkey> tun.

Lest Euch die Dokumentation des dort "Homepage" genannten
Web-Verzeichnisses auf
<http://www.informatik.uni-bremen.de/t/homepage-new> durch und führt
die Schritte für die Aktivierung aus.

Aufgabe 1, 4 Punkte, Gruppe/einzeln
-----------------------------------

Nach der Aktivierung des Web-Verzeichnisses (*Webspace*) hast Du nun auch
im Dateisystem unter `/home/wwwu/USER`
(ersetzt `USER` durch Euren eigenen Login-Namen) ein Verzeichnis.
Zunächst kannst nur Du darauf zugreifen.

Lege darin ein Unterverzeichnis `isec-ueb2` an.
-------------------------
Mit `mkdir isec-ueb2` haben wir ein Unterverzeichnis erstellt.
-------------------------
Sorge mit ACLs dafür (aufgerufene Kommandos samt Parametern und Erklärung angeben),
dass:

- Du selbst und Deine Gruppenmitglieder in dieses Verzeichnis
  schreiben (Dateien anlegen und löschen) sowie das Verzeichnis lesen
  könnt;
- Eure Tutoren mit den Login-Namen `rieckers` und
  `gerdes` den Inhalt des
  Verzeichnisses anzeigen können und eine Datei namens `isec-read` lesen
  dürfen, eine Datei namens `isec-noread` aber nicht.
- ansonsten auf den Ordner und die Dateien `isec-read` und `isec-noread`
  kein Zugriff möglich ist. Weitere (Test-)Dateien dürfen beliebige
  Zugriffsrechte besitzen.


-------------------------
`setfacl -m g::--- isec-ueb2/` - keine Rechte für Gruppe
`setfacl -m o:--- isec-ueb2/` - keine Rechte für Other
`setfacl -m u:GRUPPENMITGLIED:rwx isec-ueb2` -für die Gruppenmitglieder alle Rechte
`setfacl -m u:TUTOR:r-x isec-ueb2` - für die Tutoren nur Lese- und Ausführungsrechte 

`cd isec-ueb2` - wechseln in das erstellte Verzeichnis
`echo 'lesbar' > isec-read; chmod 700 isec-read` - es wird eine Datei 'isec-read' erstellt mit dem Inhalt 'lesbar'. Auf diese Datei hat nur der user alle Rechte(rwx) und alle anderen keinen Zugriff.
`setfacl -m u:rieckers:r isec-read` - der Tutor kann die Datei lesen.
`setfacl -m u:gerdes:r isec-read`- der Tutor kann die Datei lesen.

`echo 'nicht lesbar' > isec-read; chmod 700 isec-read` - es wird eine Datei 'isec-read' erstellt mit dem Inhalt 'lesbar'. Auf diese Datei hat nur der user alle Rechte(rwx) und alle anderen keinen Zugriff.
-------------------------
Arbeitet für diese Aufgabe auf dem Rechner
`fido.informatik.uni-bremen.de`.  Der ist von außerhalb des FB3-Netzes nicht direkt zu erreichen; geht erst einmal per SSH auf `login.informatik.uni-bremen.de` und von da aus weiter.

-------------------------
Erst die ssh Verbinung zur Uni herstellen, 
`ssh USER@login.informatik.uni-bremen.de`

dann auf den fido-Rechner wechseln.
`ssh USER@fido.informatik.uni-bremen.de`
-------------------------
Testet Eure Berechtigungen untereinander.
Dokumentiert Euer Vorgehen zum Vergeben der Berechtigungen und zum
Testen.
Legt in dem Verzeichnis eine geeignete Anzahl von Dateien ab, damit
wir die Berechtigungen überprüfen können.
Achtet bei der Vergabe der Rechte auch darauf, dass die Tutoren die
gesetzten Rechte auch überprüfen können müssen.

Für die Bearbeitung des Blatts ist es erforderlich, dass Ihr auch Rechte
auf dem Verzeichnis `/home/wwwu/USER` selbst setzt. Welche Rechte müsst Ihr
mindestens hier setzen? Welche Konsequenzen hat es, wenn Ihr die Rechte
für "Other" setzt?
-------------------------
Alle Gruppenmitglieder haben alle Rechte für das Verzeichnis `/home/wwwu/USER`.
Auch die Tutoren haben Zugriff auf dieses Verzeichnis. Sie dürfen aber keine Dateien erstellen oder löschen/ändern. 
`cd /home/wwwu`
`setfacl -m u:GRUPPENMITGLIED:rwx USER`
`setfacl -m u:TUTOR:r-x USER`
-------------------------
Dies ist eine Einzelaufgabe, ist also von jeder/m Teilnehmenden einzeln
zu bearbeiten.
Ihr könnt die Aufgabe gern in der Gruppe gemeinsam dokumentieren.
Praktisch im Fachbereichsnetz umsetzen soll sie aber jeder selbst, so
dass jedes Gruppenmitglied ein Verzeichnis `/home/wwwu/USER/isec-ueb2` mit
entsprechenden Rechten hat.
Wer dieses Verzeichnis nicht hat, bekommt keine Punkte für die Aufgabe
und hat sie nicht bearbeitet!
**Bitte gebt Eure FB3-Login-Namen in der Abgabe an!**

* * * * *

Abgabe
------

bis 2021-11-04 23:59 UTC, digital in Stud.IP (und im
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

