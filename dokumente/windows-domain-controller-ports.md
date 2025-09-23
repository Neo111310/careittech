Um einen Windows Domain Controller zu erreichen und ihn vollständig zu nutzen, sollten folgende TCP- und UDP-Ports geöffnet sein:

| Port        | Protokoll   | Dienst / Verwendungszweck                              |
|-------------|-------------|-------------------------------------------------------|
| 53          | TCP/UDP     | DNS (Domain Name System) für Namensauflösung          |
| 88          | TCP/UDP     | Kerberos-Authentifizierung                             |
| 123         | UDP         | W32Time (Zeitsynchronisation)                          |
| 135         | TCP         | RPC Endpoint Mapper (Remote Procedure Call)           |
| 137, 138    | UDP         | NetBIOS (wenn noch ältere Systeme genutzt werden)     |
| 139         | TCP         | NetBIOS Session Service (veraltet, ersetzt durch SMB) |
| 389         | TCP/UDP     | LDAP (Lightweight Directory Access Protocol)          |
| 445         | TCP         | SMB (Microsoft-DS) für Datei- und Druckfreigaben      |
| 464         | TCP/UDP     | Kerberos Passwortänderung                              |
| 636         | TCP         | LDAP über SSL (LDAPS)                                  |
| 9389        | TCP         | Active Directory Web Services (ADWS)                   |
| 3268, 3269  | TCP         | Global Catalog (LDAP GC und LDAP GC SSL)               |
| 49152-65535 | TCP         | RPC Ephemeral Ports (dynamische RPC-Ports)             |

Wichtige Hinweise:
- NetBIOS-Ports (137-139) sind bei aktuellen Windows-Versionen (Windows Server 2012 und neuer) normalerweise nicht mehr notwendig, da SMB sie ersetzt hat.
- Der Bereich der dynamischen RPC-Ports (49152-65535) ist für die Kommunikation essenziell und sollte vollständig offen sein, da die genaue Portnummer dynamisch vergeben wird.
- Zeit-Synchronisation über UDP 123 ist wichtig, da Kerberos und andere Dienste auf korrekte Systemzeit angewiesen sind.

Diese Ports sind sowohl für die Kommunikation zwischen Domain Controllern (Replikation, Trusts) als auch zwischen Client und Domain Controller entscheidend.[1][2][3][5]

Eine Firewall-Konfiguration für Domain Controller sollte diese freigeben, um einen störungsfreien Betrieb von Active Directory sicherzustellen.

[1](https://lazyadmin.nl/it/domain-controller-ports/)
[2](https://activedirectorypro.com/active-directory-ports-used-client-to-server/)
[3](https://learn.microsoft.com/en-us/answers/questions/901610/tcp-and-ud-ports-required-for-communication-betwee)
[4](https://firewall.dsinternals.com/ADDS/)
[5](https://learn.microsoft.com/de-de/troubleshoot/windows-server/active-directory/config-firewall-for-ad-domains-and-trusts)
[6](http://www.hasslinger.com/microsoft/sites/server/dotnet/grund/active_directory_ports.html)
[7](https://www.der-windows-papst.de/2023/03/05/ports-active-directory-und-active-directory-domaenendienste/)
[8](https://support.tools/required-domain-controller-ports/)
[9](https://www.encryptionconsulting.com/ports-required-for-active-directory-and-pki/)
