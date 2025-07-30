# Ansible System Checker

[Gutes Vide von Network Chuck](https://www.youtube.com/watch?v=OWKPxAgh9DU) \
Congif File
```
/etc/ansible/
```

# Install

Um **Ansible auf Ubuntu** zu installieren, kannst du folgendermaßen vorgehen:

1. **System aktualisieren und benötigte Pakete installieren:**
   ```bash
   sudo apt update
   sudo apt install software-properties-common -y
   ```

2. **Das offizielle Ansible PPA hinzufügen, um die neueste stabile Version zu bekommen:**
   ```bash
   sudo add-apt-repository --yes --update ppa:ansible/ansible
   ```

3. **Paketquellen aktualisieren und Ansible installieren:**
   ```bash
   sudo apt update
   sudo apt install ansible -y
   ```

4. **Installation überprüfen:**
   ```bash
   ansible --version
   ```
   Damit siehst du die installierte Ansible-Version und sicherst, dass die Installation erfolgreich war.

Optional kannst du auch die Bash-Tab-Vervollständigung für Ansible aktivieren:
```bash
sudo apt install python3-argcomplete
sudo activate-global-python-argcomplete3
```

Dieser Weg stellt sicher, dass du eine aktuelle Ansible-Version nutzt, die besser ist als die oft ältere Version der Standard-Paketquellen.

Falls du lieber per Python-Paketmanager `pip` installieren möchtest, ist das auch möglich, jedoch empfiehlt sich für systemweite Installation das PPA.

Diese Anleitung gilt für Ubuntu 20.04, 22.04 und neuer wie 24.04.

Wenn du möchtest, helfe ich dir auch bei der ersten Konfiguration und dem Erstellen eines Inventars für deine Ansible-Nodes.

Quellen: [9][10][11][13]

[1] https://www.youtube.com/watch?v=1LhV87kjHlo
[2] https://www.youtube.com/watch?v=p2a-_L_zNOo
[3] https://www.youtube.com/watch?v=PTqdH_cpN-Y
[4] https://www.youtube.com/watch?v=YbmBMZI3mxA
[5] https://www.youtube.com/watch?v=eVGwNME0C5w
[6] https://www.youtube.com/watch?v=fmavAIzg6rE
[7] https://www.youtube.com/watch?v=Egnsb89T0Rs
[8] https://www.youtube.com/watch?v=5bEAZ0La_Xo
[9] https://www.cherryservers.com/blog/install-ansible-ubuntu-24-04
[10] https://www.centron.de/tutorial/wie-man-ansible-auf-ubuntu-20-04-installiert-und-konfiguriert-schritt-fuer-schritt-anleitung/
[11] https://www.howtoforge.de/anleitung/ansible-unter-ubuntu-22-04-installieren-und-konfigurieren/
[12] https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html
[13] https://wiki.ubuntuusers.de/Ansible/
[14] https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-20-04-de
[15] https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
[16] https://serverspace.io/de/support/help/install-ansible-ubuntu/
[17] https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-22-04
[18] https://labex.io/de/tutorials/ansible-deploying-ansible-on-ubuntu-operating-system-411632
