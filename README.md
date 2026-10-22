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
<img width="670" height="471" alt="image" src="https://github.com/user-attachments/assets/9a4215b9-2d43-48ae-977c-50f41a18883f" />
<br>
<br>
Right click on Ethernet and go to properties section.
<br>
<br>
<img width="274" height="334" alt="image" src="https://github.com/user-attachments/assets/1496ef92-eceb-4d08-86ad-9943cc51be58" />
<br>
<br>
Go to the Properties tab and double-click Internet Protocol Version 4 (TCP/IPv4). Configure the settings according to your network architecture, then click OK.
<br>
<br>
<img width="876" height="465" alt="image" src="https://github.com/user-attachments/assets/81b69dfa-0f55-460a-8c2c-78935d668f12" />
<br>
<br>
Now You can see here my static IP
<br>
<br>
<img width="524" height="325" alt="WhatsApp Image 2026-10-21 at 2 16 45 AM" src="https://github.com/user-attachments/assets/f8d76424-6fd1-48a1-8d5b-58b042aceeac" />
<br>
<br>
<br>

# Installing/Configuring Sysmon and Splunk on the Windows 10 Target VM & Windows Server VM.
<br>
<br>
Step 10:- Download Splunk Universal Forwarder
<br>
<br>
<img width="822" height="295" alt="WhatsApp Image 2026-10-21 at 10 22 24 AM" src="https://github.com/user-attachments/assets/8bb10770-8970-48d5-9a06-2ed0fdbdd744" />
<br>
<br>
Click Customize next.
<br>
<br>
<img width="493" height="383" alt="WhatsApp Image 2026-10-21 at 10 25 47 AM" src="https://github.com/user-attachments/assets/fbf20e2c-4636-4ae1-a0f7-560cfe556ea5" />
<br>
<br>
Step 11:- Set Username password for splunk Forwarder.
<br>
<br>
<img width="491" height="384" alt="WhatsApp Image 2026-10-21 at 11 48 31 AM" src="https://github.com/user-attachments/assets/c0dd475d-96aa-4d57-b711-b31886d053d5" />
<br>
<br>
Step 12:- Set IP and default port
<br>
I set here my splunk server IP
<br>
<br>
<img width="490" height="386" alt="WhatsApp Image 2026-10-21 at 11 53 14 AM" src="https://github.com/user-attachments/assets/9e00eef0-cf25-4df0-b64a-60f61a40eb0c" />
<br>
<br>
Click Install
<br>
<br>
<img width="495" height="384" alt="WhatsApp Image 2026-10-21 at 11 53 48 AM" src="https://github.com/user-attachments/assets/b5e0dbd1-8582-452f-b37b-8787cae81543" />
<br>
<br>

# Installing and configuring Sysmon
<br>
<br>

**🔍What is Sysmon?**

<br>

When installed, **Sysmon** can log events like:

- **Process creation**
- **Network connections**
- **File creation**
- **Registry changes**
- **Process injection**

<br>
<br>
Step 13 :- Download Sysmon
<br>
<br>
<img width="591" height="422" alt="WhatsApp Image 2026-10-21 at 12 08 43 PM" src="https://github.com/user-attachments/assets/d57e523d-8caf-482a-8ee3-9a82a2862338" />
<br>
<br>

By default, _Sysmon_ does not record many events. To monitor more system activities, you need a proper configuration file.
<br>
<br>

# 🛠️ What is OLAF Config?
<br>
OLAF config is a custom configuration file created by security expert Olaf Hartong. It tells Sysmon exactly what to log, and how to log only useful events while ignoring unnecessary ones.
<br>
<br>

# 🔑 Why is OLAF config important?
<br>

### Without a Configuration File

- Sysmon logs only basic events by default.
- Many important attack activities may go undetected.
- Excessive or irrelevant logs can make threat detection difficult.

### With the OLAF Configuration File

- Captures important attack behaviors, such as PowerShell abuse and privilege escalation.
- Maps logged events to **MITRE ATT&CK techniques** used by attackers.
- Improves threat detection and alerting in tools like **Splunk** and other **SIEMs**.

<br>
<br>

Step 14: Search for the Sysmon Olaf configuration file on GitHub and download it.
<br>
<br>
>
> *config file for Sysmon:* https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml
<br>
<br>
<img width="965" height="467" alt="WhatsApp Image 2026-10-21 at 5 03 35 PM" src="https://github.com/user-attachments/assets/b0e26e84-46f6-446a-9990-09954907b4a3" />
<br>
<br>
Step 15:- Extract the Sysmon ZIP file and rename the downloaded configuration file to sysmonconfig.xml within the same folder.
<br>
<br>
<img width="871" height="361" alt="WhatsApp Image 2026-10-21 at 5 07 01 PM" src="https://github.com/user-attachments/assets/ae649c13-4389-4fee-aa3f-aa0dd5ee4d15" />
<br>
<br>
Step 16: Open Command Prompt and apply the configuration file using the command below.<br>
sysmon64.exe -c sysmonconfig.xml
<br>
<br>
<img width="647" height="299" alt="WhatsApp Image 2026-10-21 at 5 13 20 PM" src="https://github.com/user-attachments/assets/09a69c61-9ec8-4f69-900f-4ad71514e40c" />
<br>
<br>
Step 17:- Open Command Prompt as Administrator, navigate to the Sysmon folder, and install Sysmon with the configuration file.<br>
sysmon64.exe -i sysmonconfig.xml
<br>
<br>
<img width="956" height="463" alt="WhatsApp Image 2026-10-21 at 5 19 17 PM" src="https://github.com/user-attachments/assets/8920fc1b-ddca-4bd7-9a76-9f78d24fdfff" />
<br>
<br>
Step 18: Open PowerShell and verify that the Sysmon service is running.
<br>
<br>
<img width="580" height="260" alt="WhatsApp Image 2026-10-21 at 5 23 11 PM" src="https://github.com/user-attachments/assets/44996457-6654-421a-b974-8fc170735b16" />
<br>
<br>
Step 19:- Navigate to the Splunk Universal Forwarder configuration folder and create the
inputs.conf file.<br>

```yaml
C:\Program Files\SplunkUniversalForwarder\etc\system\local
```
<br>
<br>
<img width="778" height="328" alt="WhatsApp Image 2026-10-22 at 2 16 36 PM" src="https://github.com/user-attachments/assets/31df9de1-2001-440e-9a2a-5703ca62bd37" />
<br>
<br>
Step 19:- in inputs.conf file paste this.
<br>
<br>

```yaml
[WinEventLog://Security]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:Security
renderXml = false
[WinEventLog://System]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:System
renderXml = false
[WinEventLog://Application]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:Application
renderXml = false
[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index = sysmon
sourcetype = XmlWinEventLog:Microsoft-WindowsSysmon/Operational
renderXml = true

```
<br>
<br>
<img width="467" height="440" alt="WhatsApp Image 2026-10-22 at 2 18 45 PM" src="https://github.com/user-attachments/assets/53cbe0dd-66b7-4c9a-aa8b-0ba2659d6d30" />
<br>
<br>
This configuration is used in Windows Server to collect important Windows Event Logs and send them to a SIEM like Splunk, usually through the Splunk Universal Forwarder.
<br>
<br>

## 🔹 Explanation

- `[WinEventLog://Application]` – Collects application-related logs, such as crashes and errors.
- `[WinEventLog://Security]` – Collects security logs, such as login attempts and user account changes.
- `[WinEventLog://System]` – Collects system logs, such as shutdowns and service issues.
- `[WinEventLog://Microsoft-Windows-Sysmon/Operational]` – Collects Sysmon logs, which are essential for detecting attacker activities, such as process creation and network connections.

All logs are sent to the `endpoint` index in Splunk.

`renderXml = true` ensures that logs are collected in XML format, providing detailed event information and supporting MITRE ATT&CK mapping.
<br>
<br>
Step 20:-Press Win + R, type `services.msc`, and press Enter. In the Services window, search for SplunkForwarder.
<br>
<br>
<img width="857" height="294" alt="WhatsApp Image 2026-10-22 at 2 30 36 PM" src="https://github.com/user-attachments/assets/6ef772ad-0b21-484d-a11b-ff94b050c743" />
<br>
<br>






















