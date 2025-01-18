# DoS-Attack-RMIT-Cybersecurity-Project
One of the Red teaming activities for my RMIT Cybersecurity Project

## Objective

- Use Ettercap from Kali Linux to launch DoS attack against the target
- Verify the successful attack using Wireshark

## The Scenario

![red team lab nmap](https://github.com/user-attachments/assets/092e32ce-cdae-4509-8172-231a3503be58)

*Figure 1: In this follow-up scenario, the attacker has successfully scan the network using nmap and found several host with open TCP ports.*

## Lab Setup

![nmap scan red team](https://github.com/user-attachments/assets/b2a83336-6849-4f89-84b0-6fa195d3352a)

*Figure 2: We still use the same setup from my [Nmap Scan Lab](https://github.com/Kazu010101/Nmap-Scan-RMIT-Cybersecurity-Project/blob/main/README.md), in which 2 Virtual Machines were used for the victim in Windows 10 (192.168.1.254 /24) and the attacker in Kali Linux (192.168.1.33 /24).* 

## DoS Attack using Ettercap

Once verified that both machines could ping each other, the following Dos Attack is conducted by following these steps:
- **Launch Ettercap**: From the terminal, type *sudo Ettercap -G* and input password
- **Select Network Interface**: in this lab, I choose eth0. Next, click the tick icon on top right of the interface.

![ettercapg](https://github.com/user-attachments/assets/4a10ed0d-5cf4-48f4-8a1f-e1b43ed6f066)

*Figure 3: launching ettercap from Kali Linx Terminal, and choosing the network interface.*

- **Select DoS Attack plugins**: Click the 3 dots menu icon on top right > Plugins > Manage Plugins > double click dos_attack from the list.

![ettercap steps](https://github.com/user-attachments/assets/a4918a11-481f-46ba-ae55-79547a2b7481)

*Figure 4: selecting the dos attack from Ettercap plugins*

- **Insert Victim's IP Address** : 192.168.1.254 > Enter 
- **Insert Unused IP** : 192.168.1.222 (This is because no Host has this address based on Nmap Scan) > Enter

![ettercaptgt](https://github.com/user-attachments/assets/13a350a1-942c-482d-8cd6-ddabe976c372)

*Figure 5: Once the Victim's IP and Unused IP are entered, press enter to the attack.*

- **Stop the attack** :To stop the Dos Aattack, double click on the dos_attack plugins list.

![ddoossaattcck](https://github.com/user-attachments/assets/332304b3-7f13-45a5-b0ba-4390ffd77934)

*Figure 6: Prompts showing the attack is started (1). Double clicking the dos_attack plugins list will stop the attack (2).*

## Verifying the DoS attack using Wireshark

While the Ettercap DoS attack was proceeding, we opened Wireshark from Kali (can also be alternatively done from Windows 10 but required prior Wireshark installation) and captured the traffic on eth0 network interface.

![wiresharkdos](https://github.com/user-attachments/assets/d263811a-35d2-4d58-aa3d-a42e21f69b63)

*Figure 7: Verification that the DoS attack has been succesfully conducted on Wireshark.*

## Result

The Wireshark pcap log from this lab verifies the successful DoS attack. The repeated TCP Packets with of RST, ACK flags across multiple packets, especially in a short time span, suggests that the victim (192.168.1.254) is being overwhelmed with connection attempts or resets by the attacker (192.168.1.33).

## Mitigation Plan

- The Office Network needs to be subnetted into at least two subnets, each seperately for the internal staff and the guest network.
- Additional security tools such as IPS and firewalls are required to protect internal staff network from malicious traffic originiating from outside and guest network.
- Turn on the Windows Firewall on Windows 10.
