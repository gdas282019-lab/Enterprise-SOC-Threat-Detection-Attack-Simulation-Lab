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

# 🔑 Why is OLAF config important?
<br>
OLAF config is a custom configuration file created by security expert Olaf Hartong. It tells Sysmon exactly what to log, and how to log only useful events while ignoring unnecessary ones.<br>

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
 By default, the Log On As account is set to NT Service.
<br>
<br>
<img width="396" height="466" alt="WhatsApp Image 2026-10-22 at 4 59 37 PM" src="https://github.com/user-attachments/assets/b9217178-d00f-40b1-9d31-10ea9ab181fc" />
<br>
<br>
Step 21: Change the Log On As option to This account, then restart the SplunkForwarder service.
<br>
<br>
<img width="416" height="475" alt="WhatsApp Image 2026-10-22 at 5 02 43 PM" src="https://github.com/user-attachments/assets/519234ac-4cb3-4217-9658-5ccb562011a8" />
<br>
<br>
<img width="555" height="268" alt="WhatsApp Image 2026-10-22 at 5 03 35 PM" src="https://github.com/user-attachments/assets/6a6daaac-34a0-400a-aa13-c928989760cd" />
<br>
<br>
`Now You can see my changes`
<br>
<br>
<img width="1044" height="100" alt="WhatsApp Image 2026-10-22 at 5 04 37 PM" src="https://github.com/user-attachments/assets/0d7f3294-4866-4ff5-9739-c12748e4873b" />
<br>
<br>
Now, Sysmon and Splunk Universal Forwarder are installed and configured with the updated configuration file.
<br>
<br>
Step 22: On the Splunk server, go to Settings → Indexes to create an index for storing endpoint logs. Then, navigate to Settings → Forwarding and Receiving → Configure Receiving to enable the receiving port for incoming logs.
<br>
<br>
<img width="611" height="302" alt="WhatsApp Image 2026-10-22 at 5 17 44 PM" src="https://github.com/user-attachments/assets/e7bf8453-8694-4335-a765-e784a4a1a253" />
<br>
<br>
You can see this all indexes click on new indexes
<br>
<br>
<img width="1360" height="376" alt="WhatsApp Image 2026-10-22 at 5 20 06 PM" src="https://github.com/user-attachments/assets/a259737d-fadb-4fe6-983a-0fea321701e0" />
<br>
<br>
 Create a new index named wineventlog, then create a second index named sysmon,
and save both.
<br>
<br>
<img width="585" height="425" alt="WhatsApp Image 2026-10-22 at 7 08 17 PM" src="https://github.com/user-attachments/assets/10f82123-12bc-4a34-abd2-6a216ad08b6a" />
<br>
<br>
<img width="461" height="429" alt="WhatsApp Image 2026-10-23 at 1 08 15 AM" src="https://github.com/user-attachments/assets/a761e57f-34c7-45e2-b71a-537d645a00fb" />
This is my indexes.
<br>
<br>
<img width="1148" height="60" alt="WhatsApp Image 2026-10-23 at 1 10 05 AM" src="https://github.com/user-attachments/assets/beca2874-793c-47ca-8593-2bc0ee872ec6" />
<br>
<br>
now we enable our splunk server to recieve our data.<br>
click on settings forwarding and recievings.
<br>
<br>
<img width="1036" height="209" alt="image" src="https://github.com/user-attachments/assets/f6436dd5-ceb0-40b6-ad35-759f3b8c7f9b" />
<br>
<br>
This is the default port hit save
<br>
<br>
<img width="1363" height="253" alt="WhatsApp Image 2026-10-22 at 5 40 31 PM" src="https://github.com/user-attachments/assets/e40d4819-dbc4-4076-a9fe-867cb03d705e" />
<br>
<br>
Go the top select search and reporting
<br>
<br>
<img width="360" height="367" alt="WhatsApp Image 2026-10-22 at 6 17 14 PM" src="https://github.com/user-attachments/assets/e8b2f275-a544-410b-81f6-63193fd29e76" />
<br>
<br>
Run the following SPL query to identify user account creation events (Event Code
4720) across all indexes.<br>
index=sysmon EventCode=7040
<br>
<br>
<img width="1362" height="491" alt="WhatsApp Image 2026-10-23 at 1 25 50 AM" src="https://github.com/user-attachments/assets/aebaf3ec-4d8d-4f49-916b-c3fb51ae6043" />
<br>
<br>
**Repeat the same process to install and configure Sysmon and Splunk Universal Forwarder on the Target Windows VM.**
<br>
<br>
After successfully installing and configuring Splunk Universal Forwarder and Sysmon on the Target PC, you should be able to see two hosts in the Splunk search results.
<br>
<br>
<img width="1333" height="253" alt="WhatsApp Image 2026-10-23 at 1 44 40 AM" src="https://github.com/user-attachments/assets/8c1857e7-e9bb-42bc-acfc-beec438c717f" />
<br>
<br>
# Active Directory Setup

## 1. Install and Configure Windows Server 2022

Install and configure Windows Server 2022 to prepare the environment for Active Directory.

## 2. Promote the Server to a Domain Controller

Install the **Active Directory Domain Services (AD DS)** role and promote the server to a domain controller.

## 3. Join the Target Windows PC to the Domain

Join the target Windows PC to the newly created Active Directory domain.

## 4. Configure a Static IP Address

Step 23:- First, configure a static IP address on the Windows Server.

- Click the **Network** icon in the taskbar.
- Open **Network & Internet settings**.
- Navigate to the network adapter settings.
- Configure the IPv4 address, subnet mask, default gateway, and preferred DNS server as required.
<br>
<br>
<img width="361" height="140" alt="WhatsApp Image 2026-10-23 at 1 19 34 AM" src="https://github.com/user-attachments/assets/5e3b3da8-3f78-440f-95e0-37585dab6924" />
<br>
<br>
click on change adapter option.
<br>
<br>
<img width="432" height="269" alt="WhatsApp Image 2026-10-23 at 1 30 07 AM" src="https://github.com/user-attachments/assets/47720369-9ecb-4f79-b3ea-593124fbd8a1" />
<br>
<br>
set static ip
<br>
<br>
<img width="405" height="456" alt="WhatsApp Image 2026-10-23 at 1 58 20 AM" src="https://github.com/user-attachments/assets/26b2e573-dc38-40b4-b933-c6d6a8492073" />
<br>
<br>
see the ip of machine
<br>
<br>
<img width="521" height="484" alt="WhatsApp Image 2026-10-23 at 2 00 00 AM" src="https://github.com/user-attachments/assets/eb3fa42b-ed00-4d76-b494-ce38c46334de" />
<br>
<br>
Step 24:- Go to Server Manager and click add role.
<br>
<br>
<img width="846" height="345" alt="WhatsApp Image 2026-10-23 at 2 03 21 AM" src="https://github.com/user-attachments/assets/5b52fa82-1903-4f8f-bba7-6e121cbc56dd" />
<br>
<br>
select accordings to the diagram click on next.
<br>
on Server roles section click add features. and click next upto confirmation then hit install
<br>
<br>
<img width="1082" height="525" alt="image" src="https://github.com/user-attachments/assets/5d61133c-29d9-4cd5-a495-469d0814e11b" />
<br>
<br>
After end of install you can see this.
<br>
<br>
<img width="786" height="559" alt="WhatsApp Image 2026-10-23 at 2 27 34 AM" src="https://github.com/user-attachments/assets/f724404f-12ca-4b84-aa51-8a4db37c8c85" />
<br>
<br>
Then click on triangle means danger sign and click on blue painted.
<br>
<br>
<img width="673" height="358" alt="WhatsApp Image 2026-10-23 at 2 29 24 AM" src="https://github.com/user-attachments/assets/e21c9802-b586-4d7c-a6fb-c6f5318279e5" />
<br>
<br>
Step 24:- Set our new domain **mydfir.local**.
<br>
<br>
<img width="760" height="557" alt="WhatsApp Image 2026-10-23 at 10 32 12 AM" src="https://github.com/user-attachments/assets/23df3771-fc95-4882-b7d2-1e89d8770840" />
<br>
<br>
set password for Domain Controller.
<br>
<br>
<img width="747" height="551" alt="WhatsApp Image 2026-10-23 at 10 35 16 AM" src="https://github.com/user-attachments/assets/8057f471-9000-4846-a24d-06bb07f5b9d7" />
<br>
<br>
after click on next,next,next and install it then restart the system.
<br>
you can see my domain name.
<br>
<br>
<img width="1364" height="612" alt="WhatsApp Image 2026-10-23 at 1 50 27 PM" src="https://github.com/user-attachments/assets/15826868-ba57-4f80-aaeb-2f6958814145" />
<br>
<br>
click on blue painted to add user and group.
<br>
<br>
<img width="1247" height="280" alt="WhatsApp Image 2026-10-23 at 1 59 25 PM" src="https://github.com/user-attachments/assets/19da5bf4-0c61-49e2-b624-757625ac6b8f" />
<br>
<br>
right click on domain click on new then click organizatonal unit.
<br>
<br>
<img width="757" height="527" alt="WhatsApp Image 2026-10-23 at 2 01 27 PM" src="https://github.com/user-attachments/assets/717e1d5a-702c-4608-b8a6-965f174932ff" />
<br>
<br>
Give the name IT
<br>
<br>
<img width="440" height="378" alt="WhatsApp Image 2026-10-23 at 2 02 46 PM" src="https://github.com/user-attachments/assets/0633ee2c-6914-46fe-9d05-f06411e0eb5e" />
<br>
<br>
Fill the Details of New User.
<br>
<br>
<img width="440" height="371" alt="WhatsApp Image 2026-10-23 at 2 04 16 PM" src="https://github.com/user-attachments/assets/d5c768eb-1544-4621-bff0-7e9c9ffc5e03" />
<br>
Set Password for User gdas.
<br>
<br>
<img width="436" height="366" alt="WhatsApp Image 2026-10-23 at 2 08 28 PM" src="https://github.com/user-attachments/assets/4c7e5508-025d-4984-a378-04ec6f48213b" />
<br>
<br>
Create another **Organizational Unit** _HR_.
<br>
<br>
<img width="723" height="500" alt="WhatsApp Image 2026-10-23 at 2 15 11 PM" src="https://github.com/user-attachments/assets/ef3dec98-f037-426f-8a83-cdb8da469b33" />
<br>
<br>

# Now we move the target Windows machine to join our newly Domain created mydfir.local.
<br>
Go to **Network & Internet Settings**  then click change Adapter option.
<br>
<img width="900" height="567" alt="WhatsApp Image 2026-10-23 at 2 22 16 PM" src="https://github.com/user-attachments/assets/e6149c43-b5ef-44ae-a8e0-df1a07760da3" />
<br>
<br>
Change the DNS Server.
<br>
<br>
<img width="1356" height="601" alt="WhatsApp Image 2026-10-23 at 2 25 18 PM" src="https://github.com/user-attachments/assets/3fde0879-a0c8-4c0b-9c64-ef193e0e5feb" />
<br>
<br>
Now you can see my New IP configuration.
<br>
<br>
<img width="770" height="456" alt="WhatsApp Image 2026-10-23 at 2 28 05 PM" src="https://github.com/user-attachments/assets/0b35da46-a034-4727-a5df-b74aa45fb22c" />
<br>
<br>

Since *Windows 10 Home Single Language*  Edition does not support joining a domain, we need to upgrade it to Windows 10 Pro.
<br>
<br>
<img width="443" height="272" alt="WhatsApp Image 2026-10-23 at 3 00 51 PM" src="https://github.com/user-attachments/assets/c5d22329-29b0-45d1-b27c-4a1763359f8c" />
<br>
<br>
Open powershell run as administrator and type the following command.
<br>
<br>

```yaml
irm https://get.activated.win  | iex
```
<br>
<br>
<img width="469" height="166" alt="WhatsApp Image 2026-10-24 at 9 23 36 PM" src="https://github.com/user-attachments/assets/6cc05a97-734e-48b5-9f61-0a3061b9b179" />
<br>
<br>
you can see this window.
<br>
<br>
<img width="579" height="525" alt="WhatsApp Image 2026-10-24 at 9 24 21 PM" src="https://github.com/user-attachments/assets/bdf62d81-6bad-443b-8527-71018b5b516f" />
<br>
choose [6].
<br>
<br>
Press [2] and hit enter then continue.[1]
<br>
<br>
<img width="790" height="354" alt="WhatsApp Image 2026-10-24 at 9 26 08 PM" src="https://github.com/user-attachments/assets/d17ea665-2a41-4f05-89c1-29daa4a89143" />
<br>
<br>
The System will restart automatically.
<br>
<br>
<img width="1243" height="457" alt="WhatsApp Image 2026-10-24 at 9 30 24 PM" src="https://github.com/user-attachments/assets/1f40072d-6807-416c-995f-ae8c86d3bf8a" />
<br>
<br>
<img width="458" height="414" alt="WhatsApp Image 2026-10-24 at 9 36 04 PM" src="https://github.com/user-attachments/assets/39dd8325-1b62-4e8a-a81e-6c6faba73805" />
<br>
<br>


















