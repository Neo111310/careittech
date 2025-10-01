# Ubuntu SSH Agent mit Bitwarden

Enable the Bitwarden SSH Agent on Linux:
 Configure the SSH_AUTH_SOCK variable to point to the Bitwarden SSH Agent socket. The following example demonstrates how to do this after replacing <user> with your username:

``` Plain Text
export SSH_AUTH_SOCK=/home/<user>/.bitwarden-ssh-agent.sock
```
Shell configuration

Access your .bashrc or .zshrc file:
```Plain Text
nano ~/.bashrc
nano ~/.zshrc
```
Set the environment variable in the .bashrc or .zshrc file:

```Plain Text
export SSH_AUTH_SOCK=/home/<user>/.bitwarden-ssh-agent.sock
```
Snap and Flatpak

Enable the Bitwarden SSH Agent on snap or Flatpak installations:
    Configure the SSH_AUTH_SOCK variable to point to the Bitwarden SSH Agent socket. The following example demonstrates how to do this after replacing <user> with your username:

```Plain Text
# Snap
export SSH_AUTH_SOCK=/home/<user>/snap/bitwarden/current/.bitwarden-ssh-agent.sock
# Flatpak
export SSH_AUTH_SOCK=/home/<user>/.var/app/com.bitwarden.desktop/data/.bitwarden-ssh-agent.sock
```

