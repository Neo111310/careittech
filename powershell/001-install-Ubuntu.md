Um **PowerShell unter Ubuntu zu installieren**, sind nur wenige Schritte im Terminal nötig.[1][2][7]

## Installation über das Microsoft Repository

- Aktualisiere die Paketliste:
  ```
  sudo apt-get update
  ```
- Installiere notwendige Pakete:
  ```
  sudo apt-get install -y wget apt-transport-https software-properties-common
  ```
- Lade das Microsoft Repository-Paket herunter:
  ```
  wget -q https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
  ```
- Registriere das Repository:
  ```
  sudo dpkg -i packages-microsoft-prod.deb
  rm packages-microsoft-prod.deb
  ```
- Aktualisiere die Paketliste erneut:
  ```
  sudo apt-get update
  ```
- Installiere PowerShell:
  ```
  sudo apt-get install -y powershell
  ```

## Alternativ: Installation mit Snap

- Installiere Snap (falls nicht vorhanden):
  ```
  sudo apt-get install snap snapd -y
  ```
- Installiere PowerShell:
  ```
  sudo snap install powershell --classic
  ```

## PowerShell starten

- Starte PowerShell mit:
  ```
  pwsh
  ```
- Damit öffnet sich die PowerShell-Konsole und **PowerShell ist sofort auf Ubuntu einsatzbereit**.[2][3][7][1]

## Hinweise

- Für die beste Kompatibilität empfiehlt Microsoft die Installation über das Microsoft-Repository.[7]
- Nach der Installation können alle PowerShell-Module wie auf einem Windows-System genutzt werden.[3][1][2]

[1](https://linuxcapable.com/how-to-install-powershell-on-ubuntu-linux/)
[2](https://www.howtoforge.de/anleitung/so-installieren-und-verwenden-sie-powershell-unter-ubuntu-20-04/)
[3](https://it-learner.de/powershell-linux-so-funktioniert-die-installation/)
[4](https://www.youtube.com/watch?v=PSXiftoCQjE)
[5](https://www.liquidweb.com/blog/installing-microsoft-powershell-on-ubuntu-linux/)
[6](https://secure-bits.org/posts/windows/windows-powershell/)
[7](https://learn.microsoft.com/de-de/powershell/scripting/install/install-ubuntu?view=powershell-7.5)
[8](https://learn.microsoft.com/de-de/powershell/scripting/install/installing-powershell-on-linux?view=powershell-7.5)
[9](https://www.windowspro.de/wolfgang-sommergut/anleitung-powershell-7-windows-linux-installieren)
