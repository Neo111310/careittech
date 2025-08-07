Um das **Keyboard-Layout im Linux-Terminal dauerhaft auf Deutsch zu stellen**, gibt es für die überwiegende Mehrheit der Distributionen (z. B. Ubuntu, Debian) zwei empfohlene Wege:

1. **Mit Konfigurationswerkzeug (empfohlen für Konsolen/Terminals außerhalb von X11):**
   - Im Terminal folgenden Befehl eingeben:
     ```
     sudo dpkg-reconfigure keyboard-configuration
     ```
   - Als Tastaturmodell typischerweise „Generische Tastatur mit 105 Tasten (Intl)“ auswählen.
   - Deutsch als Tastaturbelegung festlegen.
   - Die Einstellungen abschließen und den Rechner neu starten oder mit
     ```
     sudo setupcon
     ```
     die Änderung sofort übernehmen.[1][3][4][5][6]

2. **Direkte Änderung der Konfigurationsdatei (auch für Boot/Anmeldung relevant):**
   - Terminal öffnen, dann folgende Datei editieren:
     ```
     sudo nano /etc/default/keyboard
     ```
   - In der Zeile
     ```
     XKBLAYOUT="de"
     ```
     sicherstellen, dass „de“ drinsteht (für deutsches Layout).[8]
   - Optional: ```XKBVARIANT="nodeadkeys"```
   - Datei speichern und schließen.
   - Nach einem Neustart wird diese Einstellung dauerhaft angewendet.

**Hinweise:**
- Die erste Methode eignet sich für Konsolensitzungen und sorgt für eine systemweite, dauerhafte Einstellung.
- Die zweite Methode ist besonders relevant, wenn das Layout schon beim Booten bzw. Login korrekt sein muss.
- Für temporäre Sitzungen (z. B. innerhalb eines XTerm-Fensters) genügt z. B. `setxkbmap de` (nur bis zum Reboot aktiviert).[4]

Falls spezielle Desktop-Umgebungen genutzt werden (z. B. GNOME, KDE), können dort weitere grafische Einstellungen vorgenommen werden, die sich allerdings meistens nur auf die grafische Sitzung auswirken.[4]

**Besonderheit für Arch Linux:** Hier kann das Tool `localectl` verwendet werden:
```
sudo localectl set-keymap de
```

[1] https://praxistipps.chip.de/deutsche-tastatur-in-der-ubuntu-konsole-einrichten_28691
[2] https://www.heise.de/ratgeber/Linux-aendern-der-Tastaturbelegung-303402.html
[3] https://forum.ubuntuusers.de/topic/tastatur-auf-deutsch-einstellen/
[4] https://armann-systems.com/wiki/debian-tastaturlayout-aendern/
[5] https://www.it-administrator.de/article-135653
[6] https://de.ifixit.com/Anleitung/%C3%84nderung+des+Tastaur-Layouts+mit+dem+Terminal+unter+Kali+Linux/150168
[7] https://debiananwenderhandbuch.de/tastaturbelegung.html
[8] https://platform.labdoo.org/content/tastaturlayout-%C3%A4ndern-boot-login
[9] https://www.reddit.com/r/archlinux/comments/17668je/how_can_i_change_the_keyboard_layout/?tl=de
[10] https://www.gutefrage.net/frage/linux-keyboard-layout-lokal-aendern
