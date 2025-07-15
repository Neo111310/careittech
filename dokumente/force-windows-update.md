Um unter **Windows** sofort alle Updates zwingend auszuführen und den Rechner neu zu starten, eignet sich ein **PowerShell-Skript** mit dem Modul **PSWindowsUpdate**. Dieses Modul ermöglicht das gezielte Suchen, Installieren und Erzwingen von Windows-Updates inklusive anschließendem Neustart.

**Schritt-für-Schritt-Anleitung:**

1. **PowerShell als Administrator öffnen.**
2. Das Modul installieren (falls noch nicht vorhanden):

```powershell
Install-Module -Name PSWindowsUpdate -Force
```
Falls es wegen alter TLS-Versionen Probleme gibt, setze vorher:

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```


3. **Updates suchen, installieren und Neustart erzwingen:**

```powershell
Import-Module PSWindowsUpdate
Get-WindowsUpdate -AcceptAll -Install -AutoReboot
```
- `-AcceptAll` akzeptiert alle vorgeschlagenen Updates
- `-Install` installiert diese sofort
- `-AutoReboot` startet das System nach Abschluss der Installation automatisch neu

**Hinweis:** Mit **diesen Befehlen wird der Rechner ohne weitere Rückfrage nach Abschluss der Updates neu gestartet**. Verwende diesen Ablauf daher nur, wenn der Neustart wirklich sofort erfolgen soll[2][7].

**Alternative:** Mit Bordmitteln ist via Eingabeaufforderung oder PowerShell auch das Tool `wusa.exe` verfügbar, um einzelne MSU-Dateien zu installieren und per `/forcerestart` einen Neustart zu erzwingen[7]. Das ist jedoch weniger flexibel, wenn alle verfügbaren Updates installiert werden sollen.

**Fazit:**  
Mit dem oben genannten PowerShell-Skript wird dein Wunsch exakt umgesetzt: **sofortige, vollständige Update-Installation mit Zwangsneustart**.

[1] https://learn.microsoft.com/de-de/windows/deployment/update/waas-wu-settings
[2] https://www.thomas-krampe.com/2022/03/windows-updates-mit-powershell-durchfuehren/
[3] https://www.reddit.com/r/PowerShell/comments/tgy788/script_for_sysadmins_to_automate_windows_updates/?tl=de
[4] https://www.mcseboard.de/topic/222913-windows-server-updates-automatisch-installieren-und-neustarten/
[5] https://www.der-windows-papst.de/2021/08/06/windows-patche-automatisch-per-skript-installieren/
[6] https://znil.net/index.php/Windows_Update_per_Skript_suchen_herunterladen_installieren_reboot
[7] https://www.computerweekly.com/de/ratgeber/So-verwalten-Sie-Windows-Updates-mit-PowerShell
[8] https://www.windowspro.de/wolfgang-sommergut/wuinstall-windows-updates-installieren-ueber-kommandozeile-scripts
[9] https://www.reddit.com/r/PowerShell/comments/1imik92/is_there_a_way_to_do_an_automatic_windows_update/?tl=de
[10] https://www.computerbase.de/forum/threads/windows-updates-automatisieren.2187293/
