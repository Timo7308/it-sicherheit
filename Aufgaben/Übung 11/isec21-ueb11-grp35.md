# Informationssicherheit, 11. Übung



von Gruppe G35
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

* * *

## Aufgabe 1, 4 Punkte, Gruppe


Needham-Schroeder-Protokoll
---
Das Needham-Schroeder Protokoll wurde 1978 entwickelt. Bei dem Protokoll handelt es sich um ein Schlüsselverteilungsprotokoll. Es benutzt sogenannte Nonces. Dabei handelt es sich um eine Zeichenfolge, die für einen einmaligen Zweck generiert wurde. Im Folgenden wird beschrieben, wie das Protokoll funktioniert. 

Es seien die Personen Alice, Sam und Bob gegeben. Dabei wollen sich Alice und Bob geheim mit einem Sitzungsschlüssel (session key) unterhalten. Dieser Schlüssel soll von Sam bereitgestellt werden. Alice erzählt Sam, dass sie Alice ist und mit Bob reden möchte und ihre Nonce N<sub>A</sub> ist. Sam stellt Alice einen Sitzungsschlüssel zur Verfügung, welcher mit dem Schlüssel, den er mit Alice teilt, verschlüsselt ist. Die geheime Nachricht enthält außerdem die Nonce von Alice, damit sie sichergehen kann, dass es eine Antwort auf ihre Anfrage ist und es sich nicht um einen Replay-Angriff handelt. Sam stellt auch ein für Bob verschlüsseltes Zertifikat zur Verfügung, damit der key an Bob übermittelt werden kann. Alice sendet den key an Bob. Dieser macht nun eine challenge-response Authentisierung, um sicherzugehen, dass es sich auch um Alice handelt. 

Ein Problem im Protokoll liegt darin, dass Bob annehmen muss, dass der key, den er von Sam durch Alice erhält, aktuell ist. Das muss aber nicht so sein. Wenn z.B. ein Gegner Charlie den key von Alice hat, könnte er diesen nutzen, um session keys mit vielen anderen Teilnehmern zu erstellen. 
Alice hätte auch nach einem key fragen können, um mit Dave zu kommunizieren. Wenn Charlie den key gestohlen hätte, hätte er an Sam eine Nachricht senden können, in der er vorgibt, Alice zu sein. Dadurch hätte er dann weitere keys bekommen können. 

Findet Alice heraus, dass ihr key gestohlen wurde, müsste sie Sam darum bitten, jeden zu kontaktieren, mit dem sie einen key ausgetauscht hat. Jeder müsste dann erfahren, dass der alte key von Alice nicht mehr gültig ist. Alice könnte dies nicht selbst tun, da sie nicht alle Kommunikationspartner kennt. Das Widerrufen von keys stellt also ein Problem dar.


Needham-Schroeder-Protokolls mit Zeitstempel
---

 Mit dieser Änderung wird von Sam neben dem Sitzungsschlüssel nun auch ein Zeitstempel mit generiert. Die Verwendung eines alten keys wird somit von Bob im 3.Schritt abgelehnt.
 Nun muss man sich noch zusätzlich um eine gemeinsame synchrone Zeit kümmern und dabei festlegen, ab wann eine key nicht mehr gültig ist, sodass keine abgelaufene keys verwendet werden.

Explizite Nennung der Akteure
---



 In einer Nachricht sollen explizit die Namen der Aktuere genannt werden, um sicher zustellen, dass der generierte key oder die Nonce auch nur für diese Aktuere erstellt wurde. Ein Man-In-The-Middle Attack wird somit verhindert, da in der verschlüsselten Nachricht nun mit angegben wird, von wem diese stammt.
 In 3.2 aus dem Artikel „Programming Satan’s Computer“ von Ross Anderson und Roger Needham wird folgendes Protokoll genannt:
 1. | A → B | {N<sub>A</sub>, A}<sub>K<sub>B</sub></sub>
 1. | B → A | {N<sub>A</sub>, N<sub>B</sub>} <sub>K<sub>A</sub></sub> 
 1. | A → B | { N<sub>B</sub>}<sub>K<sub>B</sub></sub> 
 
 Hier wird vorausgesetzt, dass die Public-Keys den anderen Akteuren schon bekannt ist.
 Im Folgenden besteht für Charlie die Möglichkeit den Man-In-The-Middle zu spielen, indem Charlie (C) vorgibt Alice (A) zu sein, während er mit Bob (B) schreibt, obwohl Bob und Alice direkt kommunizieren wollen.
 
 1. | A → C | {N<sub>A</sub>, A}<sub>K<sub>C</sub></sub>
 1. | C → B | {N<sub>A</sub>, A}<sub>K<sub>B</sub></sub>
 1. | B → C | {N<sub>A</sub>, N<sub>B</sub>} <sub>K<sub>A</sub></sub> 
 1. | C → A | {N<sub>A</sub>, N<sub>B</sub>} <sub>K<sub>A</sub></sub>
 1. | A → C | { N<sub>B</sub>}<sub>K<sub>C</sub></sub>
 1. | C → B | { N<sub>B</sub>}<sub>K<sub>B</sub></sub>
 
 
 In dem Man-In-The-Middle Szenario gelangt Charlie an die Nachricht von Alice im ersten Schritt und benutzt diese, um mit Bob zu kommunizieren. Dazu gibt Charlie sich im zweiten Schritt als Alice aus. Bob weiß nicht, dass statt Alice Charlie mit ihm kommuniziert und sendet in Schritt drei eine Antwort. Diese Antwort erhält erneut Charlie. Um nicht aufzufliegen, sendet er sie an Alice. Denn nur Alice kann die Nonce von Bob entschlüsseln und ihm die Nonce wieder zurückschicken. Alice schickt die Nonce aber an Charlie, da sie gar nicht weiß, dass die Nonce zu Bob gehört.

 Wenn nun bei jeder Nachricht explizit der Akteur genannt wird, kann Charlie sich nicht unbemerkt dazwischenschalten. Im 3. Schritt kann Bob mit explizit seine Identität mit angeben und damit bestätigen, dass die Nonce N<sub>B</sub> von ihm stammt. Wenn dann Charlie im 4. Schritt die Nachricht an Alice weiterleitet, ist in dieser jedoch die Identität von Bob angegeben. Alice bemerkt die Präsenz von Charlie und gibt keine Antwort an diesen, da die Nonce N<sub>B</sub> zu Bob gehört und nicht zu Charlie.
 

Quellen
---
 https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c03.pdf
 
 https://www.cl.cam.ac.uk/~rja14/Papers/satan.pdf
