Informationssicherheit, 9. Übung
================================

*******************

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Euer Onkel besitzt eine Konditorei. Er möchte seine Kundschaft um
Post-Millenials erweitern. Ihr sollt den Webserver aufsetzen und
natürlich soll alles „sicher“ sein. Dementsprechend müsst Ihr u.a. ein
Zertifikat erstellen und von einer geeigneten Zertifizierungsstelle
unterzeichnen lassen, damit es letztendlich über die in den Webbrowsern
der Kunden eingebauten Stammzertifikate anerkannt wird.  

Erstellt euch per "Let's Encrypt" (<https://letsencrypt.org/>) ein
Zertifikat für die Webseite isec-gruppeYY.informatik.uni-bremen.de
(wobei ihr YY mit eurer Gruppennummer ersetzt). Verbindet Euch dazu mit
dem Fachbereichsrechner isecle.informatik.uni-bremen.de (mit dem Umweg
über login). Verwendet dann das Tool certbot zur
Erstellung des Zertifikats:

`sudo certbot run --nginx -d isec-gruppeYY.informatik.uni-bremen.de \
--redirect --test-cert`

**Wichtig: erstellt das Zertifikat mittels `--test-cert` als
Testzertifikat.** (Produktiv-Zertifikate unterliegen bestimmten
Limitierungen). Was macht die Option `-d`? Was passiert, wenn ihr
dessen Wert in `heise.de` ändert? Warum?

Wenn das Erstellen des Zertifikats erfolgreich war, startet den Web
Server mit dem folgenden Kommando neu:

`sudo systemctl reload nginx`

Was könnt Ihr nun beobachten, wenn ihr
https://isec-gruppeYY.informatik.uni-bremen.de/ ansurft? Warum?

Euer Zertifikat könnt ihr euch mit eurem Browser anschauen. Welche
Informationen enthält euer Zertifikat zu Aussteller und Gültigkeit?
Für wen ist das Zertifikat ausgestellt?

Beschreibt, wie ihr vorgegangen seid. Warum und inwieweit kann diesem
Zertifikat vertraut werden? Welche Schritte führt die CA dafür
aus?

**Dokumentiert Euer Vorgehen schrittweise, begründet ggf. die gewählten
Optionen/Parameter**.

* * *

Abgabe
------

bis 2022-01-06 23:59 UTC, digital in Stud.IP als Markdown-Datei mit
dem Dateinamen `isec21_ueb09_grpYY.(md|zip|tgz)` (das `YY` mit eurer
Gruppennummer ersetzen).  Dabei bitte in der Datei die Nummer Eurer
Gruppe in Stud.IP sowie alle an der Abgabe beteiligten
Gruppenmitglieder nennen.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen aus dem Netz bedient (Anleitungen,
Howtos, etc), gebt diese bitte als URI mit an.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
