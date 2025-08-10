Um einen **Git Server unter Ubuntu** zu installieren, gehen Sie wie folgt vor:

1. **Git installieren**:
   ```
   sudo apt update
   sudo apt install git
   ```
   Damit wird Git auf Ihrem System installiert.[1][2][3][4]

2. **Eigenen Benutzer für Git anlegen** (Sicherheitsmaßnahme):
   ```
   sudo adduser git
   ```
   Ein separater Nutzer isoliert den Zugriff auf die Repository-Daten und erleichtert die Verwaltung.[1]

3. **Verzeichnis für Repositories anlegen**:
   ```
   sudo mkdir /usr/local/git
   sudo chown git:git /usr/local/git
   ```
   Dieses Verzeichnis dient als Speicherort für alle Git-Repositories.[1]

4. **Zu Git-Benutzer wechseln**:
   ```
   su -l git
   ```

5. **Repository anlegen (als „bare repository“)**:
   ```
   cd /usr/local/git
   git init --bare meinprojekt.git
   ```
   „Bare“-Repositories sind ohne Arbeitsverzeichnis und für Server zentral, an die mehrere Entwickler pushen können.[1]

6. **SSH-Zugang einrichten**:
   Die Zusammenarbeit erfolgt typischerweise per SSH. Dazu kann der git-Nutzer z. B. öffentliche SSH-Keys in `~/.ssh/authorized_keys` hinterlegen oder Sie passen die Datei `/etc/ssh/sshd_config` an, um den Zugriff zu erlauben und starten SSH neu:
   ```
   sudo service ssh restart
   ```
   Danach kann geklont werden:
   ```
   git clone git@:/usr/local/git/meinprojekt.git
   ```


Damit ist ein einfacher Git-Server installiert und bereit. Optional können Sie Projekte wie **Gitea** nutzen, um eine komfortable Web-Oberfläche und weitere Verwaltungsfunktionen zu ermöglichen. Für mehr Sicherheit sollten Firewalleinstellungen und regelmäßige Backups bedacht werden.[1]

[1] https://www.geeksforgeeks.org/git/how-to-setup-git-server-on-ubuntu/
[2] https://wiki.ubuntuusers.de/Git/
[3] https://www.ionos.de/digitalguide/server/konfiguration/git-auf-ubuntu-2204-installieren/
[4] https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04-de
[5] https://www.centron.de/tutorial/git-auf-ubuntu-24-04-installieren-und-konfigurieren-schritt-fuer-schritt-anleitung/
[6] https://git-scm.com/book/de/v2/Git-auf-dem-Server-Einrichten-des-Servers
[7] https://www.ovhcloud.com/de/community/tutorials/how-to-install-git-ubuntu/
[8] https://git-scm.com/book/de/v2/Erste-Schritte-Git-installieren
[9] https://git-scm.com/book/de/v2/Git-auf-dem-Server-Git-auf-einem-Server-einrichten
[10] https://www.thomas-krenn.com/de/wiki/Git_Server-Konfiguration
