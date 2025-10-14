Um ein Microsoft Shared Postfach (freigegebenes Postfach) so zu konfigurieren, dass beim Versenden von E-Mails immer die Shared Mailbox als Absenderadresse verwendet wird und nicht die persönliche Mailadresse, gibt es mehrere Möglichkeiten:

1. Registrierungsschlüssel (Reg-Key) in Outlook (für Clients):
   - Für Outlook-Clients kann man mit einem Registry-Eintrag bewirken, dass gesendete Mails vom Shared Postfach als Absender versandt werden und die Mails im Ordner „Gesendete Objekte“ des Shared Postfachs landen.
   - Beispiel-Registry-Pfad:
     ```
     HKEY_CURRENT_USER\Software\Microsoft\Office\<Version>\Outlook\Preferences
     ```
     Dort ein DWORD-Wert:
     ```
     DelegateSentItemsStyle = 1
     ```
   - Dies wirkt sich auf das Ablegen der gesendeten Elemente aus und kann helfen, dass Senden als Shared Mailbox korrekt funktioniert. Allerdings stellt es nicht sicher, dass beim Erstellen einer neuen Mail automatisch die Shared Mailbox als Absender gesetzt wird, sondern der Nutzer muss die Absenderadresse ggf. manuell auswählen.[6][8]

2. Exchange Online PowerShell Konfiguration:
   - Um sicherzustellen, dass gesendete Mails, die über ein Shared Mailbox mit "Senden als" oder "Im Auftrag von" verschickt wurden, auch im Ordner „Gesendete Elemente“ des Shared Postfaches gespeichert werden, kann man folgende PowerShell-Befehle nutzen:
     ```
     Set-Mailbox -Identity "SharedMailbox" -MessageCopyForSentAsEnabled $true -MessageCopyForSendOnBehalfEnabled $true
     ```
   - Dies stellt auch sicher, dass die Mail im Shared Postfach abgelegt wird und ist dem Registry-Key vorzuziehen.[8][6]

3. Für das automatische Setzen der Shared Mailbox als Absenderadresse beim Verfassen neuer Mails gibt es keine offizielle und durchgängige Reg-Key-Lösung. Die Auswahl der Absenderadresse ist in der Regel clientseitig vom Nutzer zu treffen.
   - Einige Workarounds oder Scripts (PowerShell) können auf administrativer Ebene eingesetzt werden, aber die Möglichkeiten sind stark eingeschränkt.
   - Manche Nutzer setzten Outlook-Profile eigens für das Shared Mailbox auf oder verwenden Add-Ins, um das Verhalten anzupassen.[3][7]

4. Vermeidung von Fehlern:
   - Wichtig ist, dass die Benutzer über „Senden als“- oder „Senden im Auftrag von“-Berechtigungen korrekt verfügen.
   - Wenn Benutzer statt der Shared Mailbox Adresse ihre persönliche Mailadresse als Absender erscheint, fehlt meist die korrekte Berechtigung oder die Absenderadresse wurde manuell nicht gesetzt.[4]

Fazit:
Für das automatische Versenden immer mit der Shared Mailbox Adresse gibt es keinen offiziell dokumentierten Reg-Key, der dies komplett erzwingt. Der empfohlene Weg ist:

- Benutzer mit „Senden als“-Berechtigung versehen.
- PowerShell-Command zur Speicherung von gesendeten Mails im Shared Postfach einsetzen.
- Optional Registry-Key „DelegateSentItemsStyle=1“ in Outlook setzen für sauberes Handling der gesendeten Elemente.
- Benutzer/Administratoren müssen im Outlook ggf. die Absenderadresse manuell auswählen, oder ein eigenes Profil für das Shared Mailbox anlegen.

Damit ist das Verhalten für Shared Mailbox Absenderadressen optimal konfiguriert.[4][6][8]

[1](https://learn.microsoft.com/de-de/microsoft-365/admin/email/about-shared-mailboxes?view=o365-worldwide)
[2](https://learn.microsoft.com/de-de/microsoft-365/admin/email/configure-a-shared-mailbox?view=o365-worldwide)
[3](https://www.anleitungen.rrze.fau.de/e-mail/exchange/shared-mailbox-als-primaere-absendeadresse-konfigurieren/)
[4](https://www.reddit.com/r/sysadmin/comments/1nquz1g/ps_to_change_the_send_address_of_shared_mailbox/)
[5](https://learn.microsoft.com/de-de/answers/questions/4712440/von-automatisch-bei-antwort-aus-freigegebenen-post)
[6](https://www.msxfaq.de/konzepte/sharedmailbox.htm)
[7](https://learn.microsoft.com/de-de/answers/questions/4574541/shared-mailbox-als-standard-versandadresse-festleg?forum=outlook_com-all)
[8](https://www.frankysweb.de/exchange-2016-freigegebene-postfcher-shared-mailbox/)
[9](https://www.mcseboard.de/topic/222865-shared-mailbox-von-feld/)
[10](https://www.hardwareluxx.de/community/threads/freigegebenes-postfach-in-outlook.1347435/)
