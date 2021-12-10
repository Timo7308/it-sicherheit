Informationssicherheit, 7. Übung
================================

* * * * *


Aufgabe 1, 4 Punkte, Gruppe
---------------------------

Xowj tzwyw Moxfmrw dmrwi hzj twi Cwkc wzi hwizf vwjyadnowywnc, tmszc
wy izadc uo wzixmad hzjt. Hzw iwiic smi tzw Mjc twj Vwjyadnowyywnoif,
tzw hzj dzwj mifwhwitwc dmrwi? Hzwyl zyc yzw yl wzixmad uo gimagwi?
Hwnadwj Vljfwdwi zyc uos Wicyadnowyywni ylnadwj Imadjzadcwi ms rwycwi?
Hzw ywzt zdj vljfwfmifwi, os mox twi Gnmjcwkc uo glsswi?  Fwrc twi
glsqnwccwi oivwjyadnowyywncwi Cwkc zi Wojwj Mrfmrw mi. Vwjhwitwc
tmxowj wziw Smjgtlhi-Altw-Osfwroif.

Sltwjiwjw Vwjxmdjwi yzit swzyc izadc yl nwzadc uo rjwadwi. Hwnadw
hzadczfw Jlnnw yqzwnc tmrwz tzw Nmwifw twy Yadnowyywny? Hwnadw
Yadnowyywnnmwifw wsqxwdnc Zdj xowj twi Wziymcu szc MWY, xowj hwnadw
Mjcwi vli Mihwitoifwi yzit hwnadw Yadnowyywnnmwifwi wsqxwdnwiyhwjc?
Rwjwadiwc, hzw nmifw wowj Jwadiwj zi wchm rjmoadwi howjtw, os rwz
Vwjhwitoif tzwywy Vwjxmdjwiy wziwi Yadnowyywn twj wsqxldnwiwi Nmwifw
uo rjwadwi.

**Dokumentiert eure Vorgehensweise und nennt die Quellen, die ihr
benutzt habt.**

* * * * *

Aufgabe 2, 4 Punkte, Gruppe
----------------------------

Bei einem System zur Rechnungsverwaltung der Firma "Secure Billing"
werden die ausstehenden Beträge in Latex-Dokumenten gespeichert, die
zur Darstellung zu PDF-Dateien kompiliert werden. Hier ein Ausschnitt
aus einer solchen Datei:

```
...
42,42Euro
11,20Euro%vom 1.1.2021
2000Euro
...
```

Zur Sicherung der Integrität der Daten werden in einer separaten
Datenbank für jeden Eintrag (Zeile ohne Zeilenende) aus dem
Tex-Dokument jeweils ein einzelner Hash gespeichert.  Dabei kommt
folgende, nicht standardisierte
Hashfunktion zum Einsatz:

```
char * hash (char * data){
	char * hashed_data = calloc(sizeof(char), 16);
	int i=0;
	while (i<32){
		hashed_data[i%15] = 'A' + (hashed_data[i%15] + 13*i + (*data)) % ('Z' - 'A' + 1);
		data++; i++;
	}
	return (hashed_data);
}
```

Die Einträge sind bis zu 32 Zeichen lang, beim Einlesen werden nicht belegte Zeichen durch 0-Bytes (`\0`) auf 32 Byte aufgefüllt.

Ihr möchtet nun einen Rechnungsbetrag ändern. Ihr habt auch eine
Sicherheitslücke auf dem Server der "Secure Billing" gefunden, über
die ihr die Datensätze manipulieren könnt.  Ihr habt aber keinen
Zugriff auf die gespeicherten Hashes, müsst die Sicherung durch Hashwerte also überwinden.

Wie könnt ihr dennoch den Eintrag **2000Euro** zu einem Eintrag, der
als **20Euro** dargestellt wird verändern, ohne dass die Betreiber des
Systems Verdacht schöpfen? Welchen Effekt hat die Manipulation von
Zeichen an verschiedenen Stellen? Welche Stellen müsst Ihr ändern?
Warum? Welche Eigenschaft der vorgegebenen Funktion hat die Lösung für
euch stark vereinfacht?

Beschreibt euer Vorgehen und gebt den manipulierten Eintrag an! Beschreibt eine Gegenmaßnahme um euren Angriff zu verhindern.

**Hinweis**: In Latex leitet das Prozent-Zeichen ("%") einen Kommentar bis zum Zeilenende ein.


* * * * *

Abgabe
------


bis 2021-12-10 23:59 UTC, digital in Stud.IP als Markdown-Datei mit dem
Dateinamen `isec21_ueb07_grpYY.(md|zip|tgz)` (das `YY` mit eurer Gruppennummer ersetzen).
Dabei bitte in der Datei die Nummer Eurer Gruppe in Stud.IP sowie alle
an der Abgabe beteiligten Gruppenmitglieder nennen.

Bitte steckt die Energie ins Denken und Schreiben, nicht in eine
wunderschöne Formatierung — lesbar darf es allerdings sein. Die
Lösungswege sollten ggf. nachvollziehbar sein.

Wenn Ihr Euch irgendwelcher Quellen aus dem Netz bedient (Anleitungen,
Howtos, etc), gebt diese bitte als URI mit an.

*Carsten Bormann, Karsten Sohr, Stefanie Gerdes, Jan-Frederik
Rieckers, Hugo Damer ·
<isec@tzi.org>*, WS 2021/22
