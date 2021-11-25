Informationssicherheit, 5. Übung
================================
von Gruppe **G35** 
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Anmerkung: Jegliche durch die Nmap Scriping Engine ermöglichten Scripts (für diese Aufgabe besonders Vuln-Scripts) haben wir **nicht** verwendet, in der Hoffnung so keinen Schaden anzurichten.

Nutzt bei `nmap`, sofern es Euch sinnvoll erscheint, die Optionen
`-sV`, `-O` und `-p`. Wie arbeiten diese intern ungefähr? 
- Nmap nutzt standardmäßig ein TCP-scan welcher in der Vorlesung unter RST-Attacks genannt wurde. Hierbei wird der Three-Way-Handshake abgeschlossen und die Verbindung wird sofort wieder geschlossen um DoS zu vermeiden. 
- `-sV` Service Version: Mit dieser Option können Softwareversionen erkannt werden. Erst wird der Service des angegebenen Ports ermittelt, dann die konkrete Software dieses Services und dessen Version. Mithilfe der Datenbank nmap-services wird ein Service für den Port ermittelt. Die Datenbank nmap-service-probes enthält Proben, mit welchen verschiedene Services abgefragt und dort diverse Ausdrücke miteinander abgeglichen werden, um Antworten zu untersuchen und an genauere Informationen zu gelangen.
  `-O` Operating System detection: Die Hauptfunktionalität dieser Option ist die "Schätzung" des Betriebsystems eines Hosts. Die unterschiedlichen Betriebssysteme benutzen verschiedene Netzwerkprotokolle und Netzwerkdienste. Während dem Scan sucht Nmap nach solch spezifischen Merkmalen des Hosts und gleicht sie mit einer Datenbank ab.
  `-p` for specific Ports: Die anzusprechenden Ports spezifizieren. Es können sowohl einzelne Ports, ein Bereich zwischen Ports (z.B. -p 5000-8000) oder alle Ports mit -p- gescannt werden.
- Ein Port hat entweder den Status `open, closed` oder `filtered`. Bei `open, closed` ist der Service auf dem Port aktiv, aber bei `closed` wird zusätzlich die Verbindung abgelehnt. Bei `filtered` gibt es keine Antwort von dem Host auf dem Port und somit auch keine Sicherheitsbedenken. Ein offener oder auch geschlossener Port kann für Angriffe auf das Netz genutzt werden. Dabei ist die Verwundbarkeit dieses Ports abhänging von dem Betriebssystem und dem Service, welcher diesen Dienst bereitstellt. Bei einem Scan mit `-sV` oder auch `-O` erlangen wir Erkenntnisse über diesen Service und können ggf. Sicherheitslücken dieser Version ausnutzen.

Rechner zuhause
--

Welchen Weg nehmen Eure Pakete?
```
->tracert 134.102.201.110
Tracing route to kipos.informatik.uni-bremen.de [134.102.201.110]
over a maximum of 30 hops:

  1    <1 ms    <1 ms    <1 ms  192.168.0.1
  2     9 ms    14 ms     7 ms  ip53a9b75d.static.kabel-deutschland.de [83.169.183.93]
  3    14 ms     8 ms    10 ms  ip5886ea39.static.kabel-deutschland.de [88.134.234.57]
  4     9 ms    12 ms    17 ms  145.254.3.122
  5    18 ms    16 ms    21 ms  145.254.2.51
  6    22 ms    14 ms    14 ms  145.254.2.51
  7    15 ms    21 ms    16 ms  dfn.bcix.de [193.178.185.42]
  8    25 ms    29 ms    22 ms  cr-han2-be7.x-win.dfn.de [188.1.144.137]
  9    25 ms    24 ms    25 ms  kr-bre66-0.x-win.dfn.de [188.1.244.190]
 10    28 ms    24 ms    28 ms  v6500-po405.noc.uni-bremen.de [134.102.0.14]
 11    41 ms    30 ms    48 ms  fb3-c4500x-po3.noc.uni-bremen.de [134.102.0.38]
 12    20 ms    36 ms    25 ms  kipos.informatik.uni-bremen.de [134.102.201.110]

Trace complete.

->tracert 134.102.50.15
Tracing route to gabriel-smtp.zfn.uni-bremen.de [134.102.50.15]
over a maximum of 30 hops:
...
 10    85 ms    83 ms    24 ms  v6500-po405.noc.uni-bremen.de [134.102.0.14]
 11   201 ms    21 ms    20 ms  hc-n7000-a-e1-1.noc.uni-bremen.de [134.102.0.66]
 12    25 ms    22 ms    23 ms  gabriel-smtp.zfn.uni-bremen.de [134.102.50.15]

Trace complete.
```
- Eine traceroute von dem x01 Rechner in dem Uni-Netz führte bei uns zu keinem Ergebnis. Keiner der Hops konnte aufgelöst werden.
---
**Option** `-sV` auf IPv4-Adresse 134.102.50.15:
```
->nmap -sV 134.102.50.15
Starting Nmap 7.80 ( https://nmap.org ) at 2021-11-25 01:41 CET
Nmap scan report for gabriel-smtp.zfn.uni-bremen.de (134.102.50.15)
Host is up (0.032s latency).
Not shown: 993 filtered ports
PORT    STATE SERVICE        VERSION
25/tcp  open  smtp           Postfix smtpd
110/tcp open  pop3-proxy     Perdition pop3 proxy
143/tcp open  imap
465/tcp open  ssl/smtp       Postfix smtpd
587/tcp open  smtp           Postfix smtpd
993/tcp open  ssl/imap
995/tcp open  ssl/pop3-proxy Perdition pop3 proxy
2 services unrecognized despite returning data. ...

```
- Für den Service `imap` und `ssl/imap` wurde keine Version gefunden.
- Die gelisteten offenen Ports sind alles Dienste für ein Mailserver.

---
**Option** `-O` auf IPv4-Adresse 134.102.50.15::
```
->nmap -O 134.102.50.15
...
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 (97%), Linux 2.6.35 (97%), Linux 3.10 (97%), Linux 3.4 (97%), Linux 3.5 (97%), Linux 3.7 (97%), Linux 4.2 (97%), Linux 4.4 (97%), Synology DiskStation Manager 5.1 (97%), WatchGuard Fireware 11.8 (97%)

```
- `-O` OS-Guessing: Die Wahrscheinlichkeit der Korrektheit dieser Schätzung ist sehr hoch. Als Ergebnis werden viele Versionen ausgegeben, welche teilweise sogar um Major-Versionen auseinanderliegen.
---

**Option** `-sV` auf IPv4-Adresse 134.102.201.110:
```
->nmap -sV -p- 134.102.201.110
Starting Nmap 7.60 ( https://nmap.org ) at 2021-11-25 14:55 MET
Nmap scan report for kipos.informatik.uni-bremen.de (134.102.201.110)
Host is up (0.00086s latency).
Not shown: 65528 filtered ports
PORT     STATE  SERVICE    VERSION
22/tcp   open   ssh        OpenSSH 8.4p1 Debian 5 (protocol 2.0)
80/tcp   open   http       lighttpd 1.4.59
443/tcp  open   ssl/http   lighttpd 1.4.59
5683/tcp open   coap?
5684/tcp open   ssl/coaps?
7743/tcp closed sstp-1
7744/tcp closed raqmon-pdu
2 services unrecognized despite returning data...

```
- Die Dienste http/https können zu einem Webserver gehören.
- Ein Scan mit `-A` gibt ein Https-title an mit griecheschen Zeichen als UTF-8 Kodierung. Decoded: `κήπος` übersetzt: Garten. Es handelt sich somit um einen Webserver.
- CoAP und CoAPs sind auch passende Dienste für ein Webserver. Diese sind Web-Transfer-Protokolle, welche für IoT genutzt werden.
- Der ssh-Dienst sollte vielleicht auch nur innerhalb des Uni-Netzes angeboten werden, wie es auch bei dem Mailserver ist.  

---
**Option** `-O` auf IPv4-Adresse 134.102.201.110:

```
->nmap -O 134.102.201.110
...
Running (JUST GUESSING): Linux 2.6.X (86%)
OS CPE: cpe:/o:linux:linux_kernel:2.6
Aggressive OS guesses: Linux 2.6.18 - 2.6.22 (86%)
No exact OS matches for host (test conditions non-ideal).
...
```
- `-O` OS-Guessing: Hier ist die Wahrscheinlichkeit der Korrektheit dieser Schätzung geringer, dafür ist allerdings die Schätzung der Betriebssystemversion klarer eingerahmt und bleibt innerhalb einer Minor-Version.
---
Welche zusätzlichen Erkenntnisse gewinnt Ihr, wenn Ihr `-p 5000-8000` angebt?

- Der Dienst auf dem Port 5638 ist das Constrained Application Protocol (CoAP),welches ein Web-Transfer-Protokoll für das Internet of Things von Carsten Borrmann ist.

Rechner aus dem Uni-Netz
--

Wir haben den Rechner **x01** genutzt.
Bei dem Scan des Webservers(`134.102.201.110`) sind uns keine Unterschiede aufgefallen, wenn wir diesen aus dem Uni-Netz scannen.


Der ssh-Port von dem Mailserver(`134.102.50.15`) ist aus dem Uni-Netz zusätzlich erreichbar.

```
->nmap -Pn -p22 134.102.50.15

Starting Nmap 7.60 ( https://nmap.org ) at 2021-11-25 15:56 MET
Nmap scan report for 134.102.50.15
Host is up (0.00033s latency).

PORT   STATE SERVICE
22/tcp open  ssh
```

Eine traceroute konnte wegen fehlender Root-Rechte nicht durchgeführt werden.
* * * * *


Quellen
------
https://www.elektronik-kompendium.de/sites/net/2103021.htm (letzter Zugriff: 25.11.2021)

https://linuxhint.com/nmap_version_scan/ (letzter Zugriff: 25.11.2021)

https://nmap.org/book/man-version-detection.html (letzter Zugriff: 25.11.2021)

https://coap.technology/ (letzter Zugriff: 24.11.2021)

https://en.wikipedia.org/wiki/Port_scanner (letzter Zugriff: 24.11.2021)
