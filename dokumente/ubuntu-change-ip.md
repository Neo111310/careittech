# Netplan Doku
[Netplan Doku](https://wiki.ubuntuusers.de/Netplan/)ß
Weitere Infos\
**Beispiel: statische Netzwerkkonfiguration**
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp1s0:
      addresses:
        - 10.10.10.2/24
        - 2001:DB8::5/64
      dhcp4: no
      routes:
        - to: 0.0.0.0/0 #Standardroute für IPv4
          via: 10.10.10.1
        - to: ::/0 #Standardroute für IPv6
          via: 2001:DB8::1
      nameservers:
        addresses: [10.10.10.1, 1.1.1.1, 2001:470:20::2]
```
# Netzwerk Devices Auflisten
Unter Ubuntu (und allgemein Linux) können Sie alle verfügbaren Netzwerkgeräte mit folgenden Befehlen im Terminal anzeigen:

- `ip link show`  
  Zeigt alle Netzwerkinterfaces (Netzwerkgeräte) mit ihrem Status an.

- `ip a` (oder `ip addr`)  
  Zeigt alle Netzwerkgeräte inklusive deren IP-Adressen.

- `cat /proc/net/dev`  
  Listet alle Geräte und deren Netzwerkstatistiken auf.

- `ifconfig -a` (muss eventuell installiert werden mit `sudo apt install net-tools`)  
  Listet alle Netzwerkinterfaces inklusive inaktiver.

- `nmcli device`  
  Zeigt Netzwerkgeräte und deren Verbindungsstatus (NetworkManager muss installiert sein).

Beispiel für schnelle Übersicht:

```bash
ip link show
```

Dies gibt alle Netzwerk-Schnittstellen mit Namen, Status (UP/DOWN) und anderen Basisinfos aus[1][2][3][7].

[1] https://www.veuhoff.net/linux-netzwerkkarten-anzeigen-terminal/
[2] https://www.sammsoft.ch/2021/12/netzwerk-einstellungen-unter-linux-ubuntu-anzeigen/
[3] https://gnulinux.ch/netzwerkgeraete-analysieren
[4] https://www.elektronik-kompendium.de/sites/net/1910051.htm
[5] https://www.ionos.at/digitalguide/hosting/hosting-technik/linux-ip-adresse-anzeigen/
[6] https://www.computerweekly.com/de/tipp/Sechs-nuetzliche-Linux-Befehle-zum-Checken-der-Netzwerkverbindung
[7] https://wiki.ubuntuusers.de/interfaces/
[8] https://wiki.ubuntuusers.de/Shell/Befehls%C3%BCbersicht/
# Netplan Config
Um die **IP-Adresse auf einem Ubuntu Server im Terminal** zu ändern (insbesondere ab Version 18.04 und neuer mit Netplan), gehen Sie wie folgt vor:

1. **Netzwerk-Interface erkennen**

   Führen Sie aus:
   ```bash
   ip a
   ```
   Merken Sie sich den Namen der Netzwerkkarte, z.B. ens160, eth0 oder enp0s3[3][5].

2. **Netplan-Konfigurationsdatei editieren**

   Die Konfigurationsdateien finden Sie im Verzeichnis `/etc/netplan/`. Öffnen Sie die passende Datei (z.B. 00-installer-config.yaml) mit einem Editor:
   ```bash
   sudo nano /etc/netplan/00-installer-config.yaml
   ```
   Passen Sie die Datei wie folgt an (ersetzen Sie die Beispieldaten durch Ihre Werte und achten Sie auf korrekte Einrückungen!):

   ```yaml
   network:
     version: 2
     ethernets:
       ens160:  # <- Name des Interfaces!
         dhcp4: no
         addresses: [10.1.111.71/24]
         gateway4: 10.1.111.250
         nameservers:
           addresses: [10.1.110.1,10.1.110.2]
   ```


3. **Dateirechte setzen (optional, aber empfohlen)**
   ```bash
   sudo chmod 600 /etc/netplan/00-installer-config.yaml
   ```


4. **Neue Netzwerkkonfiguration anwenden**

   ```bash
   sudo netplan apply
   ```
   Achtung: Wenn Sie über SSH verbunden sind, verlieren Sie bei Änderung der IP die Verbindung![3][6][7]

5. **Überprüfen**

   Mit
   ```bash
   ip a
   ```
   kontrollieren Sie, ob die neue **IP-Adresse** gesetzt wurde[3][6].

**Hinweise:**
- Für ältere Ubuntu-Versionen (vor 18.04) wird meist `/etc/network/interfaces` genutzt[1][5].
- Für temporäre Änderungen (bis zum nächsten Neustart): 
   ```bash
   sudo ip addr add 192.168.1.123/24 dev ens160
   sudo ip route add default via 192.168.1.1
   ```
   Diese Methode wird jedoch nach einem Neustart verworfen[5].

**Empfohlen wird immer die Konfiguration über Netplan**, um dauerhafte Änderungen zu erzielen.

[1] https://www.ionos.de/hilfe/server-cloud-infrastructure/dedicated-server-die-vor-dem-281018-erworben-wurden-und-server-power-deals/netzwerk/ipv4-adresse-auf-dedicated-server-linux-aendern-oder-hinzufuegen/
[2] https://www.rz.uni-kiel.de/de/tipps/ip-adressen-und-dns-server-aendern/linux
[3] https://troublenet.de/ubuntu-server-lts-22-04-feste-ip-zuweisen/
[4] https://schaemicon.de/wiki/ubuntu-server-20-04-lts-statische-ip-adresse-konfigurieren/
[5] https://www.itslot.de/2014/02/ubuntu-ip-adresse-per-konsole-andern.html
[6] https://armann-systems.com/wiki/ip-adresse-in-ubuntu-linux-konfigurieren/
[7] https://it-learner.de/how-to-ip-adresse-am-linux-ubuntu-server-andern/
[8] https://wiki.ubuntuusers.de/IP-Adresse_wechseln/
[9] https://linux-bibel.at/index.php/2023/09/10/statische-ip-adresse-unter-ubuntu-ohne-grafische-oberflaeche-einrichten/
[10] https://serverspace.io/de/support/help/how-to-configure-static-ip-address-on-ubuntu-18-04/

# Netplan Syntax
Die Syntax der Datei **netplan/00-installer-config.yaml** folgt dem YAML-Format und wird verwendet, um Netzwerkkonfigurationen auf Ubuntu-Systemen (ab 17.10) und anderen, die Netplan einsetzen, zu definieren. Sie definiert Netzwerk-Interfaces, deren IP-Adressen, Gateways, DNS-Server usw.

Ein grundlegendes Beispiel für die **00-installer-config.yaml** könnte so aussehen:

```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: true               # Für IPv4 DHCP aktivieren
      dhcp6: false              # IPv6 DHCP deaktivieren (optional)
    eth1:
      addresses:
        - 192.168.1.50/24      # Statische IP-Adresse mit Subnetzmaske
      gateway4: 192.168.1.1    # Gateway für IPv4
      nameservers:
        addresses:
          - 8.8.8.8            # DNS-Server
          - 8.8.4.4
```

**Wichtige Punkte:**

- `network` ist die oberste Ebene.
- `version: 2` ist die Netplan-Spezifikation.
- Unter `ethernets` werden Ethernet-Interfaces definiert (z.B. eth0, enp3s0, etc.).
- Optionen bei einem Interface:
  - `dhcp4: true/false` aktiviert/deaktiviert DHCP für IPv4.
  - `addresses:` Liste mit statischen IP-Adressen (CIDR-Notation).
  - `gateway4:` IPv4 Gateway.
  - `nameservers:` DNS-Server-Konfiguration, meist als Liste `addresses:`.
- Für WLAN oder andere Geräte gibt es entsprechend `wifis` oder `bridges` Sektionen.

**Tipp:** Nach dem Ändern der Datei immer mit folgendem Befehl die Konfiguration testen und anwenden:

```bash
sudo netplan try    # Testet die Konfiguration temporär
sudo netplan apply  # Wendet die Konfiguration dauerhaft an
```

Weitere Details finden Sie in der offiziellen Netplan-Dokumentation und in Ubuntu-Blogs/Community-Wikis.
