# Research
TCP AMP / TCP REFLECTION / UDP AMPLFICATION




----INTERNAL REFLECTION----


Infraly method: Servictics AS400529
shodan:https://www.shodan.io/search?query=asn:AS400529
TCP flags that are affective
ACK: PSH
SYN: PSH


Path method: Path networks AS396998
Ports: https://www.shodan.io/search?query=asn:AS396998
TCP flags that are affective
ACK + PSH:URG


Interal reflection POC
Send a ack or syn packet to a device that has a tcp app open and you can reflect off that device
This is useful because in most use cases hostings have trusted relationships between there own subnets
Most firewalls are accepting  anything inbound from there own ranges because it does very loose checks if it even checks it at all.

Find reflectors?
https://ipinfo.io/AS396998 copy ranges put it in file zmap on known ports 80,443,22,21,3389 are the best
zmap -p 80 -w path.lst -o p2ath.txt
zmap -p 443 -w path.lst -o p2ath2.txt
zmap -p 22 -w path.lst -o p2ath3.txt
cat p2* | sort | uniq >> pathnewreflectors.txt

Method POC
set dest to most used tcp application on hosting your trying to target
int ports[3] = {80, 443, 22};
tcph->dest = htons(ports[randnum(0, 3)]);
Dont use text file to load reflectors. use ip to digit.

Type of service matters 
length matters
Certain data is excepted better make sure tcpsum is setup correctly if it isnt some reflectors will not respond
data offset has to be set correctly 
tcp opts are useful for hostings that allow you to reflect using syn.
These are examples.

----TCP AMPLIFCATION?----
still testing
possible yes
payload:1-10 bytes
flags: ack
my average byte resp 40 to 60k bytes
reflector count:100k + 


----UDP AMPLFICATION----
ipsec 2nd port 4500 same payload same amp factor
