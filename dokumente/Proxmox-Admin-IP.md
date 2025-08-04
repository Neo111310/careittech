Um die Admin-IP-Adresse (Management-IP) bei Proxmox zu ändern, gehst du folgendermaßen vor:

1. Melde dich direkt am Proxmox-Server an oder per SSH.
2. Öffne die Netzwerkkonfigurationsdatei mit einem Editor, zum Beispiel:
   ```
   nano /etc/network/interfaces
   ```
3. Suche den Abschnitt, der die aktuelle IP-Adresse enthält (meist für das Interface `eth0` oder das Bridge-Interface `vmbr0`), z.B.
   ```
   auto eth0
   iface eth0 inet static
   address 192.168.1.100
   netmask 255.255.255.0
   gateway 192.168.1.1
   ```
4. Ändere dort die `address`-Zeile auf die neue gewünschte IP-Adresse. Passe bei Bedarf auch `netmask` und `gateway` an.
5. Speichere die Datei und verlasse den Editor (bei nano: Strg+X, dann Y, Enter).
6. Aktualisiere außerdem die Datei `/etc/hosts`, um die neue IP-Adresse für den Servernamen einzutragen:
   ```
   nano /etc/hosts
   ```
   Hier muss die alte IP durch die neue für den Hostnamen ersetzt werden.
7. Starte den Netzwerkdienst neu, um die Änderung zu aktivieren:
   ```
   systemctl restart networking
   ```
8. Optional: Starte den Server neu, um sicherzustellen, dass alle Dienste die neue IP verwenden:
   ```
   reboot now
   ```
9. Nach dem Neustart solltest du die Proxmox-Weboberfläche über die neue IP und Port 8006 erreichen können:
   ```
   https://NEUE_IP:8006
   ```

Wichtig: Wenn dein Proxmox Teil eines Clusters ist, kann die Änderung der IP-Adresse zu Problemen führen und muss sorgfältig geplant werden. Falls du virtuelle Maschinen oder Container mit fixen IPs betreibst, müssen diese ggf. ebenfalls angepasst werden[1][3][5][7].

[1] https://kenbinlab.com/how-to-change-proxmox-management-ip-address-2/
[2] https://docs.linuxmuster.net/de/latest/installation/install-from-scratch/proxmox_internes_netz.html
[3] https://www.wundertech.net/how-to-change-the-ip-address-of-proxmox-ve/
[4] https://forum.proxmox.com/tags/ip-adresse/
[5] https://www.nakivo.com/blog/how-to-change-primary-proxmox-ve-ip-address/
[6] https://www.reddit.com/r/Proxmox/comments/10jzxd8/how_to_change_the_ip_of_a_shared_drive/?tl=de
[7] https://www.reddit.com/r/Proxmox/comments/xdkeqz/actual_correct_way_to_change_the_ip_of_proxmox/?tl=de
[8] https://forum.netcup.de/administration-eines-server-vserver/vserver-server-kvm-server/9763-proxmox-vm-ip-zuweisen/
[9] https://forum.proxmox.com/threads/proxmox-ve-vorbereiten-dann-ip-adresse-%C3%A4ndern.157816/
[10] https://www.youtube.com/watch?v=-HgkigKCNMw
