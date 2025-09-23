Um eine "Microsoft Outlook OAuth2 API" für n8n einzurichten, muss zuerst eine App in Azure registriert und anschließend in n8n eine neue OAuth2-Credential mit den erhaltenen Daten hinterlegt werden. Dies funktioniert sowohl für n8n-Cloud als auch für Self-Hosted-Instanzen.[1][2][10]

### Schritt-für-Schritt-Anleitung

#### 1. Azure App Registration
- Gehe zu https://portal.azure.com/ und wähle „App-Registrierungen“ aus.[2][1]
- Klicke auf „Neue Registrierung“ und gib einen Namen ein, z. B. „n8n Outlook Integration“.[1]
- Wähle bei „Unterstützte Kontotypen“ am besten „Konten in jedem Organisationsverzeichnis und persönliche Microsoft-Konten“.[2][1]
- Gib als Umleitungs-URI (Redirect URI) folgendes an:
  - Typ: Web
  - URL: https://DEINE-N8N-DOMAIN/rest/oauth2-credential/callback
  - (Ersetze DEINE-N8N-DOMAIN durch die echte URL deiner n8n-Instanz).[5][1][2]
- Klicke auf „Registrieren“.[1]

#### 2. Rechte & Client-Secret festlegen
- Gehe zu „API-Berechtigungen“ ➔ „Berechtigung hinzufügen“ ➔ Microsoft Graph ➔ Delegierte Berechtigungen.[2][1]
- Wähle z. B. folgende Scopes:
  - `Mail.Read`, `Mail.ReadWrite`, `Mail.Send`, `offline_access`, `Calendars.ReadWrite`.[1][2]
- Bestätige und vergib ggf. Admin-Konsens.[1]
- Gehe zu „Zertifikate & Geheimnisse“ ➔ „Neues geheimer Schlüssel“, gib einen Namen an und kopiere das generierte Secret.[2]

#### 3. Daten in n8n eintragen
- Öffne n8n ➔ „Credentials“ ➔ „Neue Credential anlegen“ ➔ Typ „Microsoft OAuth2 API“.[10][2]
- Gib die „Client ID“ und das „Client Secret“ aus Azure ein.[2]
- Gib die „Scopes“ an, z. B.:  
  - `openid offline_access Mail.ReadWrite Mail.Send Calendars.ReadWrite`.[2]
- Stelle sicher, dass die Redirect-URI in Azure und in n8n exakt gleich sind.[5]
- Klicke auf „Connect my account“ und folge der Anmeldung bei Microsoft.[10][2]

#### 4. Verbindung testen
- Nach erfolgreichem Login wird die Verbindung grün angezeigt und n8n kann nun Outlook automatisch steuern (Mails, Kalender usw.).[7][10]

Mit dieser Integration kannst du Outlook in Automatisierungen mit n8n-Workflows einbinden – etwa zum Lesen, Schreiben und Senden von E-Mails sowie für Kalenderaktionen.[10][1][2]

[1](https://www.scribd.com/document/898491862/Outlook-API-n8n-Setup-Guide)
[2](https://docs.n8n.io/integrations/builtin/credentials/microsoft/)
[3](https://www.youtube.com/watch?v=Rh_GuNtgq-U)
[4](https://www.youtube.com/watch?v=aqr_PwR1Sgc)
[5](https://community.n8n.io/t/microsoft-outlook-oauth2-error/83168)
[6](https://www.youtube.com/watch?v=4CCtuXVtDt8)
[7](https://www.youtube.com/watch?v=h7BLVKh7yzc)
[8](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.microsoftoutlook/)
[9](https://community.latenode.com/t/troubleshooting-outlook-smtp-authentication-in-n8n/14657)
[10](https://n8n.io/workflows/6226-automate-daily-outlook-calendar-digests-to-microsoft-teams/)


# n8n Config
unter /opt/n8n.env Editor Eintragen\
**Muster**
```
N8N_SECURE_COOKIE=false
N8N_PORT=5678
N8N_PROTOCOL=http
N8N_HOST=172.18.9.25
WEBHOOK_URL=https://n8n.mintakalab.blabla.org/
N8N_EDITOR_BASE_URL=https://n8n.mintakalab.blabla.org/
```
