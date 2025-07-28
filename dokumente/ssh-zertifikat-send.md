# SSH auf Remote Server senden
Um ein SSH-Zertifikat (genauer: ein SSH-Schlüsselpaar) auf einem Remote-Server zu installieren, sind folgende Schritte üblich:

1. **SSH-Schlüsselpaar lokal erzeugen** (falls noch nicht vorhanden):  
   Im Terminal lokal ausführen:
   ```
   ssh-keygen
   ```
   Dabei werden zwei Dateien erzeugt: der private Schlüssel (z.B. `id_rsa`) und der öffentliche Schlüssel (z.B. `id_rsa.pub`) im Verzeichnis `~/.ssh/`.

2. **Öffentlichen Schlüssel auf den Remote-Server kopieren:**  
   Der einfachste Weg ist `ssh-copy-id` zu verwenden:
   ```
   ssh-copy-id -i ~/.ssh/id_rsa.pub user@remote-server
   ```
   Dabei wird der öffentliche Schlüssel in die Datei `~/.ssh/authorized_keys` des Zielbenutzers auf dem Server eingefügt.

   Falls `ssh-copy-id` nicht verfügbar ist, kannst du es auch manuell machen:
   - Öffentliche Schlüsseldatei lokal anzeigen:
     ```
     cat ~/.ssh/id_rsa.pub
     ```
   - Auf dem Server anmelden (mit Passwort):
     ```
     ssh user@remote-server
     ```
   - Sicherstellen, dass das Verzeichnis `.ssh` im Home-Verzeichnis existiert:
     ```
     mkdir -p ~/.ssh
     chmod 700 ~/.ssh
     ```
   - Public Key zum Autorisierungsspeicher hinzufügen:
     ```
     echo "DER_INHALT_VON_id_rsa.pub" >> ~/.ssh/authorized_keys
     chmod 600 ~/.ssh/authorized_keys
     ```
   (Dabei ersetzt du `"DER_INHALT_VON_id_rsa.pub"` durch den kopierten Text aus der öffentlichen Schlüsseldatei.)

3. **Test der SSH-Verbindung per Schlüssel:**  
   Nun sollte folgendes ohne Passwort funktionieren:
   ```
   ssh user@remote-server
   ```

4. **Wichtig:**  
   - Die Dateiberechtigungen (`~/.ssh` auf `700`, `authorized_keys` auf `600`) müssen korrekt gesetzt sein, sonst verweigert SSH die Schlüsselauthentifizierung.  
   - Der private Schlüssel bleibt auf deinem lokalen Rechner und wird niemals auf den Server kopiert.

Diese Methode ermöglicht dir eine passwortlose, sichere Anmeldung via SSH durch den zuvor installierten öffentlichen Schlüssel auf dem Remote-Server[9][12][13][14][11].

Falls du weitere Details oder Hilfe bei der Einrichtung auf Windows oder anderen Systemen brauchst, kann ich das gerne erläutern.

[1] https://www.youtube.com/watch?v=c6yGF0bjQLY
[2] https://www.youtube.com/watch?v=K1pZEf6r06o
[3] https://www.youtube.com/watch?v=Py4Gtp8fj1k
[4] https://www.youtube.com/watch?v=U_uiVyF6MEs
[5] https://www.youtube.com/watch?v=9dhQIa8fAXU
[6] https://www.youtube.com/watch?v=Kjc0pzR2eeU
[7] https://www.youtube.com/watch?v=3TiDwy2oSVI
[8] https://www.youtube.com/watch?v=Bd5rdLzb5GM
[9] https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server-de
[10] https://www.ionos.at/digitalguide/server/konfiguration/ubuntu-ssh/
[11] https://learn.microsoft.com/de-de/windows-server/administration/openssh/openssh_keymanagement
[12] https://www.thomas-krenn.com/de/wiki/OpenSSH_Public_Key_Authentifizierung_unter_Ubuntu
[13] https://www.ionos.at/digitalguide/server/sicherheit/ssh-keys-fuer-ihre-netzwerkverbindung-nutzen/
[14] https://www.cyberciti.biz/faq/install-ssh-identity-key-remote-host/
[15] https://cloud.ibm.com/docs/ssh-keys?topic=ssh-keys-generating-and-using-ssh-keys-for-remote-host-authentication&locale=de
[16] https://wiki.ubuntuusers.de/SSH/
[17] https://gridscale.io/community/tutorials/per-ssh-mit-cloud-server-verbinden/
[18] https://community.hetzner.com/tutorials/howto-ssh-key/de/
