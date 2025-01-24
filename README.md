# Post-Network-hacking

## Objective
Post Network hacking like gathering information and MITM attacks

### Skills Learned

- Connecting wireless adapter to Virtual Machine

### Tools used

- Netdiscover
- Zenmap
- nmap

### Steps to use netdiscover

- In Kali linux we will use ifcofig to find our IP address
- Look for Your Active Network Interface:
  - If you’re using Ethernet (wired connection), the interface is likely eth0 or enp0s3.
  - If you’re using Wi-Fi, the interface is usually wlan0 or wlp2s0.
```bash
ifconfig
```
> Linux provides a command called ip and it has an option called addr (address). Type ip, a space, addr, and press Enter.
```bash
ip addr
```
- The IP address (e.g., 192.168.233.133) will follow immediately after inet.
- We will use netdiscover to scan all the ip addresses range
```bash
netdiscover -r 192.168.1.1/24
```
- If we connect a wifi adapter then we can connect to Wifi from the VM of Kali linux and make a scan with the IP address of wlan0

### Steps to use Zenmap

- We open zenmap
```bash
zenmap
```
- We will enter the IP we want to scan and it will show us the nmap code for the profile you choose
<img width="803" alt="image" src="https://github.com/user-attachments/assets/c1be386f-f06e-410b-93fe-f71286488ee4" />

<img width="785" alt="image" src="https://github.com/user-attachments/assets/9abeb0f6-83c8-4b3a-9f72-d90feac5406d" />

- A ping scan in Zenmap is a quick way to discover active hosts on a network by sending ICMP echo requests (ping packets).
- Quick Scan in Zenmap (or Nmap) is designed to rapidly scan a network or individual host to identify open ports and services without performing a deep inspection.
- Quick Scan Plus
This is an Nmap scan profile that performs a slightly more thorough scan compared to a regular "Quick Scan." Here's what it does: Scans the top 1000 TCP ports.
Detects service versions (using -sV). Enables OS detection (using -O). Performs a traceroute (using --traceroute).
