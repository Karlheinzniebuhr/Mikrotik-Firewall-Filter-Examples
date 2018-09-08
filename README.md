# Mikrotik-Example-Firewall-Filter
A collection of useful Mikrotik Firewall Filter/Rules

### Social media & streaming filter
```console
/ip firewall filter
add action=drop chain=forward comment="Drop Facebook" connection-mark=conexion_facebook dst-port=80,443 protocol=tcp src-address-list=!Permitidos_Facebook
add action=drop chain=forward comment="Drop Twitter" connection-mark=conexion_Twitter dst-port=80,443 protocol=tcp src-address-list=!Permitidos_Twitter
add action=drop chain=forward comment=Drop_WindowsUpdate connection-mark=conexion_WindowsUpdate dst-port=80,443 protocol=tcp
	
/ip firewall mangle
add action=mark-connection chain=prerouting comment=Youtube content=youtube dst-port=80,443 new-connection-mark=conexion_youtube passthrough=yes protocol=tcp
add action=mark-connection chain=prerouting content=youtube dst-port=80,443 new-connection-mark=conexion_youtube protocol=udp
add action=mark-connection chain=prerouting content=googlevideo dst-port=80,443 new-connection-mark=conexion_youtube protocol=tcp
add action=mark-connection chain=prerouting content=googlevideo dst-port=80,443 new-connection-mark=conexion_youtube protocol=udp
add action=mark-connection chain=prerouting content=youtu.be dst-port=80,443 new-connection-mark=conexion_youtube protocol=tcp
add action=mark-connection chain=prerouting content=youtu.be dst-port=80,443 new-connection-mark=conexion_youtube protocol=udp
add action=mark-packet chain=prerouting connection-mark=conexion_youtube new-packet-mark=paquetes_Youtube passthrough=no
add action=mark-connection chain=prerouting comment=Netflix content=netflix.com new-connection-mark=conexion_Netflix passthrough=yes port=80,443 protocol=tcp
add action=mark-connection chain=prerouting content=nflxvideo.net new-connection-mark=conexion_Netflix passthrough=yes port=80,443 protocol=tcp
add action=mark-connection chain=prerouting content=nflxso.net new-connection-mark=conexion_Netflix passthrough=yes port=80,443 protocol=tcp
add action=mark-packet chain=prerouting connection-mark=conexion_Netflix new-packet-mark=paquetes_Netflix passthrough=no port=80,443 protocol=tcp
add action=mark-connection chain=prerouting comment=Facebook content=facebook dst-port=80,443 new-connection-mark=conexion_facebook passthrough=no protocol=tcp
add action=mark-connection chain=prerouting content=fbcdn.net dst-port=80,443 new-connection-mark=conexion_facebook passthrough=no protocol=tcp
add action=mark-connection chain=prerouting comment=Twitter content=twitter dst-port=80,443 new-connection-mark=conexion_Twitter passthrough=no protocol=tcp
add action=mark-connection chain=prerouting content=twimg.com dst-port=80,443 new-connection-mark=conexion_Twitter passthrough=no protocol=tcp
add action=mark-connection chain=prerouting comment=WindowsUpdate content=windowsupdate dst-port=80,443 new-connection-mark=conexion_WindowsUpdate passthrough=no protocol=tcp


```
