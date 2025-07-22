# Caddy Reverse Proxy

[Gutes Video zu caddy](https://youtu.be/I8c7u28K9z8?si=0hvCDo1YAPKrcFjW)\
[Quick Start Caddy](https://caddyserver.com/docs/quick-starts/reverse-proxy)\
[Der Blog Beitrag](https://jusec.me/caddy/)

# Installations Hilfe Ubuntu

## Vorbereitungen
- Domainamen als A Record im DNS eintragen
- Host muss am Port 80 und 443 Erreichbar sein aus dem Internet

ää Installation

Um **Caddy auf Ubuntu zu installieren**, folge diesen Schritten:

1. **GPG-Key für das Caddy-Repository hinzufügen:**
   ```bash
   curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
   ```
2. **Caddy-Repository zu den Paketquellen hinzufügen:**
   ```bash
   curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
   ```
3. **Paketliste aktualisieren:**
   ```bash
   sudo apt update
   ```
4. **Caddy installieren:**
   ```bash
   sudo apt install caddy
   ```
   
Nach der Installation startet Caddy automatisch als Dienst und ist bereit für Konfiguration und Einsatz[2][4].

**Optional, aber empfohlen:**  
- Stelle sicher, dass Ports **80** und **443** in deiner Firewall geöffnet sind, damit Caddy HTTP- und HTTPS-Traffic empfangen kann[2][4].

**Anzeigen der installierten Version zur Überprüfung:**
```bash
caddy version
```
Damit ist Caddy betriebsbereit. Du kannst jetzt den Reverse-Proxy oder andere Funktionen konfigurieren.\
**Vorteile:**\
Automatische SSL-Konfiguration: Sobald du eine echte Domain nutzt und die DNS-Einträge richtig gesetzt sind, holt Caddy automatisch ein gültiges SSL-Zertifikat (Let's Encrypt/ZeroSSL) und kümmert sich um die Erneuerung
Das Konfig File ist unter **/etc/caddy/Caddyfile** [Zusatzinfo](https://blog.ordix.de/caddy-reverse-proxy-in-einfach) 
```
deinedomain.de {
  reverse_proxy /api/* localhost:5000
}
```
Diesre eintrag ins Config File ***! Vorsicht UUNerlin nicht Dash !***

Restarte caddy
```
systemctl restart caddy
```
## Das ist so weit alles

[1] https://cloudinfrastructureservices.co.uk/setup-caddy-reverse-proxy-on-ubuntu-in-azure-aws-gcp/
[2] https://pimylifeup.com/ubuntu-caddy/
[3] https://www.youtube.com/watch?v=PdkTn6XhdMQ
[4] https://docs.vultr.com/how-to-install-caddy-webserver-on-ubuntu-24-04
[5] https://caddyserver.com/docs/quick-starts/reverse-proxy
[6] https://caddy.community/t/using-caddy-in-ubunutu-to-reverse-proxy-to-local-devices/20469
[7] https://caddyserver.com/docs/install
[8] https://amirpourmand.ir/posts/2024/caddy-reverse-proxy/
[9] https://www.rosehosting.com/blog/how-to-install-caddy-web-server-on-ubuntu-22-04/
[10] https://linuxiac.com/how-to-set-up-caddy-as-reverse-proxy/

# Simpler Webserver mit Python
Alternativ, wenn es wirklich nur für ganz simple Tests sein soll, kann man auch ganz minimalistisch mit Python einen Webserver starten:
```
bash
cd /pfad/zum/ordner
python3 -m http.server 8080
```
Dies startet einen schnellen HTTP-Server auf Port 8080, ideal für temporäre Tests ohne Installation.

Für dauerhafte oder produktive Dienste ist jedoch Apache (oder ein anderer Webserver wie Nginx) zu empfehlen.
