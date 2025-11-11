# Setup-and-Configuration-of-pfSense-Firewall
The Setup and Configuration, and management of a pfSense Firewall (network-based firewall) in a virtualized lab environment

OBJECTIVE:

The goal of this project is to simulate a real world enterprise network, focusing on network segmentation, traffic filtering and monitoring, with probable VPN configuration.

TOOLS:

- pfSense (from Netgate)
- VirtualBox (Hypervisor)
-Kali Linux (for offensive testing)
- Ubuntu (as client machine)
-Wireshark
-SSH/WebGUI

NETWORK TOPOLOGY:

[Internet] ------> WAN ----> [pfSense] ----> LAN -----> [Ununtu (internal network)]
                         
- WAN Interface: This will be connected to the external network using NAT (Network Address Translation)
- LAN Interface - the network access will be set to Intnet (Internal Network).

STEP-BY-STEP SETUP:

- Installation:

1. Download the pfSense ISO from
    https://www.pfsense.org/download/.
2. Create a Virtual Machine with:
      - 2 Network Adapters:
         *Adapter 1 (WAN): NAT
      *Adapter 2 (LAN): Internal Network 
3. Boot from the ISO and follow the installation wizard
4. Assign interfaces:
      -WAN ---> em0
      - LAN ----> em1
5. Access the WebGUI via the Internal (ubuntu) browser. (its important to note that pfSense won't allow access to the WebGUI from the WAN side)
       https://192.168.1.1
       username: admin
       password: pfsense

 - Basic Configuration:

1. Change default admin and password
2. Configure hostname and DNS
3. Enable NTP service
4. Update packages

- Firewall Rules:

1. Allow LAN ---> Any (default)
2. Block WAN inbound traffic
3. Create specific allow rules for SSH, HTTP or ICMP as needed
      e.g
      Action:  Pass
      Interface:  WAN
      Protocol:  TCP
      Source:   any
      Destination:  WAN address
      Destination Port:  22 (SSH)
      Description:  Allow SSH from trusted IP

- DHCP & NAT

1. Enable DHCP Server on LAN (e.g 192.168.1.100 - 192.168.1.200)
2. Verify NAT is auto enabled for outbound traffic

- Monitoring & Logs

1. Enable Dashboard widgets for WAN/LAN traffic
2. View Firewall Logs under Status ---> System Logs ---> Firewall
3. Use Wireshark on LAN client (Ubuntu) for packet inspection


TESTING SCENARIOS

- Ping WAN IP from LAN: (Success)
- Ping external IP  (e.g 8.8.8.8): (Success) 
- Try accessing blocked service e.g port 23: (Blocked)
- Generate firewall log for denied traffic.: (Visible inlogs)

VPN SETUP

- Configure OpenVPN server for remote access
- Export client configuration file and test connectivity


Author: 
Name: Olumide Akinokun
Role: Cybersecurity Analyst
LinkedIn:  www.linkedin.com/in/akinokun-olumide
