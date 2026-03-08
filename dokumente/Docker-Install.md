# Docker Install

Docker lässt sich einfach auf Ubuntu installieren, indem du das offizielle Repository nutzt. Als guten Docker-Manager empfehle ich Portainer oder Dockge für eine benutzerfreundliche Weboberfläche. [kati-pierson](https://www.kati-pierson.de/3153/docker-die-besten-tools-zum-management-von-containern/)

## Docker installieren

Aktualisiere zuerst dein System und installiere Voraussetzungen:

```
sudo apt update && sudo apt upgrade -y
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

Füge den Docker-GPG-Schlüssel und das Repository hinzu:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```

Installiere Docker:

```
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Starte Docker und aktiviere den Autostart:

```
sudo systemctl start docker
sudo systemctl enable docker
```

Überprüfe die Installation mit `sudo docker run hello-world`. [datacamp](https://www.datacamp.com/de/tutorial/install-docker-on-ubuntu)

Füge deinen Benutzer zur Docker-Gruppe hinzu, um sudo zu vermeiden: `sudo usermod -aG docker $USER` und logge dich neu ein. [blog.nevercodealone](https://blog.nevercodealone.de/docker-auf-ubuntu-installieren-gruppenrechte-sudo-probleme-und-best-practices-direkt-geloest/)

## Docker-Manager empfehlen

Portainer ist ein beliebter Web-Manager für Container, Images und Volumes – leicht zu installieren via `docker volume create portainer_data && docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce`. [kati-pierson](https://www.kati-pierson.de/3153/docker-die-besten-tools-zum-management-von-containern/)

Dockge ist eine moderne Alternative speziell für Docker Compose, mit einfacher Web-Verwaltung von Stacks und Updates – ideal für Selfhosting. [reddit](https://www.reddit.com/r/selfhosted/comments/1ltcc51/best_dashboard_for_a_ubuntu_docker_server/)

Andere Optionen: Yacht oder Homarr für Dashboards. Starte mit Portainer für Einsteiger. [reddit](https://www.reddit.com/r/selfhosted/comments/xuv0hq/any_recommendations_for_an_web_based_docker/)

