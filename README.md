# Setting up a Windows VM in VMware and enable RDP

## Objective

The objective of this project was to set up a Windows virtual machine (VM) in VMware Workstation Pro and enable Remote Desktop Protocol (RDP) for remote access. This involved configuring system settings, adjusting firewall rules, and ensuring a successful connection between the host machine and the VM. Additionally, the project focused on understanding networking fundamentals, troubleshooting potential RDP connection issues, and implementing basic security measures to protect the remote session. By completing this project, learners gained hands-on experience in virtualization, Windows administration, and remote access security.

## Skills Learned

- Virtualization & System Administration – Set up and configured a Windows VM in VMware.
- Networking & Remote Access – Established an RDP session, identified IP addresses, and understood RDP over TCP/IP.
- Windows Security & Firewall Management – Configured firewall rules, enabled Network Level Authentication (NLA), and managed settings via PowerShell.
- Troubleshooting & Problem-Solving – Diagnosed RDP connection issues, tested network connectivity, and analyzed Windows Event Viewer logs.
- RDP Security Hardening – Secured RDP by changing ports, restricting user access, and exploring MFA options.

## Tools
- VMware Workstation Pro 17
- Windows 10 Enterprise

### Step 1: Create a Windows Virtual Machine in VMware

*Ref 1: Installing VMware Workstation Pro*

![image](https://github.com/user-attachments/assets/8d50b58d-bd21-45a1-9cdf-dc19591fa629)

*Ref 2: Installing Windows Server 2022 on VM*

![image](https://github.com/user-attachments/assets/7988407d-4020-4a82-bf5d-3a92a8e6560f)

*Ref 3: Running Windows Server 2022 on VM*

![image](https://github.com/user-attachments/assets/56abd418-f4c4-4b79-b3be-5a8752899f02)

### Step 2: Enable Remote Desktop (RDP) in Windows
Log into the Windows VM.
Open Run (Win + R), type sysdm.cpl, and press Enter.
Go to "Remote" tab and select "Allow remote connections to this computer".
Check "Allow connections only from computers running Remote Desktop with Network Level Authentication" (for security).
Click "Select Users" → Add your Windows user account.
Click Apply > OK.

### Step 3: Configure Firewall to Allow RDP
Open Windows Defender Firewall (Win + R, type firewall.cpl, press Enter).
Click "Allow an app or feature through Windows Defender Firewall".
Scroll down, find "Remote Desktop", and check both Private & Public boxes.
Click OK.
OR, enable RDP via PowerShell:
powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

### Step 4: Find Your VM's IP Address
Open Command Prompt (Win + R, type cmd, press Enter).
Type:
ipconfig
Look for IPv4 Address (e.g., 192.168.1.100).

### Step 5: Connect to the Windows VM via RDP
On your host machine, open Remote Desktop Connection (Win + R, type mstsc, press Enter).
Enter the VM’s IP address (192.168.1.100).
Click Connect and enter your Windows VM username & password.
Click OK, and you should be connected! 🎉

### 🔐 Bonus: Secure Your RDP Setup
✅ Change RDP Port (Default 3389 → Custom Port):

powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -Name PortNumber -Value 3390
✅ Disable RDP for non-admin users using Group Policy (gpedit.msc).
✅ Enable Multi-Factor Authentication (MFA) for RDP (if using Azure AD).
