Informationssicherheit, 8. Übung
================================

*******************

Aufgabe 1, 5 Punkte, Gruppe
---------------------------

Macht Euch mit dem System PGP vertraut.  PGP ist spezifiziert in den
OpenPGP-RFCs [RFC 4880]( http://tools.ietf.org/html/rfc4880) und
[RFC 3156]( http://tools.ietf.org/html/rfc3156) und unter anderem
implementiert im Open-Source-Paket [GnuPG]( http://www.gnupg.org/).

Legt Euch (wenn Ihr noch keines habt) je ein persönliches
Schlüsselpaar an, das maximal 5 Jahre gültig ist. Haltet den privaten
Schlüssel auf geeignete Weise geheim. Macht euren Schlüssel bis
**spätestens Di 2021-12-14** auf dem Keyserver
`keys.supersahnetorten.de` bekannt.  
Weshalb ist es sinnvoll, für die Schlüssel ein Ablaufdatum zu definieren?

Bei der Interaktion mit dem Keyserver könnt ihr den URL
hkps://keys.supersahnetorten.de nehmen.

Der Keyserver fordert die Bestätigung eurer E-Mail-Adresse, bevor der
Key mit eurer User-ID veröffentlicht wird. Warum ist das grundsätzlich
sinnvoll?  
Diese Bestätigung muss mindestens für die E-Mail-Adresse, mit der ihr
die geforderten E-Mails verschickt, durchgeführt werden.

Signiert innerhalb eurer Gruppe eure Schlüssel gegenseitig.
Welche Signierungsstufe (certification level) wählt ihr? Warum?

Der Keyserver wird alle Signaturen von anderen Schlüsseln wieder
entfernen. Damit wir eure Signaturen trotzdem überprüfen können, gebt
die öffentlichen Schlüssel mit den importierten Signaturen in der
Abgabe mit ab. (jeweils in einer eigenen Datei, Hilfestellung: `gpg
--export --armor <KEYID>`)

Jedes Gruppenmitglied schickt jedem seiner Gruppenmitglieder eine mit
seinem persönlichen PGP-Schlüssel signierte und mit dem Schlüssel des
Empfängers verschlüsselte E-Mail.

Beschreibt und begründet die wesentliche Schritte in Eurem
Vorgehen. Wie sicher könnt Ihr Euch sein, dass nur der ausgewählte
Gesprächspartner Eure E-Mails lesen kann? Warum? Ist die E-Mail Eurer
Gruppenmitglieder an euch ordnungsgemäß verschlüsselt und signiert?
Wie habt Ihr das überprüft? Welche Software habt ihr für die Analyse
benutzt? Dokumentiert, mit welchem Programm ihr welche Schritte
ausgeführt habt.

**Bitte gebt in Eurer Abgabe an, wer von Euch welche E-Mail-Adresse verwendet hat**.


Weitere Verwendung eures Schlüsselpaares
----------------------------------------

Ziel dieser Aufgabe ist es u.a. auch, dass jeder Teilnehmer ein PGP-Schlüsselpaar hat und
darüber verschlüsselte Mails empfangen kann. Ihr dürft euren Schlüssel dementsprechend auch
auf anderen Keyservern (wie z.B. `keys.openpgp.org`) bekannt machen.


Kleine Hilfestellung zu den Kommandos
-------------------------------------

Für die Bearbeitung können die folgenden gpg-Parameter hilfreich sein.
Macht euch selbst (z.B. über die manpage) mit den Effekten vertraut.

* `--ask-cert-level`
* `--fingerprint`
* `--full-gen-key`
* `--keyserver`



* * * * *

Abgabe
------


bis 2021-12-16 23:59 UTC, digital in Stud.IP als Markdown-Datei mit dem
Dateinamen `isec21_ueb08_grpYY.(md|zip|tgz)` (das `YY` mit eurer Gruppennummer ersetzen).
Dabei bitte in der Datei die Nummer Eurer Gruppe in Stud.IP sowie alle
an der Abgabe beteiligten Gruppenmitglieder (und deren E-Mail-Adressen) nennen.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen aus dem Netz bedient (Anleitungen,
Howtos, etc), gebt diese bitte als URI mit an.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
