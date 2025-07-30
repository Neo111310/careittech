# CopyParty Fileserver

Um **copyparty** auf Ubuntu als Service zu installieren und zu betreiben, kannst du folgende Schritte durchführen:

1. **Systemvoraussetzungen installieren:**
   Stelle sicher, dass Python 3, pip, OpenSSL und Git installiert sind:
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip python3-openssl git
   ```

2. **copyparty Repository klonen:**
   ```bash
   git clone https://github.com/9001/copyparty.git
   cd copyparty
   ```

3. **copyparty mit pip installieren:**
   (Im kopierten Verzeichnis)
   ```bash
   sudo pip3 install --no-cache-dir --user .
   ```

4. **copyparty testen:**
   Starte copyparty manuell, um sicherzugehen, dass es läuft:
   ```bash
   copyparty
   ```
   Standardmäßig ist es unter `http://localhost:3923/` erreichbar.

5. **Systemd Service Datei erstellen:**
   Erstelle eine Service-Datei, z.B. `/etc/systemd/system/copyparty.service` mit folgendem Inhalt (angepasst auf deinen Installationspfad):
   ```ini
   [Unit]
   Description=copyparty file server
   After=network.target

   [Service]
   User=
   ExecStart=/usr/bin/copyparty --no-auth
   Restart=on-failure
   WorkingDirectory=/home//copyparty

   [Install]
   WantedBy=multi-user.target
   ```
   Ersetze `` mit deinem tatsächlichen Benutzernamen und passe den Pfad ggf. an, wenn du copyparty anders installiert hast.

6. **Service neu laden und starten:**
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable copyparty.service
   sudo systemctl start copyparty.service
   ```

7. **Status überprüfen:**
   ```bash
   sudo systemctl status copyparty.service
   ```

Mit diesem Setup läuft copyparty als Hintergrunddienst (Service) auf deinem Ubuntu-System und startet beim Boot automatisch.

Falls du zusätzliche Konfigurationsoptionen für copyparty brauchst, kannst du diese in der `ExecStart`-Zeile ergänzen, z.B. Ports ändern oder Authentifizierung aktivieren.

Diese Anleitung basiert auf der offiziellen GitHub-Installation mit Python und pip sowie üblichen Linux-Systemd-Service-Methoden[8][14]. Wenn du möchtest, kann ich dir auch helfen, den Service mit speziellen Optionen oder für andere Benutzerkonten einzurichten.

[1] https://github.com/9001/copyparty
[2] https://www.youtube.com/watch?v=VB68aY71bTI
[3] https://www.youtube.com/watch?v=yKNp1VnjGVI
[4] https://www.youtube.com/watch?v=Ms2gz6Cl6qo
[5] https://www.youtube.com/watch?v=MpMhTb0-hDM
[6] https://www.youtube.com/watch?v=Vt_Wd_tYFco
[7] https://www.youtube.com/watch?v=_ChTxdxrlhc
[8] https://www.youtube.com/watch?v=qGPciLwCKVk
[9] https://ipv6.rs/tutorial/Ubuntu_Server_Latest/copyparty/
[10] https://ipv6.rs/tutorial/Arch_Linux/copyparty/
[11] https://www.youtube.com/watch?v=Foqs70mT2yc
[12] https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04-de
[13] https://github.com/DanielPalaio/Ubuntu_Setup
[14] https://www.youtube.com/watch?v=aq6zoi1DPVg
[15] https://askubuntu.com/questions/1450781/how-to-install-an-application-from-github
[16] https://www.reddit.com/r/selfhosted/comments/1m9roco/introducing_copyparty_the_foss_file_server/
[17] https://szmer.info/post/8706885
