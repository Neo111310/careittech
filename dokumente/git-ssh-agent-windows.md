Git anweisen, OpenSSH zu verwenden:
In der Eingabeaufforderung oder PowerShell:

```bash
git config --global core.sshCommand C:/Windows/System32/OpenSSH/ssh.exe
```
Dadurch verwendet Git den Windows OpenSSH-Client und kommuniziert mit dem laufenden SSH-Agent.
