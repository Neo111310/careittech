## Proxmox remove subscription notice oneliner
## Credit to the original author whoever they are...

Run this command in the proxmox shell..
```
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```
Restart Proxmox just incase.
