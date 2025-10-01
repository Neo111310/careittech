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

# Mehrere Zertifikate gleichzeitig

Um mit zwei oder mehreren SSH-Schlüsseln auf einem Rechner zu arbeiten, nutzt man die SSH-Konfigurationsdatei, die unter ~/.ssh/config liegt. Dort kann man für jeden Server oder Dienst eine eigene Sektion anlegen und den passenden privaten Schlüssel angeben.

### Einfach erklärt:

1. Erstelle für jeden SSH-Schlüssel (z.B. für verschiedene Server oder Git-Konten) ein eigenes Schlüsselpaar mit ssh-keygen.
2. Speichere die Schlüssel unter unterschiedlichen Namen in deinem ~/.ssh Verzeichnis.
3. Erstelle oder bearbeite die Datei ~/.ssh/config und füge für jeden Host (Server/Service) eine Konfiguration hinzu, z.B.:

```
Host server1
  HostName server1.example.com
  User benutzername
  IdentityFile ~/.ssh/id_rsa_server1

Host gitlab
  HostName gitlab.com
  User git
  IdentityFile ~/.ssh/id_rsa_gitlab
```

4. Beim Verbinden mit `ssh server1` oder beim Klonen eines Git-Repos benutzt SSH automatisch den zugewiesenen Schlüssel.
5. Du kannst auch einen SSH-Agenten (ssh-agent) nutzen, um deine Schlüssel zu laden und nicht jedes Mal das Passwort eingeben zu müssen.

So kannst du bequem mit mehreren Schlüsseln auf einem Rechner arbeiten, ohne ständig manuell den Schlüssel wechseln zu müssen.[1][3][4]

[1](https://mobile.fhstp.ac.at/allgemein/ssh-schluessel-gitlab/)
[2](https://www.reddit.com/r/hetzner/comments/sq7ikt/adding_second_ssh_key_to_cloud_server_possible/)
[3](https://www.hosting.de/helpdesk/anleitungen/server/openssh_server/)
[4](https://www.ionos.at/digitalguide/server/sicherheit/ssh-keys-fuer-ihre-netzwerkverbindung-nutzen/)
[5](https://www.reddit.com/r/linuxquestions/comments/hlyp4v/is_it_bad_to_use_the_same_ssh_key_on_multiple/)
[6](https://www.computerbase.de/forum/threads/ssh-mehrere-schluesselpaare.1065827/)
[7](https://forum.linuxguides.de/index.php?thread%2F7167-mehrere-ssh-key-s-nutzen%2F)
[8](https://forum.netcup.de/administration-eines-server-vserver/vserver-server-kvm-server/10110-umgang-mit-ssh-keys-und-passw%C3%B6rtern-bei-mehreren-servern/)
[9](https://docs.github.com/de/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
