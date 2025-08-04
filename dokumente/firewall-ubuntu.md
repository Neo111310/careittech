# SSH HHTP HTTPS ALLOW
Um UFW (Uncomplicated Firewall) unter Ubuntu für SSH, HTTP und HTTPS korrekt zu konfigurieren, führen Sie folgende Befehle als root oder mit sudo im Terminal aus. Damit ermöglichen Sie den Zugriff auf die standardmäßigen Ports 22 (SSH), 80 (HTTP) und 443 (HTTPS):

1. **Standardregeln setzen:**  
   Alles Eingehende blockieren, Ausgehendes zulassen:
   ```
   sudo ufw default deny incoming
   sudo ufw default allow outgoing
   ```
   Diese Grundeinstellung sorgt dafür, dass nur explizit erlaubte Ports von außen erreichbar sind, ausgehende Verbindungen aber standardmäßig möglich bleiben[6][3].

2. **SSH erlauben:**  
   Damit Sie die Serveradministration per SSH nicht verlieren, lassen Sie diesen Dienst zuerst zu:
   ```
   sudo ufw allow ssh
   ```
   Alternativ (explizit für Port 22):
   ```
   sudo ufw allow 22/tcp
   ```
   Für einen abweichenden SSH-Port passen Sie die Portnummer entsprechend an[7][6].

3. **HTTP und HTTPS erlauben:**  
   Webserverdienste werden so erreichbar:
   ```
   sudo ufw allow http
   sudo ufw allow https
   ```
   Alternativ explizit:
   ```
   sudo ufw allow 80/tcp
   sudo ufw allow 443/tcp
   ```
   Beide Varianten sind funktionell identisch[5][4][6][7].

4. **Firewall aktivieren:**  
   Nachdem die gewünschten Ports freigegeben sind, schalten Sie UFW ein:
   ```
   sudo ufw enable
   ```
   Überprüfen Sie den Status und die aktiven Regeln:
   ```
   sudo ufw status verbose
   ```
   So stellen Sie sicher, dass die korrekten Ports wirklich offen sind[6][1][7].

Damit ist Ihr Ubuntu-System so konfiguriert, dass nur SSH sowie Webserver-Zugänge von außen erlaubt sind; alle anderen Ports bleiben blockiert. Sie können natürlich weitere Regeln ergänzen oder mit spezifischen Portnummern/IP-Adressen arbeiten, wenn Sie den Zugriff weiter einschränken möchten[7][1].

**Wichtige Hinweise:**
- Aktivieren Sie die Firewall erst, wenn SSH-Zugriff korrekt freigegeben ist, um einen Ausschluss vom Server zu verhindern[7][3].
- Über die Anwendung von Dienstnamen (`ssh`, `http`, `https`) erkennt UFW automatisch die richtigen Ports anhand von `/etc/services`[3][5].

Diese Konfiguration ist die empfohlene und getestete Standardmethode für Webserver oder VPS unter Ubuntu[6][4][3][7].

[1] https://www.heise.de/tipps-tricks/Ubuntu-Firewall-einrichten-4633959.html
[2] https://www.hedgehogsecurity.co.uk/blog/configuring-ufw-on-ubuntu-for-a-web-server-a-step-by-step-guide
[3] https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04-de
[4] https://hostman.com/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu/
[5] https://www.zenarmor.com/docs/de/netzwerksicherheitstutorials/wie-richtet-man-eine-firewall-mit-ufw-auf-ubuntu-ein
[6] https://www.youstable.com/de/Blog/ufw-unter-Linux-konfigurieren/
[7] https://www.running-cool.de/linux/hackangriffe-abwehr-und-analysewerkzeuge/ufw-firewall-setup-konfiguration.html
[8] https://wiki.ubuntuusers.de/ufw/
[9] https://www.privacy-handbuch.de/handbuch_92.htm
[10] https://www.sim-networks.com/de/kb/ubuntu-config-firewall-ufw-utility
# SSH von Spezifischen IPs
Um SSH-Zugriff auf Ihrem Ubuntu-System mit UFW nur aus einem bestimmten IP-Bereich zu erlauben, verwenden Sie folgende Syntax:

```
sudo ufw allow from  to any port 22
```

Dabei ersetzen Sie `` durch den gewünschten Bereich in CIDR-Notation, z.B. `192.168.1.0/24` für das komplette Subnetz, oder eine einzelne IP wie `203.0.113.4`[1][2][3].

**Beispiele:**
- Nur eine bestimmte IP erlauben:
  ```
  sudo ufw allow from 203.0.113.4 to any port 22
  ```
- Nur aus einem Subnetz (Beispiel: 192.168.1.0 bis 192.168.1.255):
  ```
  sudo ufw allow from 192.168.1.0/24 to any port 22
  ```

Dadurch wird der SSH-Zugriff auf Port 22 ausschließlich aus diesem IP-Bereich gestattet; alle anderen eingehenden Zugriffe auf diesen Port werden blockiert[1][2][3].

**Wichtige Hinweise:**
- Falls Sie andere SSH-Regeln haben (z.B. „sudo ufw allow 22“ oder „sudo ufw allow ssh“), löschen Sie diese vorher, um keine ungewollten Zugriffe zuzulassen:
  ```
  sudo ufw delete allow 22
  ```
- Die gleiche Methode funktioniert auch, wenn Sie SSH auf einem anderen Port nutzen: Ändern Sie einfach die Portnummer[1][2].

Mit diesem Vorgehen sichern Sie SSH optimal gegen ungewollte Zugriffe ab.

[1] https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04-de
[2] https://www.kim.uni-konstanz.de/e-mail-und-internet/it-sicherheit/sicherer-server-it-dienst/linux-fernadministration-mit-pam-und-ssh/einschraenken-von-authentifizierungen/
[3] https://www.youstable.com/de/blog/understand-ufw-on-linux/
[4] https://www.zenarmor.com/docs/de/netzwerksicherheitstutorials/wie-richtet-man-eine-firewall-mit-ufw-auf-ubuntu-ein
[5] https://forum.ubuntuusers.de/topic/ssh-remotezugriff-auf-ein-netz-einschraenken/
[6] https://wiki.ubuntuusers.de/ufw/
[7] https://www.reddit.com/r/oraclecloud/comments/10jfncp/oci_instances_ubuntu_2204_dont_seem_to_respect/?tl=de
[8] https://www.thomas-krenn.com/de/wiki/Absicherung_eines_Debian_Servers
[9] https://www.linux.digibeatrix.com/de/security-and-user-management/ubuntu-ufw-firewall-guide/
[10] https://www.reddit.com/r/linuxadmin/comments/1ax92h3/configuring_ssh_to_only_allow_access_from_1_ip/?tl=de
