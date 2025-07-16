Um **Docker auf Ubuntu** zu installieren, folge diesen Schritten:

1. **System vorbereiten:**
   ```bash
   sudo apt-get update
   sudo apt-get install \
     ca-certificates \
     curl \
     gnupg \
     lsb-release
   ```
2. **Docker GPG-Schlüssel hinzufügen:**
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```
3. **Docker-Repository hinzufügen:**
   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   ```
4. **Docker installieren:**
   ```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```
5. **Docker-Dienst starten und beim Booten aktivieren:**
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```
6. **Installation testen:**
   ```bash
   docker --version
   sudo docker run hello-world
   ```

Diese Schritte installieren die aktuelle Version der **Docker Engine** direkt aus dem offiziellen Docker-Repository auf Ubuntu[1][2][4].

[1] https://armann-systems.com/wiki/installation-von-docker-engine-unter-ubuntu-ein-umfassender-leitfaden/
[2] https://www.datacamp.com/de/tutorial/install-docker-on-ubuntu
[3] https://docs.docker.com/desktop/setup/install/linux/ubuntu/
[4] https://www.ionos.at/digitalguide/server/konfiguration/docker-auf-ubuntu-2204-installieren/
[5] https://kinsta.com/de/blog/installieren-docker-ubuntu/
[6] https://docs.docker.com/engine/install/ubuntu/
[7] https://www.thomas-krenn.com/de/wiki/Docker_Installation_unter_Ubuntu_24.04
[8] https://www.ionos.at/digitalguide/server/konfiguration/docker-auf-ubuntu-2004-installieren/
[9] https://www.youtube.com/watch?v=YJSf5VpIOyE
[10] https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04
