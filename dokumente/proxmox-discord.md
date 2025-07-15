# Proxmox Notification to Discord Webhook

Erstelle einen Webhook am Server bzw. kanal und dann Erstelle einen Webhook mit POST\
Header: Content-Type = application/json\
Dann folgendes als Vorlage:
```
{"content":null,"embeds":[{"title":"```{{ escape title }}```","description":"```{{ escape message }}```","color":null,"footer":{"text":"Proxmox"}}],"attachments":[]}
```
Thats IT
