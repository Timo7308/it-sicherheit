Informationssicherheit, 8. Übung
================================

*******************

Aufgabe 1, 5 Punkte, Gruppe
---------------------------
Namen und Email-Adressen:

Timo Schuchmann: timo5@uni-bremen.de
Philias Borrmann: borrmann@uni-bremen.de
Adrian Lindloff: lindloff@uni-bremen.de



Weshalb ist es sinnvoll, für die Schlüssel ein Ablaufdatum zu definieren?

- Um ungenutze Schlüssel nach einer Weile automatisch zu deaktivieren.
- Die Sicherheitsanforderungen steigen über die Jahre immer weiter an, weswegen eine Erneuerung nach einiger Jahren sinnvoll ist

Der Keyserver fordert die Bestätigung eurer E-Mail-Adresse, bevor der
Key mit eurer User-ID veröffentlicht wird. Warum ist das grundsätzlich
sinnvoll?  

- Per E-Mail-Adresse lassen sich Identitäten schnell verifizieren oder erreichen.
- In dem Key wird eine E-Mail-Adresse mit angegeben. Durch die Bestätigung wird sichergestellt, dass der Nutzer auch Zugriff auf diese angegebene E-Mail-Adresse hat.

---

Signiert innerhalb eurer Gruppe eure Schlüssel gegenseitig.
Welche Signierungsstufe (certification level) wählt ihr? Warum?

Es gibt vier Signierungsstufen zur Auswahl:

  ``sig = "I will not answer"``
  ``sig1 = "I have not checked at all"``
  ``sig2 = "I have done casual checking"``
  ``sig3 = "I have done very careful checking"``

Wir haben uns für Stufe sig2 entschieden, da wir die Fingerabdrücke abgleichen können und uns wegen der Aufgaben vertauen. Für sig3 wäre eine Überprüfung öffentlicher Dokumente sinnvoll.

---


Beschreibt und begründet die wesentliche Schritte in Eurem
Vorgehen. Wie sicher könnt Ihr Euch sein, dass nur der ausgewählte
Gesprächspartner Eure E-Mails lesen kann? Warum? Ist die E-Mail Eurer
Gruppenmitglieder an euch ordnungsgemäß verschlüsselt und signiert?
Wie habt Ihr das überprüft? Welche Software habt ihr für die Analyse
benutzt? Dokumentiert, mit welchem Programm ihr welche Schritte
ausgeführt habt.

**Bitte gebt in Eurer Abgabe an, wer von Euch welche E-Mail-Adresse verwendet hat**.

---
Mit Kleopatra haben wir unsere Schlüsselpaare nach den vorgegebenen Bedingungen generiert und anschließend bei https://keys.supersahnetorten.de/upload hochgeladen.
Zur Versendung von verschlüsselten E-Mails haben wir das Mailprogramm Thunderbird verwendet. Im ersten Schritt haben wir unseren eigenen private key und public key in das Mailprogramm geladen. Danach haben wir den public key des jeweils anderen geladen. Den public key haben wir als nächstes signiert. Um sicher zu stellen, dass es sich um den richtigen key handelt, haben wir den fingerprint der public keys im Voicechat von Discord miteinander verglichen. Damit Philias eine E-Mail an Timo schicken kann, benötigt er seinen private key und den public key von Timo. Timo kann die E-Mail dann mit seinem private key entschlüsseln. Damit jemand anderes diese E-Mail lesen kann, müsste herausgefunden werden, welcher public key verwendet wurde und es müsste der PC mit dem zugehörigen private key gehackt werden. Außerdem sind die eigenen keys mit einem Passwort geschützt, welches ebenfalls geknackt werden müsste. Ein erraten des private keys ist aufgrund dessen Länge nur in der Theorie möglich. Da wir auch nicht über vertrauliche Informationen eines Unternehmens kommunizieren, können wir mit großer Wahrscheinlichkeit davon ausgehen, dass kein anderer unsere E-Mails lesen kann. Es wäre einiges an Arbeit nötig, um die eben genannten Bedingungen zu erfüllen und dies ist deshalb ohne ein Motiv sehr unwahrscheinlich.

Für die Analyse der E-Mails gibt es in Thunderbird die Möglichkeit bestätigt zu bekommen, ob, mit welcher Technologie und wann die Nachricht verschlüsselt wurde (bei uns per OpenPGP). Außerdem wird angezeigt, ob die Nachricht signiert wurde und in welchem Verhältnis der Schlüssel des Empfängers zum Sender steht. Der public key des Empfängers kann beispielsweise vom Sender akzeptiert sein, jedoch dessen Identität unter Umständen noch nicht verifiziert.

---


Key erstellen:
--
- https://gpg4win.org/get-gpg4win.html herunterladen und installieren
- cleopatra starten
- File-NEW KEY PAIR erstellen von einem personal OenPGP
- Name und Email angeben und expireDate auf +5Jahre setzen
- key exportieren
- key auf den Keyserver hochladen








```
KEY von borrmann@uni-bremen.de
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
BPLUcFXBt675s7eGG4kc7025fmwAzTscEg==
=eflV
-----END PGP PUBLIC KEY BLOCK-----

```



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
