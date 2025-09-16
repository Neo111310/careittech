Um ein **ISO-Image mit dd auf einen USB-Stick** unter Linux zu schreiben, kann der folgende Befehl verwendet werden:

```bash
sudo dd if=/pfad/zur/datei.iso of=/dev/sdX bs=4M status=progress && sync
```
Dabei gilt:

- `if=` ist der Pfad zur ISO-Datei.
- `of=` ist das Gerät des USB-Sticks (z.B. `/dev/sdb`, beachten: niemals eine Partitionsnummer wie `/dev/sdb1` nehmen, sondern das komplette Gerät!).
- `bs=4M` oder `bs=1M` steht für die Blockgröße (4M ist oft schneller, 1M funktioniert immer).
- `status=progress` zeigt den Fortschritt an.
- `sync` stellt sicher, dass alle Daten wirklich geschrieben werden.[1][2][3][5][8]

### Hinweise zur Anwendung

- Den **richtigen Gerätenamen** ermitteln mit `lsblk` oder `fdisk -l`, damit keine falsche Festplatte überschrieben wird.[3][4]
- Stick vor dem Schreiben aushängen: `umount /dev/sdX*` (wobei `X` der Buchstabe des USB-Sticks ist).[2][3]
- Nach Abschluss ist der Stick bootfähig und kann verwendet werden.[5][1]

### Wichtige Warnhinweise

- **Achtung:** Der Vorgang löscht unwiderruflich alle Daten auf dem USB-Stick! Unbedingt prüfen, dass mit `of=` das korrekte Gerät angegeben ist.
- Keine Partitionsnummer (wie `/dev/sdb1`), sondern das Gerät selbst (z.B. `/dev/sdb`) verwenden.[2][3][5]

### Beispiel

```bash
sudo dd if=ubuntu-24.04-desktop-amd64.iso of=/dev/sdb bs=4M status=progress && sync
```

So lässt sich unter Linux einfach und sicher ein ISO-Image auf einen USB-Stick schreiben – vorausgesetzt, der Gerätename ist korrekt bestimmt worden.[3][5]

[1](https://help.it-nerd24.de/hc/de/articles/17873171548177-Erstellen-eines-bootf%C3%A4higen-USB-Sticks-unter-Linux)
[2](https://yourdevice.ch/iso-dateien-mit-dd-flashen-auf-linux/)
[3](https://techjunkies.blog/digital-life/ubuntu-vom-usb-stick-installieren/)
[4](https://linuxundich.de/gnu-linux/iso-images-mit-gnome-disks-auf-usb-sticks-schreiben/)
[5](https://www.cyberciti.biz/faq/creating-a-bootable-ubuntu-usb-stick-on-a-debian-linux/)
[6](https://www.reddit.com/r/Ubuntu/comments/1ijdx0f/how_to_create_a_iso_on_a_usbstick/)
[7](https://www.mikrocontroller.net/topic/566093)
[8](https://forum.ubuntuusers.de/topic/mit-dd-ein-iso-image-auf-usb-stick-erstellen/)
[9](https://www.opensuse-forum.de/thread/66093-linux-bootstick-erstellen-mit-dd/)
[10](https://linux-bibel.at/index.php/2023/09/17/iso-images-mit-dem-befehl-dd-unter-linux-auf-einen-usb-stick-kopieren/)
