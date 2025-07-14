Einrichten von E-Card Readern und Ärzte Pc's in einem LAN

Auf Jeden Rechner der Zugriff braucht die Statische Route Eintragen (Als Admin)

Route -p add 84.38.112.0 mask 255.255.240.0 <Gateway-IP> METRIC 1

Weitere Infoemationen

Zertifikate von https://www.chipkarte.at/cdscontent/?contentid=10007.897509&portal=ecardportal runterladen und installieren, sonst kann auf die Reader nicht zugegriffen werden.

[Inhalt]

Das Dokument in der Aktuellen Version ist Hier Erhältlich: https://www.chipkarte.at/cdscontent/load?contentid=10008.
765054&version=1646760724

																					
Auszug aus der Dokumentation Seite 35 und Folgende


Beschreibung:

	1. Die Schnittstelle „Zuständigkeit Provider“ ändert sich nicht, der Provider führt auch keine zusätzlichen Konfigurationen am Router aus. (Außer DHCP – ON / OFF und bei Wunsch IP-Adresse des Routers) Siehe auch Abschnitt: 2.3 Zuständigkeiten und Schnittstelle im VP-LAN 
	2. WICHTIG: der erste GINO ist am Router anzuschließen; damit wird auch (üblicherweise) die Abnahme durchgeführt. 
	3. Der GIN-Router empfängt (nur lesend!) RIP2-Updates aus dem VP-LAN. Er sendet aber niemals eigene RIP2-Updates aus. 
	4. Der lokale IT-DL kann nun seinerseits die notwendigen Routen per RIP2 propagieren (seine / die lokalen) und die Routen zum PP als statische Routen in „seinem“ Router konfigurieren. Gegebenenfalls (bei Internet-MWDs) konfiguriert er auch die Default Route zum VP-Router. Siehe auch Anmerkung „Statische Routen“ weiter unten.
	5. Das „Sub-Netzwerk des VP“ wird von der e-card Serviceline und von den Providern nicht supportet (z.B. auch Sub-LAN mittels VPN Verbindung!). 

Um solche Konfigurationen stabil und für alle Router konstant zu implementieren, sind einige Parameter zu beachten bzw. zu konfigurieren, die im folgenden Abschnitt ausgeführt werden.

Statische Routen im „privaten“ Router/FW: 
Die Routen, die vom IT-DL statisch in „seinem“ Router (6) zu konfigurieren sind, beinhalten mindestens folgende Routen: 

• 84.38.112.0/20 (zentrale Services im RZ, PP und EHI, ELGA) 
• 172.16.0.0 bis 172.31.255.255 (= 172.16.0.0/12) PP, MWD, Provider und RZ 
• 79.174.96.0/19 (HEALIX) 
• 193.46.140.0/24 (HEALIX) 
• 193.46.141.0/24 (HEALIX) 
• 193.46.142.0/24 (HEALIX) 
• Um die Nutzung von Internet-MWDs über den PP zu ermöglichen, ist eine "Default-Route" zum GIN-Zugangsnetz Router erforderlich. 

6.3 Technische Randbedingungen und Anforderungen
Die RIPv2-Konfiguration ist konstant, Netze aus 10.0.0.0/9 und 192.168.0.0/16 (oder Sub-Netze davon) werden unterstützt. Wenn RIPv2 unterstützt werden soll, muss das verwendete VP-LAN ein Netz aus den freigegebenen Netzbereichen 10.0.0.0/9 oder 192.168.0.0/16 sein.

RIPv2 im GIN-Router ist als RIPv2-Listener (reader-only) ausgelegt! Es werden nur freigegebene Netze für das VP-LAN gelernt, siehe weiter unten. Der Routing-Table ist auf 200 Routen limitiert. Die RIPv2-Konfiguration ist in jedem Router per Default vorhanden, kann aber bei der Herstellung des e-card Anschlusses auf Wunsch deaktiviert werden.

Freigegebene Netze für das VP-LAN (Arzt): Netzbereich_1: 192.168.0.0 bis 192.168.255.255 Netzbereich_2 10.0.0.0 bis 10.127.255.255 Diese Netze oder Subnetze werden per RIP2 gelernt (wenn die IP-Adresse des Routers in Netzbereich_1 liegt) – alle anderen nicht!

BILD -- BILD

Konfig Zusammenfassung

Erlaubte Quell Netze:
10.0.0.0/9
192.168.0.0/16

Ziel Netze zu Routen über GINS Router

Netzwerk	Subnetmask	Adressbereich	Dienstbeschreibung
84.38.112.0/20	255.255.240.0	84.38.112.1 - 84.38.127.254	(zentrale Services im RZ, PP und EHI, ELGA)
172.16.0.0/12	255.240.0.0	172.16.0.0 - 172.31.255.255	PP, MWD, Provider und RZ
79.174.96.0/19	255.255.224.0	79.174.96.1 - 79.174.127.254	(HEALIX)
193.46.140.0/24	255.255.255.0	193.46.140.1 - 193.46.140.254	(HEALIX)
193.46.141.0/24	255.255.255.0	193.46.141.1 - 193.46.141.254	(HEALIX)
193.46.142.0/24	255.255.255.0	193.46.141.1 - 193.46.141.254	(HEALIX)
Um die Nutzung von Internet-MWDs über den PP zu ermöglichen, ist eine Default-Route zum GIN-Zugangsnetz Router erforderlich.			
193.46.140-143 könnte als CheatCheat verwendet Werden			
193.46.140.0/22	255.255.252.0	193.46.140.1 - 193.46.143.254	(HEALIX)

