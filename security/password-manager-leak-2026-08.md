# DOM-based extension clickjackin

Bitwarden hat den "DOM-based extension clickjacking" nicht komplett strukturell gefixt, aber mit Version 2025.8.0 im August 2025 ein wichtiges Update veröffentlicht, das viele Exploit-Möglichkeiten stark eingeschränkt und Schutzmaßnahmen wie Autofill-Restriktionen und Kontextprüfungen eingeführt hat.[1][4][7]

Das Update schränkt vor allem das automatische Ausfüllen ein, indem Autofill unter bestimmten Bedingungen deaktiviert wird, was den Angriff deutlich erschwert. Dennoch beruht der aktuelle Fix auf Einschränkungen und Filtern, nicht auf einer vollständigen Neuentwicklung der Ausfüll-Engine, die das grundlegende Designproblem beheben würde.[1]

Das bedeutet: Zwar ist die schlimmste Gefahr deutlich reduziert, aber Bitwarden (wie andere Anbieter) ist immer noch anfällig für DOM-basierte Clickjacking-Angriffe, solange die Architektur den DOM zur Geheimnis-Übergabe nutzt. Die dauerhafte Lösung wäre eine Zero-DOM-Architektur, die aktuell von keinem großen Anbieter vollständig implementiert ist.[3][1]

Nutzer sollten weiterhin vorsichtig sein, Autofill-Einstellungen prüfen und Sicherheitsupdates umgehend einspielen.[2][4]

Zusammengefasst: Bitwarden hat reagiert und wichtige Patches geliefert, jedoch noch keine endgültige, architektonische Lösung für das Problem.[4][1]

[1](https://freemindtronic.com/dom-extension-clickjacking-def-con-33-en/)
[2](https://community.bitwarden.com/t/should-i-be-worried-about-clickjacking/87988?page=2)
[3](https://www.nudgesecurity.com/post/dom-based-extension-clickjacking-vulnerabilities-in-popular-password-managers)
[4](https://www.ghacks.net/2025/08/21/zero-day-clickjacking-exploit-impacts-several-password-managers/)
[5](https://community.bitwarden.com/t/should-i-be-worried-about-clickjacking/87988)
[6](https://community.bitwarden.com/t/should-i-be-worried-about-clickjacking/87988/24)
[7](https://www.securityweek.com/password-managers-vulnerable-to-data-theft-via-clickjacking/)
[8](https://community.bitwarden.com/t/dom-based-extension-clickjacking/88441)
[9](https://www.reddit.com/r/selfhosted/comments/1mx4cn2/vulnerability_for_all_using_vaultwarden_with/)


Check auf OnePassword