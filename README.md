# DoS-Attack-RMIT-Cybersecurity-Project
One of the Red teaming activities for my RMIT Cybersecurity Project

## Objective

- Use Ettercap from Kali Linux to launch DoS attack against the target
- Verify the successful attack using Wireshark

![red team lab nmap](https://github.com/user-attachments/assets/092e32ce-cdae-4509-8172-231a3503be58)

*Figure 1: In this follow-up scenario, the attacker has successfully scan the network using nmap and found several host with open TCP ports.*

## Lab Setup

![nmap scan red team](https://github.com/user-attachments/assets/b2a83336-6849-4f89-84b0-6fa195d3352a)

*Figure 2: We still use the same setup from my [Nmap Scan Lab](https://github.com/Kazu010101/Nmap-Scan-RMIT-Cybersecurity-Project/blob/main/README.md), in which 2 Virtual Machines were used for the victim in Windows 10 (192.168.1.254) and the attacker in Kali Linux (192.168.1.33).* 


## DoS Attack using Ettercap

Once verified that both machines could ping each other, the following Dos Attack is conducted by following these steps:
- Launch Ettercap: From the terminal, type *sudo Ettercap -G* and input password
- Select Network Interface: in this lab, I choose eth0. Next, click the tick icon on top right.

![ettercapg](https://github.com/user-attachments/assets/4a10ed0d-5cf4-48f4-8a1f-e1b43ed6f066)


*Figure 3: Ettercap is open in GUI mode. Select the network interface, and click the tick icon to confirm*

- nmap -sT -v -p0 192.168.1.5
  
![nmap scan 4](https://github.com/user-attachments/assets/fb9b12fb-1620-4160-a881-e612c702cc80)

*Figure 5: Further scan against 192.168.1.5 discovers open ports on the host.*

-nmap -O 192.168.1.5

![nmap scan 5](https://github.com/user-attachments/assets/12e2ede9-be25-49bd-b7c1-1ccda79c81d0)

*Figure 6: This command scans for the Operating System of the host machine; it identifies the host's OS is Windows 10.*

## Result

The most important information from the nmap scan is that there are 3 open TCP ports, which are 135, 139, and 445. Considering that the target also uses Windows 10 OS, these information suggest that the host is running a file sharing service such as SMB protocol, which can be further exploited by the attacker.

## Mitigation

- The Office Network needs to be subnetted into at least two subnets, each seperately for the internal staff and the guest.
- Additional security tools such as IPS and firewalls are required to protect internal staff network from malicious traffic originiating from outside and guest network.
- Additions of network devices such as pfSense Router is required so that ACL can be set up to prevent the flow of traffic from guest network entering the internal staff network.
- Turn on the Windows Firewall
