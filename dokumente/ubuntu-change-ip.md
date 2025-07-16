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
