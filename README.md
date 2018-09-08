# Mikrotik-Example-Firewall-Filter
A collection of useful Mikrotik Firewall Filter/Rules

### Social & Streaming Filter/Queue 
```console

/ip firewall filter
add action=drop chain=forward comment="Drop Facebook" connection-mark=facebook_connection dst-port=80,443 protocol=tcp src-address-list=!Facebook_Allowed
add action=drop chain=forward comment="Drop Twitter" connection-mark=twitter_connection dst-port=80,443 protocol=tcp src-address-list=!Twitter_Allowed
	
/ip firewall mangle
add action=mark-connection chain=prerouting comment=Youtube content=youtube dst-port=80,443 new-connection-mark=youtube_connection passthrough=yes protocol=tcp
add action=mark-connection chain=prerouting content=youtube dst-port=80,443 new-connection-mark=youtube_connection protocol=udp
add action=mark-connection chain=prerouting content=googlevideo dst-port=80,443 new-connection-mark=youtube_connection protocol=tcp
add action=mark-connection chain=prerouting content=googlevideo dst-port=80,443 new-connection-mark=youtube_connection protocol=udp
add action=mark-connection chain=prerouting content=youtu.be dst-port=80,443 new-connection-mark=youtube_connection protocol=tcp
add action=mark-connection chain=prerouting content=youtu.be dst-port=80,443 new-connection-mark=youtube_connection protocol=udp
add action=mark-packet chain=prerouting connection-mark=youtube_connection new-packet-mark=youtube_packets passthrough=no
add action=mark-connection chain=prerouting comment=Netflix content=netflix.com new-connection-mark=netflix_connection passthrough=yes port=80,443 protocol=tcp
add action=mark-connection chain=prerouting content=nflxvideo.net new-connection-mark=netflix_connection passthrough=yes port=80,443 protocol=tcp
add action=mark-connection chain=prerouting content=nflxso.net new-connection-mark=netflix_connection passthrough=yes port=80,443 protocol=tcp
add action=mark-packet chain=prerouting connection-mark=netflix_connection new-packet-mark=netflix_packets passthrough=no port=80,443 protocol=tcp
add action=mark-connection chain=prerouting comment=Facebook content=facebook dst-port=80,443 new-connection-mark=facebook_connection passthrough=no protocol=tcp
add action=mark-connection chain=prerouting content=fbcdn.net dst-port=80,443 new-connection-mark=facebook_connection passthrough=no protocol=tcp
add action=mark-connection chain=prerouting comment=Twitter content=twitter dst-port=80,443 new-connection-mark=twitter_connection passthrough=no protocol=tcp
add action=mark-connection chain=prerouting content=twimg.com dst-port=80,443 new-connection-mark=twitter_connection passthrough=no protocol=tcp

/queue simple
add name=”YOUTUBE” target=192.168.88.0/24 parent=none packet-marks=youtube_connection priority=8/8 queue=default/default limit-at=0/0 max-limit=50M/50M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1 total-queue=default

add name=”NETFLIX” target=192.168.88.0/24 parent=none packet-marks=netflix_connection priority=8/8 queue=default/default limit-at=0/0 max-limit=50M/50M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1 total-queue=default

```
