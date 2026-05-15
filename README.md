# Packet_Analysis_with_WireShark
Cybersecurity lab project demonstrating packet analysis, network protocol forensics, scan detection, and traffic inspection using Wireshark, Kali Linux, and VirtualBox.

Wireshark Network Protocol Analysis — Cybersecurity Lab Project
Tools Used: Wireshark · Kali Linux · windows · VirtualBox
Lab Environment: Isolated virtual network (Kali attacker + Ubuntu target)
Purpose: Deep packet analysis of core network protocols — understanding traffic from both attacker and defender perspectives
________________________________________
About This Project
This project documents hands-on Wireshark packet capture and analysis across 5 core network protocols. Each lab was performed in a controlled virtual environment using Kali Linux and Ubuntu VMs. The goal is to understand how protocols behave at the packet level, what attackers can extract from unprotected traffic, and how defenders can identify suspicious patterns.
This is not a theoretical exercise — every screenshot, filter, and finding comes from live captures performed on real traffic between virtual machines.
________________________________________
Lab Index
#	Lab	Protocol	Key Skill Demonstrated
1	TCP Three-Way Handshake & Flag Analysis
TCP	Connection lifecycle, flag forensics
2	ICMP Ping & Echo Analysis
ICMP	Network recon detection
3	UDP & DNS Traffic Analysis
UDP / DNS	DNS query inspection, data exfiltration vectors
4	HTTP vs HTTPS — Plaintext vs Encrypted
HTTP / TLS	Credential exposure, encryption importance
5	Nmap Scan Signature Detection
TCP / ICMP	Attack traffic recognition, IDS logic
ARP Spoofing Lab — Coming soon (Lab 6). Environment: Kali performing arpspoof against Ubuntu gateway, captured in Wireshark.
________________________________________







Lab Environment Setup
┌─────────────────────────────────────────────┐

│           VirtualBox Host-Only Network       │

│                                             │

│   ┌──────────────┐      ┌──────────────┐   │

│   │  Kali Linux  │◄────►│   Ubuntu     │   │

│   │  (Attacker)  │      │   (Target)   │   │

│   │ 192.168.x.x  │      │ 192.168.x.x  │   │

│   └──────────────┘      └──────────────┘   │

└─────────────────────────────────────────────┘
Both VMs on the same host-only adapter — traffic is fully capturable by Wireshark running on either machine.
________________________________________
Tools & Commands Reference
Tool	Purpose
wireshark	GUI packet capture and analysis
tcpdump	CLI packet capture
ping	Generate ICMP traffic
nslookup / dig	Generate DNS/UDP traffic
curl http://	Generate HTTP traffic
nmap	Generate scan signatures
apache2	Host HTTP server on Ubuntu
________________________________________
Key Wireshark Filters Used Across Labs
tcp                          # All TCP traffic
tcp.flags.syn == 1           # SYN packets only
tcp.flags.reset == 1         # RST packets (connection resets)
icmp                         # All ICMP traffic
udp.port == 53               # DNS traffic
dns                          # DNS queries and responses
http                         # HTTP only (not HTTPS)
tls                          # TLS/HTTPS handshakes
tcp.port == 80               # HTTP port
tcp.port == 443              # HTTPS port
________________________________________
What I Learned
•	How the TCP three-way handshake works at the byte level and what each flag means to an attacker
•	How ICMP reveals network topology and can be used for OS fingerprinting
•	How DNS queries are sent in plaintext over UDP, enabling traffic interception and DNS spoofing
•	Why HTTP is dangerous — credentials, form data, and session cookies are fully visible in Wireshark
•	How TLS/HTTPS hides application data while still leaking metadata
•	How to identify Nmap scan types from flag patterns — the exact signatures an IDS looks for
________________________________________
Security Mindset
Every lab in this project is analyzed from two perspectives:
•	Red Team (Attacker): What can be extracted, spoofed, or exploited?
•	Blue Team (Defender): What does this look like in logs? How would an IDS detect it?
________________________________________
Repository Structure
wireshark-network-analysis/
├── README.md                        ← This file
├── labs/
│   ├── 01_TCP_Analysis.md
│   ├── 02_ICMP_Analysis.md
│   ├── 03_UDP_DNS_Analysis.md
│   ├── 04_HTTP_HTTPS_Analysis.md
│   └── 05_Nmap_Scan_Signatures.md
└── screenshots/
    ├── tcp/
    ├── icmp/
    ├── dns/
    ├── http_https/
    └── nmap/
________________________________________
 Author
[Manoj Kumar]

________________________________________
All labs performed in an isolated virtual environment for educational purposes only.

