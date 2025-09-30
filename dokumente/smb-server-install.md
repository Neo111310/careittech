Um einen SMB4 Server (Samba) auf Ubuntu zu installieren, wird das Samba-Paket verwendet, das ab Version 4 standardmäßig SMBv3/SMBv4 unterstützt. Die Installation erfolgt einfach über die Paketverwaltung. Nachfolgend werden die Schritte ausführlich erklärt, inklusive der wichtigsten Konfigurationsoptionen für eine typische Freigabe:[3][4][6]

### Samba installieren

Führe im Terminal folgende Befehle aus, um Samba zu installieren:
```bash
sudo apt update && sudo apt install samba
```
Nach der Installation kannst du mit `smbd --version` die installierte Version überprüfen.[4][6][3]

### Verzeichnisse für Freigaben anlegen

Erzeuge ein öffentliches und ggf. private Verzeichnisse:
```bash
sudo mkdir -p /srv/samba/public
sudo chmod 777 /srv/samba/public
```
Für private Verzeichnisse:
```bash
sudo mkdir -p /srv/samba/private1
sudo chmod 700 /srv/samba/private1
```
Passe die Berechtigungen nach deinen Bedürfnissen an.[1][4]

### Samba-Konfigurationsdatei bearbeiten

Öffne die Konfigurationsdatei:
```bash
sudo nano /etc/samba/smb.conf
```
Am Ende der Datei kannst du einen neuen Abschnitt für dein Verzeichnis hinzufügen:
```
[Public]
path = /srv/samba/public
writable = yes
guest ok = yes
create mask = 0777
directory mask = 0777
```
Für eine private Freigabe ergänze:
```
[Private1]
path = /srv/samba/private1
valid users = benutzername
writable = yes
guest ok = no
create mask = 0700
directory mask = 0700
```
Ersetze "benutzername" mit deinem Ubuntu-Benutzer.[6][3][4]

### Samba-Benutzer anlegen

Falls du Passwortschutz für private Freigaben möchtest, führe aus:
```bash
sudo smbpasswd -a benutzername
```
Dadurch wird ein Samba-Benutzer angelegt.[4]

### Samba-Dienst starten und aktivieren

Starte und aktiviere den Dienst:
```bash
sudo systemctl restart smbd
sudo systemctl enable smbd
```
Damit werden die Änderungen übernommen und Samba wird beim Systemstart automatisch geladen.[4]

### (Optional) Protokollversion im smb.conf einstellen

Ab Samba 4.X wird standardmäßig SMBv3/SMBv4 verwendet, dennoch kannst du das Protokoll explizit setzen:
```
[global]
server min protocol = SMB2
server max protocol = SMB4
```
Dies wird im Bereich `[global]` der smb.conf eingetragen.[6]

### Firewall konfigurieren

Falls die Firewall aktiv ist, schalte die Samba-Ports frei:
```bash
sudo ufw allow Samba
```
Oder für firewalld:
```bash
sudo firewall-cmd --add-service=samba --permanent
sudo firewall-cmd --reload
```


### Verbindung testen

Von einem Windows-PC kannst du im Datei-Explorer folgendes eingeben:
```
\\<Server-IP>\Public
```
Von einem Linux-Client:
```bash
smbclient -L //<Server-IP> -U benutzername
```


### Fazit

Die Installation und Grundkonfiguration eines SMB4/Samba-Servers auf Ubuntu ist mit wenigen Schritten erledigt. Durch die Anpassung der smb.conf kannst du öffentliche oder private Freigaben erstellen und diese mit Benutzerrechten versehen. Die aktuelle Samba-Version auf Ubuntu unterstützt standardmäßig sichere SMB-Protokolle ab Version 3/4 und sollte aus Sicherheitsgründen auch so genutzt werden.[3][6][4]

Für weitere Anpassungen siehe die Ubuntu- und Samba-Dokumentation.[3][6][4]

[1](https://www.reddit.com/r/Ubuntu/comments/1fslvru/i_need_help_to_create_a_samba_server_in_ubuntu/)
[2](https://www.youtube.com/watch?v=clMgaISw_ag)
[3](https://alexhost.com/de/faq/wie-man-samba-unter-ubuntu-installiert/)
[4](https://weber-system.ch/samba-auf-einem-ubuntu-server-installieren/)
[5](https://shape.host/resources/wie-man-samba-auf-ubuntu-22-04-installiert-de)
[6](https://wiki.ubuntuusers.de/Samba_Server/)
[7](https://www.ionos.at/digitalguide/server/konfiguration/samba-server-plattformuebergreifendes-netzwerk/)
[8](https://forum.ubuntuusers.de/topic/samba-fileserver-installieren/)
[9](https://www.youtube.com/watch?v=k3yvG4zDJFQ)
[10](https://ubuntu.com/tutorials/install-and-configure-samba)

# WEb Admin mit cockpit

Installieren
```
sudo apt install cockpit
```
## SMB Addon

Ja, es gibt für Linux Cockpit ein SMB-Plugin. Ein bekanntes Plugin ist das "cockpit-file-sharing" von 45Drives, das sowohl Samba (SMB) als auch NFS Shares über die Cockpit Weboberfläche verwaltet. Damit können Samba-Freigaben komfortabel erstellt, bearbeitet und verwaltet werden, inklusive globaler Einstellungen, Benutzer- und Gruppenmanagement (über ein separates Plugin), sowie spezifischer Optionen wie Windows ACLs, Schattenkopien und mehr. Das Plugin ist sowohl für RHEL-basierte Systeme als auch für Debian/Ubuntu verfügbar.

Zusätzlich existiert ein weiteres SMB-Plugin für Cockpit namens "cockpit-smb-plugin", das Samba-Shares ebenfalls über die Cockpit-Oberfläche verwaltbar macht. Dieses Plugin ist jedoch als etwas roh und experimentell beschrieben.

Die Installation des 45Drives cockpit-file-sharing Plugins erfolgt beispielsweise unter Ubuntu mit:
```bash
curl -sSL https://repo.45drives.com/setup | sudo bash
sudo apt-get install cockpit-file-sharing -y
```
Unter RHEL-basierten Systemen mit dnf kann das RPM direkt installiert werden.

Für das Samba-Management mit Cockpit wird natürlich Samba auf dem System benötigt.

Quellen für weitere Details und Installationsanleitungen:
- Cockpit mit Samba Shares Management (45Drives plugin)
- GitHub repo: enira/cockpit-smb-plugin
- TechRepublic Artikel über Cockpit und Samba Shares[1][2][3]

[1](https://www.techrepublic.com/article/cockpit-creating-samba-shares-simple/)
[2](https://github.com/enira/cockpit-smb-plugin)
[3](https://github.com/45Drives/cockpit-file-sharing)
[4](https://www.reddit.com/r/homelab/comments/fyx94z/best_way_to_manage_samba_shares_linuxmint/)
[5](https://www.reddit.com/r/Proxmox/comments/1gu6xtr/confused_about_cockpit_samba_share_in_an_lxc/)
[6](https://www.reddit.com/r/Proxmox/comments/1fn81gy/cockpit_file_sharing_smb_config_file/)
[7](https://discussion.fedoraproject.org/t/smb-conflicts-using-cockpit-45drives-plugins/82111)
[8](https://docs.openitcockpit.io/development/setup-dev-env/)
[9](https://www.youtube.com/watch?v=l92lp9C2gXg)
[10](https://cockpit-project.org/applications)

