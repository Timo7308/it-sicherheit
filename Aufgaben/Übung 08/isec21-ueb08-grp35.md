Informationssicherheit, 8. Übung
================================

*******************

Namen und Email-Adressen:

Timo Schuchmann: timo5@uni-bremen.de
Philias Borrmann: borrmann@uni-bremen.de
Adrian Lindloff: lindloff@uni-bremen.de

*******************

**Weshalb ist es sinnvoll, für die Schlüssel ein Ablaufdatum zu definieren?**

- Um ungenutze Schlüssel nach einer Weile automatisch zu deaktivieren.
- Die Sicherheitsanforderungen steigen über die Jahre immer weiter an, weswegen eine Erneuerung nach einiger Jahren sinnvoll ist

**Der Keyserver fordert die Bestätigung eurer E-Mail-Adresse, bevor der
Key mit eurer User-ID veröffentlicht wird. Warum ist das grundsätzlich
sinnvoll?**


- Per E-Mail-Adresse lassen sich Identitäten schnell verifizieren oder erreichen.
- Im Key wird eine E-Mail-Adresse mit angegeben. Durch die Bestätigung wird sichergestellt, dass der Nutzer auch Zugriff auf diese angegebene E-Mail-Adresse hat.

---

**Signiert innerhalb eurer Gruppe eure Schlüssel gegenseitig.
Welche Signierungsstufe (certification level) wählt ihr? Warum?**

Es gibt vier Signierungsstufen zur Auswahl:

  ``sig = "I will not answer"``
  ``sig1 = "I have not checked at all"``
  ``sig2 = "I have done casual checking"``
  ``sig3 = "I have done very careful checking"``

Wir haben uns für Stufe sig2 entschieden, da wir die Fingerabdrücke abgleichen können und uns wegen der Aufgaben vertauen. Für sig3 wäre eine Überprüfung öffentlicher Dokumente sinnvoll.

---



**Beschreibung der Vorgehensweise**

---
Mit Kleopatra haben wir unsere Schlüsselpaare nach den vorgegebenen Bedingungen generiert und anschließend bei https://keys.supersahnetorten.de/upload hochgeladen.
Zur Versendung von verschlüsselten E-Mails haben wir das Mailprogramm Thunderbird verwendet. Im ersten Schritt haben wir unseren eigenen private key und public key in das Mailprogramm geladen. Danach haben wir den public key des jeweils anderen geladen. Den public key haben wir als nächstes signiert. Um sicher zu stellen, dass es sich um den richtigen key handelt, haben wir den fingerprint der public keys im Voicechat von Discord miteinander verglichen. Damit Philias eine E-Mail an Timo schicken kann, benötigt er seinen private key und den public key von Timo. Timo kann die E-Mail dann mit seinem private key entschlüsseln. Damit jemand anderes diese E-Mail lesen kann, müsste herausgefunden werden, welcher public key verwendet wurde und es müsste der PC mit dem zugehörigen private key gehackt werden. Außerdem sind die eigenen keys mit einem Passwort geschützt, welches ebenfalls geknackt werden müsste. Ein Erraten des private keys ist aufgrund dessen Länge nur in der Theorie möglich. Da wir auch nicht über vertrauliche Informationen eines Unternehmens kommunizieren, können wir mit großer Wahrscheinlichkeit davon ausgehen, dass kein anderer versucht unsere E-Mails zu lesen. Es wäre einiges an Arbeit nötig, um die eben genannten Bedingungen zu erfüllen und dies ist deshalb ohne ein Motiv sehr unwahrscheinlich.

Für die Analyse der E-Mails gibt es in Thunderbird die Möglichkeit bestätigt zu bekommen, ob die Nachricht verschlüsselt wurde, mit welcher Technologie sie verschlüsselt wurde und wann sie verschlüsselt wurde (bei uns per OpenPGP). Außerdem wird angezeigt, ob die Nachricht signiert wurde und in welchem Verhältnis der Schlüssel des Empfängers zum Sender steht. Der public key des Empfängers kann beispielsweise vom Sender akzeptiert sein, jedoch dessen Identität unter Umständen noch nicht verifiziert.

---


**Key erstellen:**
--
- https://gpg4win.org/get-gpg4win.html herunterladen und installieren
- cleopatra starten
- File-NEW KEY PAIR erstellen von einem personal OenPGP
- Name und Email angeben und expireDate auf +5Jahre setzen
- key exportieren
- key auf den Keyserver hochladen
