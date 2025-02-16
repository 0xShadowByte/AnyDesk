# Home Lab Simulation: Secure RDP Access & Incident Investigation Using Azure Sentinel

## Objective

This home lab simulation focuses on setting up an Azure Virtual Machine (VM) with secure Remote Desktop Protocol (RDP) access, leveraging Azure Sentinel to monitor and investigate RDP login attempts, and implementing basic security measures to protect against unauthorized access. You will deploy a Windows-based VM in Azure, configure Network Security Group (NSG) rules to allow only trusted IP addresses, and integrate the VM with Azure Sentinel to track authentication events. Additionally, you will create alert rules to detect failed login attempts, investigate security logs, and apply best practices for securing remote access. By the end of this lab, you will have hands-on experience in remote access management, security monitoring, and incident response, which are essential skills for IT support and cybersecurity roles.

## Skills Learned

- Configuring and securing Remote Desktop Protocol (RDP) access in Azure
- Deploying and managing a Windows Virtual Machine (VM) on Azure
- Using Network Security Groups (NSG) rules to restrict unauthorized access
- Integrating Azure Sentinel for real-time security monitoring and log analysis
- Investigating RDP login attempts using Windows Event Viewer & Log Analytics
- Creating alert rules to detect multiple failed RDP login attempts (Event ID 4625)
- Implementing best practices for securing remote access, such as Azure Bastion, Multi-Factor Authentication (MFA), and 
  Just-In-Time (JIT) VM access
- Strengthening incident response skills by analyzing security logs and mitigating potential threats

## Tools/Programs Used

- Azure Sentinel
- Azure Bastion

### Step 1: Create a Virtual Machine on Azure

Login to Azure portal and navigate to Virtual Machines then click create. Select Windows Server 2022 or Windows 10/11. Set up an admin username and password and under networking, ensure that RDP (Port 3389) is enabled the click review + create and waite for the deployment to complete.

*Ref 1-2: Creating a VM on Azure*

![image](https://github.com/user-attachments/assets/1aeff27d-269c-466d-9251-c0ba831f0ed2)

![image](https://github.com/user-attachments/assets/149d5a65-e415-46b0-963b-b721b31328bd)

### Step 2: Secure the RDP Access

Navigate to the VM's Networking settings and modify the NSG (Network Security Group) rules to 1.) restrict Inbound RDP (TCP 3389) access to your public IP only and 2.) Disable RDP access from 'Any' IPs for security. 

To clarify on the first portion of the excerise, restrict Inbound RDP access to your public IP only. To edit the RDP rule to allow only your public IP you first first click on the exisitng RDP rule (Port 3389, Allow) to modify it. Under source change: (source - IP Addresses, Source IP Addresses/CIDR: enter your public IP address, Destination: Any, Service: RDP (3389), Action: Allow, Priority: Keep the existing priority or lower number for higher priority, Name: Update the name if necessary, e.i. Allow-RDP-MyIP) then click save to apply changes. Enable Azure Bastion for a more secure alternative to direct RDP.

*Ref 3-4: securing RDP access*

![image](https://github.com/user-attachments/assets/48154030-d742-4804-933c-20d884e692b1)

![image](https://github.com/user-attachments/assets/26abf40e-8f59-419c-99ad-7e7596773302)

### Step 3: Connect to the VM via RDP

Open Remote Desktop Connection (mstsc.exe) and enter the VM's Public IP Address. Log in using the Admin credentials set eariler. Once connected, open Event Viewer and navigate to Windows Logs > Security > Event ID 4624 (Successful Logins). Event ID 4625 (Failed Logins). Use Bastion RDP to login if the first method fails.

*Ref 5-6: Connect to VM via RDP*

![image](https://github.com/user-attachments/assets/b4e129f4-b5f6-45c5-b785-3a19aa722931)

![image](https://github.com/user-attachments/assets/fa5a6ced-11e9-430c-86dd-62941b798851)

### Step 4: Intergrate the VM with Azure Sentinel for RDP Monitoring

Enable Azure Sentinel by going to Microsoft Sentinel and create a Sentinel workspace. Connect Log Analytics to the VM by attaching the VM to a log analytics workspace and enable windows security event logs collection. Create an alert rule for RDP access attempts by going to analytics > create rule, set condition: EventID 4625 (Failed RDP login) and configure an email alert for multiple failed login attempts.

![image](https://github.com/user-attachments/assets/efd2173c-1515-4612-b1fe-f88ef1d92e08)


### Step 5: Simulate an RDP Security Incident

Attempt muple failed logins (use wrong credentials). Check Windows Event Viewer for failed login attempts. Open Azure Sentinel to review logs in Log Analytics. Identify the failed login events and generate an incident report.

### Step 6: Document Findings and Remediation Steps
Summarize who attempted access, from where, and when. Identify if it was a brute force attempt or a misconfigured account.
Suggest mitigation strategies (e.g., enable MFA, restrict RDP to VPN users only)






