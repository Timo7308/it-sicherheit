Informationssicherheit, 10. Übung
================================

*******************

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

---

*Angenommen, ihr solltet eine IT-Strukturanalyse durchführen. Wie
würdet ihr vorgehen, das heißt, welche Schritte sind durchzuführen?*

Grundsätzlich würden wir uns an die vom BSI empfohlene Vorgehensweise halten.

**1. Informationen erheben und die vorhandene Infrastruktur analysieren** 
--> wesentliche Geschäftsprozesse listen
--> zu schützende IT-Anwendungen listen
--> ggf. Geschäftsprozesse und dessen Anwendungen verknüpfen

**2. Aktuellen Netzplan erstellen**
--> IT-Systeme und dessen Vernetzungen/Verbindungen untereinander, sowie Außenverbindungen darstellen
--> Komponenten ggf. bereinigen und gruppieren

**3. IT-Systeme erfassen**
--> Auflistung der IT-Systeme und von wem sie alles benutzt werden
--> Zu den IT-Systemen gehören alle elektronischen datenverarbeitende Systeme, die im Unternehmen genutzt werden

**4. Räume erfassen**
--> IT-bezogene Gebäude und Raume, sowie spezielle Schutzobjekte (z.B. Schutzschrank)


---------------------------------

Vorgehensweise auf das Beispiel bezogen:

**1.** 
Da wir nicht genau wissen, was das Unternehmen herstellt, können wir die Geschäftsprozesse nur grob auflisten. Dennoch können wir folgende Informationen erheben: 
 - Überblick über die Anzahl der Mitarbeiter in den einzelnen Abteilungen verschaffen.
 - Daran anschließend überlegen, welcher Mitarbeiter welchen Computer braucht. Welche Mitarbeiter benutzen welche IT-Anwendungen?
 - Festlegen wie interne Daten verwaltet werden.
 - Interne Kommunikation planen. Zugang für Mitarbeiter aus dem Außendienst zum Intranet planen.

**2.**
 - Überlegen an welchen Stellen Server zum Einsatz kommen, und wie die einzelnen Komponenten verbunden werden.

**3.**
 - Einheitliches Vorgehen zur Authentisierung von Mitarbeitern und Geräten festlegen.
 - Kommunikation per Email in dem Unternehmen untersuchen.
 - Datenspeicherungssysteme betrachten.
 - Bereitstellung der öffentlichen Website untersuchen.

**4.** 
Wird für dieses Beispiel nicht benötigt.

---



*Erstellt einen Netzplan. Gruppiert die angegebenen Komponenten
sinnvoll. Trefft, wo erforderlich, ergänzende Annahmen. Dokumentiert
Euer Vorgehen.*


![](https://hackmd.informatik.uni-bremen.de/uploads/36132e07d272621fb3752ce66.40.07.png)

Um einen vollständigen Netzplan für das Unternehmen zu erstellen, haben wir die erforderlichen Web-, Mail- und den zentralen Datenbank-Server mit einem Switch angeschlossen, wodurch alle Computer verbunden sind. Die Firewall sorgt für einen geschützen Zugriff in das Intranet und der Router verbindet das Unternehmen mit dem Internet und somit auch mit dem Außendienst im Homeoffice. Der Domänencontroller ist ein Server zur  Authentifizierung von Benutzern und Computern.


---

*Erhebt die IT-Systeme für die Strukturanalyse. Welche Informationen
benötigt Ihr dafür?*

- Wie viele Mitarbeiter gibt es im Unternehmen? 
- Wie viele Mitarbeiter arbeiten in jeder Abteilung? 
- Wie viele Mitarbeiter arbeiten im Außendienst? 
- Welche Zugriffsrollen gibt es? Welche Rolle ist verantwortlich für ein IT-System?
- Wie wird die interne Kommunikation geregelt? 
- Wie können sich Mitarbeiter an ihren Computern anmelden? 
- Wie erhalten die Mitarbeiter im Außendienst Zugang zum Intranet? 
- Nutzen die Mitarbeiter im Außendienst nur einen Laptop? 
- In welchen Räumen bzw. an welchem Standort steht ein IT-System und wie ist dessen Status?
- Wie gestalten wir die Kriterien für das Gruppieren von IT-Systemen
- Falls ein IT-System mehrere zusammenfasst, wie viele IT-Systeme werden abgebildet? 
- Wie viele Server werden benötigt? 
- Wie wird das Intranet nach außen hin geschützt? 


**IT-Systeme:**
- Arbeitsplatz-Computer
- HomeOffice-Computer/Laptop
- Mail-Server
- (Druck-Server)
- Domäncontroller (Anmeldung an den internem System)
- Zentraler Server (Datenbank) mit Backup
- Webserver (öffentliche Website/ Dokumente mit eingeschränktem Zugriff)
- Switch
- Firewall
- Router (mit Internetanbindung)



---



*Erstellt eine Tabelle der denkbaren IT-Anwendungen.
Identifiziert die drei aus Eurer Sicht wichtigsten.
Ordnet diesen jeweils diejenigen IT-Systemkomponenten zu, die für ihre
Ausführung benötigt werden.*


**IT-Anwendungen**
- Verwaltung, Buchhaltungs-Software, Präsentationen etc. (Office, DBMS ggf. über Webanwendung)
- Emailprogramm (z.B. Thunderbird)
- Authorisierung über Verzeichnisdienst (um sich im Intranet anzumelden, mit Rollen/Rechten Modell)
- Auftrags- und Kundenverwaltung
- Manuelle oder automaitsche Backup-Anwendung
- Druckservice


**Tabelle	der drei wichtigsten IT-Anwendungen**

| Bezeichnung |Beschreibung | Anzahl | Benutzer| IT-Systemkomponenten|
| -------- | --------   | --------   |   --------     |   --------       |        
| A01     |  Verwaltung, Buchhaltungs-Software, Präsentationen: Alle gschäftlichen Informationen werden über eine Software verwaltet, die Zugriff zu dem internen Datenbank-Server hat. Bsp. Office, oder interne Webanwendung| 5     |   Verwaltung, Buchhaltung   |    Computer, Switch, zentraler DB-Server, Webserver     |
|A02 | Kommunikation: Die Unternehmenskommunikation findet über Mail statt, die von einer Mail-Software(Bsp. Thunderbird) gestreuert wrid | 60 | Alle Mitarbeiter | Computer/Laptop, Router, Switch, Firewall, Mail-Server
|A03 |Backup: ein Backup der Datenbank wird jede Nacht vorgenommen | 1  | Administrator | zentraler DB-Server 






























* * *

Abgabe
------

bis 2022-01-13 23:59 UTC, digital in Stud.IP als Markdown-Datei mit
dem Dateinamen `isec21_ueb10_grpYY.(md|zip|tgz)` (das `YY` mit Eurer
Gruppennummer ersetzen).  Dabei bitte in der Datei die Nummer Eurer
Gruppe in Stud.IP sowie alle an der Abgabe beteiligten
Gruppenmitglieder nennen.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen aus dem Netz bedient (Anleitungen,
Howtos, etc.), gebt diese bitte als URI mit an.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
