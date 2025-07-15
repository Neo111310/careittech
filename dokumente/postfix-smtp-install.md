# Postfix auf Ubuntu Installieren und Konfigurieren

Um **Postfix** auf einem Linux-System (zum Beispiel Ubuntu oder Debian) zu installieren, gehen Sie wie folgt vor:

1. **Paketliste aktualisieren:**
   ```sh
   sudo apt update
   ```
2. **Postfix installieren:**
   ```sh
   sudo apt install postfix
   ```
   Während der Installation öffnet sich eine Konfigurationsabfrage im Terminal. Wählen Sie als "Postfix-Konfigurationstyp" in der Regel „Internet Site“ (für normale Mailserver-Nutzung). Als „System-Mail-Name“ geben Sie Ihre Domain (z.B. beispiel.de) ein[1][5][4].

3. **Konfiguration abschließen:**
   Sie können die Standardwerte in den meisten Fällen einfach übernehmen und mit Enter bestätigen. Spätere Änderungen nehmen Sie mit folgendem Befehl vor:
   ```sh
   sudo dpkg-reconfigure postfix
   ```
   oder manuell in der Konfigurationsdatei `/etc/postfix/main.cf`[7][4].

4. **Postfix-Status prüfen:**
   ```sh
   service postfix status
   ```
   Sie sollten sehen, dass der Dienst aktiv ist[4].

Optional, aber empfohlen: Installieren Sie zusätzliche Pakete für Authentifizierung oder die Nutzung aus der Konsole:
```sh
sudo apt install libsasl2-modules bsd-mailx
```
(bsd-mailx ist beispielsweise für den E-Mail-Versand per Kommandozeile praktisch)[3].

Damit ist **Postfix** installiert und einsatzbereit. Für die weitere Konfiguration (TLS, Authentifizierung, virtuelle Domains) empfehlen sich vertiefende Anleitungen, speziell angepasst an Ihre Anforderungen.

[1] https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-postfix-on-ubuntu-20-04-de
[2] https://www.ionos.at/digitalguide/e-mail/e-mail-technik/postfix-mail-server-mit-dovecot-und-squirrelmail-auf-ubuntu/
[3] https://wiki.ubuntuusers.de/Postfix/
[4] https://blog.stueber.de/posts/setup-postfix/
[5] https://linux-bibel.at/index.php/2023/09/10/postfix-der-mailserver-unter-linux/
[6] https://www.thomas-krenn.com/de/wiki/Postfix_unter_Debian_einrichten
[7] https://documentation.ubuntu.com/server/how-to/mail-services/install-postfix/
[8] https://serverspace.io/de/support/help/install-configure-postfix-ubuntu-20-04/
[9] https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-postfix-as-a-send-only-smtp-server-on-ubuntu-18-04-de
[10] https://www.redhat.com/de/blog/install-configure-postfix
