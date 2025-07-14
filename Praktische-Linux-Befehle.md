# Praktische Linux Befehle

Services / Daemons unter Linux Listen
```
systemctl --type=service --state=running
```
Man zu Systemctl https://www.commandlinux.com/man-page/man1/systemctl.1.html 

Daemon Stoppen und disablen

systemctl stop [servicename]

systemctl disable [servicename]

rm /etc/systemd/system/[servicename]

rm /etc/systemd/system/[servicename] # and symlinks that might be related

rm /usr/lib/systemd/system/[servicename] 

rm /usr/lib/systemd/system/[servicename] # and symlinks that might be related
systemctl daemon-reload

systemctl reset-failed

Geklaut aus: https://superuser.com/questions/513159/how-to-remove-systemd-services


SSH Zugriff Erlauben / Löschen

SSH Root Access
Login to your server as root.
As the root user, edit the sshd_config file found in /etc/ssh/sshd_config:vim /etc/ssh/sshd_config
Add the following line to the file, you can add it anywhere but it’s good practice to find the block about authentication and add it there.
NANO Install!
sudo apt install nano
nano - /etc/ssh/sshd_config
PermitRootLogin yes
Save and exit the file.
 
Restart the SSH server:
systemctl restart sshd
or
service sshd restart
 
And that’s it! With the new line added and the SSH server restarted, you can now connect via the root user.

SSh Server Install
https://ubuntu.com/server/docs/openssh-server
 
`sudo apt update && sudo apt upgrade`
`sudo apt install openssh-server`
`service ssh status

SSH Am Client und Server

..# Create Local certificate
Create SSH Key on Linux
 
To create an SSH key pair on a Linux system, follow these steps:
 
1. Open a terminal window on your local machine.
2. Use the `ssh-keygen` command to generate a new SSH key. You can specify the type of key to create and the length of the key. For example, to create an RSA key with a length of 4096 bits, you can use the following command:
 
```shell
ssh-keygen -t rsa -b 4096
```
 
oder
 
```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```
<img width="693" height="2139" alt="image" src="https://github.com/user-attachments/assets/8de1b304-fcdd-437d-9f65-234a778fe99c" />
