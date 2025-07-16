Um **gelöschte Dateien auf NTFS-Partitionen unter Linux per Live-System wiederherzustellen**, empfiehlt sich die Nutzung folgender Live-Distros und Tools:

**Geeignete Tools und Live-Distributionen:**

- **ntfsundelete**: Dieses Kommandozeilen-Tool ist speziell für das Wiederherstellen gelöschter Dateien auf NTFS-Dateisystemen konzipiert. Es ist Teil des Pakets **ntfsprogs** und in vielen Linux-Distributionen sowie auf zahlreichen Live-Systemen (z. B. Ubuntu Live CD, Knoppix) verfügbar. Damit lassen sich gelöschte Files auf NTFS-Partitionen effektiv scannen und mit guter Chance wiederherstellen – sofern sie noch nicht überschrieben wurden[1][3].
- **Testdisk/PhotoRec**: Das Paket **testdisk** beinhaltet auch das Tool **photorec**, mit dem gelöschte Dateien wiederhergestellt werden können – unabhängig vom Dateisystem, also auch NTFS. Beide Tools sind auf vielen Live-Distributionen wie Knoppix bereits vorinstalliert. Die Nutzung empfiehlt sich besonders, wenn ntfsundelete nicht ausreicht oder kompliziertere Datenverluste vorliegen[9][10].

**Live-Distributionen mit passenden Tools (direkt nutzbar, keine Installation notwendig):**

- **Knoppix**: Sehr gut geeignet, da **ntfsundelete** und **photorec/testdisk** in der Regel bereits vorinstalliert sind[9].
- **Ubuntu Live CD/USB**: Einfach zu starten, alle genannten Tools können direkt aus den Paketquellen nachinstalliert werden. **ntfsundelete** ist oft direkt verfügbar[3].
- **Kali Linux**: Für forensische Zwecke gedacht, mit vielen Datenrettungstools wie photorec und foremost bereits an Bord[7].

**Kurzanleitung mit Ubuntu Live oder Knoppix:**

1. **Mit Live-Distro starten** (Knoppix, Ubuntu Live, etc.).
2. **NTFS-Partition aushängen** (wichtig, um Überschreiben zu vermeiden):
   ```bash
   sudo umount /dev/sdXN
   ```
3. **ntfsundelete oder photorec ausführen**:
   - ntfsundelete (Vorschau und Wiederherstellung):
     ```bash
     sudo ntfsundelete /dev/sdXN --scan
     sudo ntfsundelete /dev/sdXN --undelete --inodes [Nummer]
     ```
   - photorec:
     ```bash
     sudo photorec
     ```
4. **Wiederhergestellte Daten auf separates Medium sichern**.

**Hinweis:** Je weniger nach dem Löschen auf die Partition geschrieben wurde, desto besser stehen die Chancen auf eine erfolgreiche Wiederherstellung. Ein Live-System ist ideal, da das betroffene NTFS-Laufwerk im Lesemodus bleibt und keine weiteren Daten überschrieben werden[1][9].

**Zusammengefasst:**  
Mit Live-Systemen wie **Knoppix** oder **Ubuntu Live** und Tools wie **ntfsundelete** und **photorec** kannst du sehr effektiv gelöschte Dateien auf NTFS-Partitionen retten, ohne die Gefahr eines Überschreibens durch das laufende Betriebssystem[1][3][9].

[1] https://recoverit.wondershare.de/file-recovery/undelete-ntfs-linux.html
[2] https://www.r-studio.com/de/free-linux-recovery/
[3] https://recoverit.wondershare.de/file-recovery/recover-deleted-windows-files-linux.html
[4] https://forum.ubuntuusers.de/post/67573/
[5] https://wiki.ubuntuusers.de/Datenrettung/
[6] https://docs.citrix.com/de-de/linux-virtual-delivery-agent/2212/linux-virtual-delivery-agent-2212.pdf
[7] https://www.centron.de/tutorial/top-20-der-besten-linux-datenwiederherstellungstools/
[8] https://recoverit.wondershare.de/online-audio/adobe-audio-ai-enhancer.html
[9] https://linux-bibel.at/index.php/2023/09/13/geloeschte-partitionen-und-daten-wiederherstellen-mit-testdisk-und-photorec/
[10] https://www.linux-community.de/ausgaben/linuxuser/2010/07/geloeschte-daten-und-laufwerke-rekonstruieren/
