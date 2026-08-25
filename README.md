# Enterprise-SOC-Threat-Detection-Attack-Simulation-Lab
A hands-on Enterprise SOC lab focused on attack simulation, endpoint monitoring, Splunk-based SIEM analysis, threat detection, incident investigation, and MITRE ATT&amp;CK mapping. Built to demonstrate practical SOC workflows and real-world cybersecurity detection techniques.
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/305d8138-5430-408f-b5e3-03dbdbaac226" />

# Summary
This project delivered practical experience in building and securing an enterprise-style cybersecurity environment, with a strong focus on attack simulation, detection, and incident analysis. Key areas include:

- **Enterprise Network Setup:** Designed and configured a virtualized network environment for secure communication between systems.
- **Active Directory Security:** Implemented OUs, user accounts, Group Policies, and RBAC to simulate centralized enterprise identity management.
- **Attack Simulation:** Reproduced real-world adversary behaviors using Kali Linux, Crowbar, and Atomic Red Team to generate security events.
- **SOC Monitoring:** Integrated Splunk for centralized log collection, investigation, and detection of suspicious activities.
- **Threat Mapping:** Analyzed attack activity and mapped observed behaviors to relevant **MITRE ATT&CK TTPs**.
- **Incident Investigation:** Investigated security events and correlated endpoint and network logs to identify suspicious behavior and attack patterns.
- **Security Operations:** Applied practical SOC workflows covering monitoring, detection, analysis, and threat investigation.

# Architecture
<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/0c66808c-2dfb-4b1e-abe9-d39f710d1622" />



I started the project by designing a network architecture diagram to visualize the overall lab environment and understand how each system would communicate. The diagram includes the **Active Directory server, Splunk server, Windows 10 target machine, and Kali Linux attacker machine**, along with their respective roles. Planning the architecture beforehand helped me organize the setup, understand the communication flow, and build the environment in a structured way that reflects a real-world enterprise network.

# Tools & Tech

> *Oracle VirtualBox:* https://www.virtualbox.org/wiki/Downloads
>
> *Server 2022 ISO:* https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
>
> *Windows 10 ISO:* https://drive.google.com/drive/folders/1NpJ5gKg4avlnsQI0WverCuzFix-jPOsK?usp=sharing
>
> *Ubuntu Server 24.04.2 LTS:* https://ubuntu.com/download/server
>
> *Splunk for linux:* https://download.splunk.com/products/splunk/releases/10.2.0/linux/splunk-10.2.0-d749cb17ea65-linux-amd64.deb

Here I setup My all machine.

# Objective

**Install & Configure Sysmon & Splunk on a Windows target machine (Windows Server) to enable centralized log collection, endpoint monitoring, security event analysis, and threat detection within the SOC environment.**

Step 1:- Open virtualbox and go to Network click NAT network.


<img width="463" height="334" alt="image" src="https://github.com/user-attachments/assets/8a27b01b-cb8f-4a5b-9477-30614e6703f4" />

Step 2:- Create a NAT Network. Right-click or press *ctrl+shift+c* and select the ‘Create’ option.

<img width="463" height="334" alt="image" src="https://github.com/user-attachments/assets/be0435dd-fa54-40ae-a838-9a9ff44b14ce" />

Step 3:- Name the NAT network with with following configuration.

<img width="1063" height="334" alt="image" src="https://github.com/user-attachments/assets/3176901e-a180-4cf0-bad2-b594bb337511" />












