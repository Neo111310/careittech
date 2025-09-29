Um eine HDD unter Ubuntu Server zu partitionieren, zu formatieren und dauerhaft ins System zu mounten, können folgende Schritte im Terminal ausgeführt werden:

### 1. Festplatte erkennen
Mit dem Befehl
```bash
sudo fdisk -l
```
werden alle angeschlossenen Laufwerke angezeigt. Die entsprechende Festplatte (z.B. /dev/sdb) identifizieren.

### 2. Partitionierung mit fdisk
```bash
sudo fdisk /dev/sdb
```
- Mit `n` eine neue Partition erstellen
- Partitionstyp wählen (normalerweise Primär `p`)
- Partitionsnummer (meist 1)
- Start- und Endsektor bestätigen oder Größe angeben (z.B. +100G)
- Mit `w` die Partitionstabelle speichern und fdisk verlassen

### 3. Partition formatieren
Beispiel für ext4-Dateisystem:
```bash
sudo mkfs.ext4 /dev/sdb1
```

### 4. Einhängepunkt erstellen
```bash
sudo mkdir /mnt/meineplatte
```

### 5. Temporär mounten
```bash
sudo mount /dev/sdb1 /mnt/meineplatte
```

### 6. Dauerhaft mounten (fstab)
UUID der Partition ermitteln:
```bash
sudo blkid /dev/sdb1
```
Ausgabe enthält etwas wie:
```
UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```
Diese UUID in der Datei `/etc/fstab` eintragen:
```bash
sudo nano /etc/fstab
```
Eintrag hinzufügen, z.B.:
```
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt/meineplatte ext4 defaults 0 2
```

### 7. Testen ob fstab korrekt ist
```bash
sudo mount -a
```
Keine Fehlermeldung bedeutet, dass die Partition dauerhaft beim Systemstart gemountet wird.

Diese Schritte ermöglichen die Partitionierung, Formatierung und den permanenten Einhängepunkt der HDD im Ubuntu Server System.[1][2][5]

[1](https://gcore.com/de/learning/how-to-partition-a-disk-in-linux)
[2](https://www.mynewsdesk.com/de/easeus/pressreleases/fixed-ubuntu-format-disk-wie-man-eine-festplatte-unter-ubuntu-formatiert-3315742)
[3](https://www.heise.de/tipps-tricks/Ubuntu-Festplatte-formatieren-4172528.html)
[4](https://recoverit.wondershare.de/harddrive-tips/format-and-wipe-linux-disk.html)
[5](https://u-labs.de/portal/neue-festplatte-partitionieren-und-formatieren-unter-ubuntu-server/)
[6](https://wiki.ubuntuusers.de/Partitionierung/)
[7](https://www.thomas-krenn.com/de/wiki/Festplatte_formatieren_/_partitionieren_und_mounten_unter_Debian_Linux)
[8](https://wiki.ubuntuusers.de/Formatieren/)
[9](https://www.easeus.de/partitionieren-tipps/linux-partition-formatieren.html)
[10](https://www.centron.de/tutorial/linux-partitionierung-leicht-gemacht-ein-einfaches-tutorial/)
