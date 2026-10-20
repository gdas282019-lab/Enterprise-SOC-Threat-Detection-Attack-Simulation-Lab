# Enterprise-SOC-Threat-Detection-Attack-Simulation-Lab
<br>
<br>
A hands-on Enterprise SOC lab focused on attack simulation, endpoint monitoring, Splunk-based SIEM analysis, threat detection, incident investigation, and MITRE ATT&amp;CK mapping. Built to demonstrate practical SOC workflows and real-world cybersecurity detection techniques.
<br>
<br>

<img width="500" height="490" alt="image" src="https://github.com/user-attachments/assets/305d8138-5430-408f-b5e3-03dbdbaac226" />

# Summary
This project delivered practical experience in building and securing an enterprise-style cybersecurity environment, with a strong focus on attack simulation, detection, and incident analysis. 

 **Key areas include:**

- **Enterprise Network Setup:** Designed and configured a virtualized network environment for secure communication between systems.
- **Active Directory Security:** Implemented OUs, user accounts, Group Policies, and RBAC to simulate centralized enterprise identity management.
- **Attack Simulation:** Reproduced real-world adversary behaviors using Kali Linux, Crowbar, and Atomic Red Team to generate security events.
- **SOC Monitoring:** Integrated Splunk for centralized log collection, investigation, and detection of suspicious activities.
- **Threat Mapping:** Analyzed attack activity and mapped observed behaviors to relevant **MITRE ATT&CK TTPs**.
- **Incident Investigation:** Investigated security events and correlated endpoint and network logs to identify suspicious behavior and attack patterns.
- **Security Operations:** Applied practical SOC workflows covering monitoring, detection, analysis, and threat investigation.

# Architecture

<img width="1100" height="700" alt="file_000000009ac882118b2eba031c7d34b7" src="https://github.com/user-attachments/assets/044e266d-b1e2-4cfa-a037-13c818c73dc8" />


I started the project by designing a network architecture diagram to visualize the overall lab environment and understand how each system would communicate. The diagram includes the **Active Directory server, Splunk server, Windows 10 target machine, and Kali Linux attacker machine**, along with their respective roles. Planning the architecture beforehand helped me organize the setup, understand the communication flow, and build the environment in a structured way that reflects a real-world enterprise network.

# Key Requirements
> i5 12th gen processor or equivalent.
> 
> 16 gb ram(DDR4)
> 
> 100 gb available storage


# Tools & Tech

> *Oracle VirtualBox:* https://www.virtualbox.org/wiki/Downloads
>
> *Windows Server 2022 ISO:* https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
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

Step 3:- Name the NAT network with this following configuration.

<img width="1063" height="300" alt="image" src="https://github.com/user-attachments/assets/3176901e-a180-4cf0-bad2-b594bb337511" />

Step 4:- The following machines should have at least the specified RAM:

> *kali*----> 3 GB(min)
> 
> *Windows Server*-----> 2gb(min)
> 
> *Ubuntu Server*---->4 gb(min)
> 
> *Windows Client PC*----> 4gb(min)

<img width="300" height="362" alt="image" src="https://github.com/user-attachments/assets/e53aa826-066b-4e35-9ea2-018405e327ba" />

Step 5:-Make sure all four machines are connected to the same NAT Network, **"Ad-project."**

<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/6e6c9b03-9ba2-43b5-9d39-f7e142438b98" />

enable copy paste..............
power on machine go to upper panel.

<img width="697" height="100" alt="image" src="https://github.com/user-attachments/assets/212c5f27-4eb9-4b82-b5b0-cb0e714f6083" />


click devices--> go to shared clipboard-->click Bidirectional

<img width="881" height="356" alt="image" src="https://github.com/user-attachments/assets/82104abc-c198-4a83-9922-e5b65aebe1e6" />


Step 6:- This is the my ip of Ubuntu Server.

<img width="847" height="300" alt="image" src="https://github.com/user-attachments/assets/f0d9ed69-aa20-4525-b68d-f6f8ee2ddb96" />


Now we set our Static IP in Ubuntu that reflect our network ip
<br>
type
<br>
**nano /etc/netplan/00-installer-config.yaml**
<br>
paste this:-

```yaml
network:
    ethernets:
        enp0s3:
            dhcp4: no
            addresses: [192.168.10.10/24]
            nameservers:
                addresses: [8.8.8.8]
            routes:
                - to: default
                  via: 192.168.10.1
    version: 2
```
<br>
<br>

Write the exact same code shown in the image, maintaining proper indentation.

<img width="1056" height="232" alt="image" src="https://github.com/user-attachments/assets/5d9e50e6-9bdb-4d5a-aead-ccb78952a702" />

<br>
<br>

Step 7:- Run this command.
<br>
```yaml
sudo netplan apply
```
<br>
<img width="1284" height="307" alt="image" src="https://github.com/user-attachments/assets/98062c82-027b-42ae-9dc3-9e75361245d3" />
<br>
<br>

My Ping is also work

<img width="809" height="227" alt="image" src="https://github.com/user-attachments/assets/5014901c-ca07-4627-9106-3af2dfa1329f" />

# Instalaltion of Splunk In ubuntu server.
<br>

Step 8:- Now I will download splunk by following this commands.
<br>
```yaml
wget -O splunk-10.2.0-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.2.0/linux/splunk-10.2.0-d749cb17ea65-linux-amd64.deb"
```
<br>
<img width="1302" height="215" alt="image" src="https://github.com/user-attachments/assets/622d8539-aed3-41de-b02a-c5c52ae0eac8" />
<br>
*check the available storage before unpacking.*
<br>

```yaml
df -h /
```
<br>

<br>
<img width="979" height="200" alt="image" src="https://github.com/user-attachments/assets/d23d8f7d-5866-4d9f-9460-5512f1611b5a" />
.

```yaml
 sudo dpkg -i splunk-10.2.0-linux-amd64.deb
```
<br>
<img width="763" height="310" alt="image" src="https://github.com/user-attachments/assets/a6eb9457-4673-470d-b57e-65680f8de2a4" />
<br>
<br>
Here I change my host IP according to the my ubuntu Ip Follow this command
<br>

```yaml
 cd /opt/splunk/etc
nano splunk-launch.conf
BINDIP = 0.0.0.0    #add this line
```
<br>
<img width="612" height="264" alt="WhatsApp Image 2026-10-21 at 1 06 06 AM" src="https://github.com/user-attachments/assets/dfff98b4-2b40-4015-a9f1-c7f1fc2be855" />
<br>
<br>
<br>
Here I can access splunk from windows machine.
<br>
<br>
<img width="884" height="404" alt="WhatsApp Image 2026-10-21 at 1 35 29 AM" src="https://github.com/user-attachments/assets/4601e719-6e83-4466-b64f-06bf7b22cb81" />
<br>
<br>
Step 9: Rename this PC to Target PC.
<br>
<br>
Go to Settings → About, then click Rename this PC.
<br>
<br>
<img width="436" height="87" alt="image" src="https://github.com/user-attachments/assets/b06d574e-3039-4098-bc7e-7019e6de71d4" />
<br>
<br>
<img width="501" height="313" alt="WhatsApp Image 2026-10-21 at 1 48 34 AM" src="https://github.com/user-attachments/assets/6dfa69e4-c36b-4ccb-b105-5946eb07536f" />
<br>
<br>
<br>
Step 10:- Convert dynamic IP to static IPV4.
<br>
<br>
Go to ethernet icon in taskbar--> click Network & Internet Settings.
<br>
<br>
<img width="361" height="150" alt="WhatsApp Image 2026-10-21 at 1 58 41 AM" src="https://github.com/user-attachments/assets/36c77da3-2200-412c-9280-95628eefc04b" />
<br>
<br>
Click Change adapter settings.
<br>
<br>
<img width="1070" height="471" alt="image" src="https://github.com/user-attachments/assets/9a4215b9-2d43-48ae-977c-50f41a18883f" />
<br>
<br>
Right click on Ethernet and go to properties section.
<img width="274" height="334" alt="image" src="https://github.com/user-attachments/assets/1496ef92-eceb-4d08-86ad-9943cc51be58" />
<br>
<br>
Go to the Properties tab and double-click Internet Protocol Version 4 (TCP/IPv4). Configure the settings according to your network architecture, then click OK.
<br>
<br>
<img width="776" height="465" alt="image" src="https://github.com/user-attachments/assets/81b69dfa-0f55-460a-8c2c-78935d668f12" />
<br>
<br>
















