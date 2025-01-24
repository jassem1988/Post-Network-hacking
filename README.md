# Post-Network-hacking

## Objective
Post Network hacking like gathering information and MITM attacks

### Skills Learned

- Connecting wireless adapter to Virtual Machine

### Tools used

- Netdiscover

### Steps to use netdiscover

- In Kali linux we will use ifcofig to find our IP address
- Look for Your Active Network Interface:
  - If you’re using Ethernet (wired connection), the interface is likely eth0 or enp0s3.
  - If you’re using Wi-Fi, the interface is usually wlan0 or wlp2s0.
```bash
ifconfig
```
- The IP address (e.g., 192.168.233.133) will follow immediately after inet.
- We will use netdiscover to scan all the ip addresses range
```bash
netdiscover -r 192.168.1.1/24
```
- If we connect a wifi adapter then we can connect to Wifi from the VM of Kali linux and make a scan with the IP address of wlan0
