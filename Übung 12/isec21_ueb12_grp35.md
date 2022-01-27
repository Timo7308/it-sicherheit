Informationssicherheit, 12. Übung
================================

von Gruppe G35
Adrian Lindloff (lindloff), Timo Schuchmann (timo5) und Philias Borrmann (borrmann)

*******************

**Was kann passieren? / Welche Angriffsvektoren gibt es?**

Das erste Problem besteht darin, dass der DSL-Router das Verschlüsselungsprotokoll Wired Equivalent Privacy (WEP) verwendet. Das WEP-Protokoll verwendet eine 40-Bit-RC4 Verschlüsselung. Diese Schlüssellänge ist viel zu kurz und ermöglicht Brute Force-Angriffe auf den DSL-Router. Der verwendete Schlüssel ist außerdem statisch. Das heißt, es wird immer der gleiche Schlüssel verwendet. Dies sorgt ebenfalls für eine geringere Sicherheit. WEP bietet außerdem keinen Schutz vor Bit flipping Angriffen, Replay Angriffen und FMS-Angriffen. WEP gilt heute als gebrochen und sollte unter keinen Umständen mehr verwendet werden. 

Auch wenn man der "erste Gast" ist, muss davon ausgegangen werden, dass sich weitere Teilnehmer im Netzwerk des Biergartens befinden. Alle diese Teilnehmer können miteinander interagieren und sich gegenseitig hacken. Selbst für Laien ist es mithilfe von einer Reihe von Tools möglich, Schwachstellen an dem verbundenen Gerät zu identifizieren sowie diese potenziell auszunutzen. Dies gilt selbstverständlich auch für Konkurrenten und feindselige Parteien, welche im schlimmsten Fall Zugang zu internen Firmendaten erlangen.



---

**Welche Sicherheitsziele werden verletzt?**

Zu den verletzten Sicherheitszielen zählt zum einen die Vertraulichkeit. Aufgrund unzureichender Sicherheit des DSL-Routers kann kein Schutz von persönlichen Informationen gewährleistet werden. Es wird außerdem das Sicherheitsziel der Integrität verletzt. Aufgrund der Verwendung von WEP kann es passieren, das unautorisiert auf persönliche Daten zugegriffen wird. Schließlich wird das Sicherheitsziel Verfügbarkeit verletzt. Durch Angriffe von außen ist kein Schutz vor Beeinträchtigung der Funktionalität von Komponenten und Diensten gewährleistet. 

---

**Sollte man so wie in der Aufgabe beschrieben online gehen?**

Es ist nicht ratsam in einem öffentlichen WLAN mit vertraulichen/persönlichen Informationen zu arbeiten. Es besteht die Gefahr eines unbefugten Zugriffs. Möchte man sich hingegen nur über das Wetter oder die neusten Nachrichten informieren, sollte dies kein Problem sein. Hinzu kommt in diesem Fall noch, dass der Gastwirt noch nicht einmal SSID aussprechen kann, geschweige denn dessen Nutzen kennt. Der Praktikant hat höchstwahrscheinlich die volle und alleinige Kontrolle über den Router und somit auch den Datenverkehr ohne das ihn jemand kontrolliert.

---

**Was sind mögliche Sicherheitsmaßnahmen?**


Eine mögliche Sicherheitsmaßnahme wäre die Verwendung eines Virtual Private Networks (VPN). Dadurch läuft der eigene Datenverkehr verschlüsselt über einen VPN-Server. Angreifer sind so nicht mehr in der Lage zu sehen, mit welchen Daten man arbeitet oder welche Webseiten man besucht. 
Der VPN-Anbieter sollte eine gute Reputation besitzen und (so blöd es auch klingt) Geld kosten. Der Anbieter kann nämlich den (nicht verschlüsselten) Datenverkehr sehen, weswegen die User höchst wahrscheinlich mit ihren eigenen Daten "bezahlen".
Es ist außerdem sinnvoll nur verschlüsselte "Nachrichten" zu übermitteln, da alles andere abgefangen und verwendet werden kann. Bei den zu besuchenden Webseiten sollte auch darauf geachtet werden das diese verschlüsselt sind (https). Persönliche Daten sind sonst nicht sicher. 
Die im Biergarten verwendeten Geräte sollten auf dem aktuellsten Stand sein (für iPhones bspw. neuste iOS Version) und eine Firewall aktiviert haben.
Für den nächsten Besuch ist es sinnvoll die LTE-Karte mitzunehmen.
Ein mobiler Hotspot wäre eine weitere Möglichkeit ein öffentliches Wi-Fi zu umgehen, da dessen Verbindung mit dem Gerät im Normalfall verschlüsselt ist. 

* * *
