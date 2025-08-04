Um unter einem Ubuntu Server die Befehle **ping** und **traceroute** zu installieren, gehen Sie wie folgt vor:

1. Paketliste aktualisieren:

```bash
sudo apt update
```

2. **Ping** installieren (im Paket iputils-ping enthalten):

```bash
sudo apt install iputils-ping
```

3. **Traceroute** installieren:

```bash
sudo apt install traceroute
```

4. Installation prüfen:

```bash
ping -c 4 google.com     # Testet 4 Ping-Anfragen
traceroute google.com    # Führt Traceroute zu google.com aus
```

So stehen Ihnen beide Netzwerktools auf dem Ubuntu Server zur Verfügung[1][2][3][5].

[1] https://secure-bits.org/posts/linux/der-traceroute-befehl-unter-linux/
[2] https://www.linux.digibeatrix.com/de/network-configuration/install-ping-command-ubuntu/
[3] https://wiki.ubuntuusers.de/traceroute/
[4] https://pimylifeup.com/ubuntu-traceroute/
[5] https://alexhost.com/faq/ping-command-not-found-how-to-install-ping-in-ubuntu/
[6] https://wiki.ubuntuusers.de/ping/
[7] https://www.thomas-krenn.com/de/wiki/Linux_Netzwerk_Analyse_mit_traceroute
[8] https://www.layerstack.com/resources/tutorials/How-to-install-and-use-Traceroute-on-CentOS-Ubuntu-Debian-Cloud-Servers
[9] https://serverspace.io/de/support/help/traceroute-to-trace-network-in-linux-instruction/
