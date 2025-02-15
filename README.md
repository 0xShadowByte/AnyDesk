# Setting up a Windows VM in VMware and enable RDP

## Objective


## Skills Learned


## Tools
- VMware Workstation Pro 17

## Steps

Step 1: Create a Windows Virtual Machine in VMware
Open VMware Workstation Pro (or VMware Player).
Click "Create a New Virtual Machine".
Select "Typical (Recommended)" and click Next.
Choose "Install from ISO" and select your Windows ISO file (Windows 10/11 or Windows Server).
Click Next and select Windows version (e.g., Windows 10 Pro).
Set VM Name & Location (e.g., Windows-RDP-VM).
Allocate CPU & RAM (recommend 2 vCPUs, 4GB+ RAM).
Set Disk Size (recommend 50GB+, choose "Store as a single file").
Click Finish, then Power On the VM to install Windows.

Step 2: Enable Remote Desktop (RDP) in Windows
Log into the Windows VM.
Open Run (Win + R), type sysdm.cpl, and press Enter.
Go to "Remote" tab and select "Allow remote connections to this computer".
Check "Allow connections only from computers running Remote Desktop with Network Level Authentication" (for security).
Click "Select Users" → Add your Windows user account.
Click Apply > OK.

Step 3: Configure Firewall to Allow RDP
Open Windows Defender Firewall (Win + R, type firewall.cpl, press Enter).
Click "Allow an app or feature through Windows Defender Firewall".
Scroll down, find "Remote Desktop", and check both Private & Public boxes.
Click OK.
OR, enable RDP via PowerShell:
powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

Step 4: Find Your VM's IP Address
Open Command Prompt (Win + R, type cmd, press Enter).
Type:
ipconfig
Look for IPv4 Address (e.g., 192.168.1.100).

Step 5: Connect to the Windows VM via RDP
On your host machine, open Remote Desktop Connection (Win + R, type mstsc, press Enter).
Enter the VM’s IP address (192.168.1.100).
Click Connect and enter your Windows VM username & password.
Click OK, and you should be connected! 🎉

🔐 Bonus: Secure Your RDP Setup
✅ Change RDP Port (Default 3389 → Custom Port):

powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -Name PortNumber -Value 3390
✅ Disable RDP for non-admin users using Group Policy (gpedit.msc).
✅ Enable Multi-Factor Authentication (MFA) for RDP (if using Azure AD).
