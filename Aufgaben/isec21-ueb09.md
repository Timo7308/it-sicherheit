Informationssicherheit, 9. Übung
================================

von Gruppe **G35**
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

*******************

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Was macht die Option `-d`? Was passiert, wenn ihr
dessen Wert in `heise.de` ändert? Warum?

Erstellung des Zertifikates mit `sudo certbot run --nginx -d isec-gruppeYY.informatik.uni-bremen.de \
--redirect --test-cert`

- Mit `--ngix` wird der Webserver angegeben.
- Mit `-d` wird eine Domain angegeben für welche ein Zertifikat erstellt werden soll.
- Das Zertifikat für die Domain `heise.de` kann nicht erstellt werden, da wir nicht mit dem Server verbunden sind, auf welchem die Seite `heise.de` gehostet wird. So wird sichergestellt, dass ein Zertifikat nur von denjenigen erstellt werden kann, welche auch Kontrolle über den Webserver haben.
- Mit `--redirect` wird der Traffic auf HTTPS umgeleitet.
- Mit `--test-cert` wird ein Test-Zertifikat erstellt.


Was könnt Ihr nun beobachten, wenn ihr
https://isec-gruppeYY.informatik.uni-bremen.de/ ansurft? Warum?

- Wir haben unsere Seite nicht vorher aufgerufen und wissen deshalb nicht, welche Änderungen zu beobachten wären.
- Es erscheint eine Warnung. Beim Zugang zur Seite handelt es sich um keine sichere Verbindung. Es wird außerdem vor Hackern gewarnt, welche persönliche Daten stehlen könnten. Zusätzlich kann man sich das Zertifikat der Seite anzeigen lassen. Wenn man nun bestätigt, dass man die Seite trotzdem betreten möchte, erscheint die Fehlermeldung 403 Forbidden. In diesem Fall fehlen die nötigen Berechtigungen, um die Seite zu betreten. Die Fehlermeldung erscheint, weil das Zertifikat als nicht vertrauenswürdig eingestuft wird. 

---

Euer Zertifikat könnt ihr euch mit eurem Browser anschauen. Welche
Informationen enthält euer Zertifikat zu Aussteller und Gültigkeit?
Für wen ist das Zertifikat ausgestellt?

- Der Aussteller des Zertifikates ist Artifical Apricot R3. Das Zertifikat wurde am 17 Dezember 2021 erstellt und ist bis zum 17 März 2022 gültig. Das Zertifikat wurde für https://isec-gruppe35.informatik.uni-bremen.de/ ausgestellt. 

---

Beschreibt, wie ihr vorgegangen seid. Warum und inwieweit kann diesem
Zertifikat vertraut werden? Welche Schritte führt die CA dafür
aus?

- Der Webbrowser vertraut der Seite nicht "This page is not secure (broken HTTPS)", da ein gültiges, vertrauswürdiges Zertifkat fehlt (nicht valid und trusted).
- Mit F12(Chrome) in dem Security-Tab sind die Resourcen und die Verbindung (TLS) als sicher eingestuft worden.
 Das Zertifikat wird als fehlend angegeben, da das Root Zertifikat(Durian) seit 30.01.2021 abgelaufen ist.
 
- Certificate Path (Google Chrome)

  (Staging) Doctored Durian Root CA X3 
  ----(Staging) Pretend Pear X1 
    ------- (Staging) Artifical Apricot R3 
     -----------isec-gruppe35.informatik.de 
     
 Das untere Zertifikat wird immer von den weiter oben liegenden Zertifikaten ausgestellt.

- Unser Testzertifikat wird von einem Root-Zertifikat ausgestellt, welches nicht in Browser-/Client-Truststores vorhanden ist. Deshalb wird dem Testzertifikat nicht vertraut. Dieses Problem kann durch das Hinzufügen des Zertifikats (Staging) Pretend Pear X1 umgangen werden. Letsencrypt weist aber darauf hin, dass dies nur zu Testzwecken geschehen darf, da sonst nicht die nötige Sicherheit gewährleistet werden kann (siehe Quelle).


* * *

Quellen: 

- https://letsencrypt.org/de/docs/staging-environment/
