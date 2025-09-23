[https://www.simplysmart.house/blog/how-to-install-HACS-docker-portainer](https://www.simplysmart.house/blog/how-to-install-HACS-docker-portainer)\

# Portainer Installation
Step 1: Access Portainer
Open your Portainer interface and go to the Containers section from the left sidebar.

Step 2: Access the Console
Find your Home Assistant container in the list and click on the "Exec Console" button (>_).

Step 3: Connect to the Terminal
Ensure /bin/bash is selected in the Command field, then click "Connect" to open a terminal session inside your container.

```
wget -O - https://get.hacs.xyz | bash -
``´

