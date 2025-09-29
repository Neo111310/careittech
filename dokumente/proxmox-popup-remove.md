## Proxmox remove subscription notice oneliner
## Credit to the original author whoever they are...

Run this command in the proxmox shell..
```
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```
Restart Proxmox just incase.

# Methode 2

Um den „Splashscreen“ bzw. die Lizenzhinweis-Meldung („Sie haben kein gültiges Abonnement für diesen Server“) beim Login in Proxmox VE zu deaktivieren, gibt es einen einfachen Weg, der in der Community vielfach genutzt wird:
 
Kurzanleitung: Lizenzhinweis in Proxmox VE abschalten
	1. Per SSH auf dem Proxmox-Server anmelden
Oder die Shell/Konsole über die Weboberfläche öffnen.
	2. In das Verzeichnis wechseln:

text
cd /usr/share/javascript/proxmox-widget-toolkit
	3. Backup der Datei erstellen:

text
cp proxmoxlib.js proxmoxlib.js.bak
	4. Datei bearbeiten:

text
nano proxmoxlib.js

Suche im Editor nach dem Text

text
Kein gültiges Abonnement

oder nach

text
.data.status.toLowerCase() !== 'active'

und ändere die Zeile so ab, dass das Ausrufezeichen (!) entfernt wird, also:

text
.data.status.toLowerCase() == 'active'
	5. Datei speichern und Editor beenden.
	6. Proxmox Proxy neu starten:

text
systemctl restart pveproxy.service
	7. Weboberfläche neu laden und erneut einloggen.
Damit ist die Lizenzwarnung dauerhaft entfernt – bis zum nächsten Update, bei dem die Datei ggf. überschrieben wird und der Vorgang wiederholt werden muss6108.
 
Automatisierungstipp:
Du kannst dir ein kleines Skript anlegen, das die Änderung automatisch vornimmt, z.B. wie hier beschrieben10:

bash
#!/bin/bash
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
Das Skript als remove-subscription-warning.sh speichern, ausführbar machen (chmod +x remove-subscription-warning.sh) und ausführen.
 
Hinweis:
Diese Methode entfernt lediglich die Lizenzhinweis-Meldung in der Weboberfläche. Einen klassischen „Splashscreen“ im Sinne eines Startbildes gibt es bei Proxmox VE nicht im Zusammenhang mit der Lizenz. Falls du den Boot-Splashscreen von GRUB meinst, kann dieser über die GRUB-Konfiguration angepasst oder entfernt werden5, ist aber unabhängig von der Lizenzmeldung.
 
Rechtlicher Hinweis:
Das Entfernen der Warnmeldung ist technisch möglich und wird von vielen Nutzern genutzt, widerspricht aber ggf. dem Geist der Software, die mit dem Hinweis auf ein kostenpflichtiges Abo auf Support und Updates aufmerksam macht.
	1. https://www.reddit.com/r/kdenlive/comments/1dbk7uc/disable_splash_screen/?tl=de
	2. https://forum.ubuntuusers.de/topic/splash-screen-wird-immer-angezeigt-wie-aendern/
	3. https://forum.proxmox.com/threads/proxmox-auf-notebook-thinkpad-t480-wie-display-zuklappen-ohne-ausschalten.137620/
	4. https://www.reddit.com/r/Proxmox/comments/tdcvx9/turning_off_the_screen_on_a_laptop_running_proxmox/?tl=de
	5. https://c-nergy.be/blog/?p=1794
	6. https://www.reddit.com/r/Proxmox/comments/tgojp1/removing_proxmox_subscription_notice/?tl=de
	7. https://forum.portfolio-performance.info/t/optionale-deaktivierung-des-splash-screens/31705
	8. https://www.youtube.com/watch?v=zuP8xJLaXFk
	9. https://forum.proxmox.com/threads/firewall-deaktivieren.98272/
	10. https://decatec.de/home-server/proxmox-ve-installation-und-grundkonfiguration/
	11. https://forum.proxmox.com/threads/turn-off-proxmox-primary-monitor.120769/

Aus <https://www.perplexity.ai/search/wie-schalte-ich-bei-proxmox-de-JSS0oZW1STyDH2DiUsJ5fg> 

