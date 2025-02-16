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
- VirtualBox
- Kali Linux

### Step 1: Create a Kali Linux on Virtual Box


### Step 2: Set up RDP on Kali Linux

*Ref 1: Install xrdp and xfce4 (if not installed)*

Use statement:

sudo apt update && sudo apt upgrade -y

sudo apt install -y xrdp xfce4 xfce4-goodies

(xrdp: The RDP server for Linux, xfce4: A lightweight desktop environment for smooth remote sessions)

![image](https://github.com/user-attachments/assets/0701b5d2-10fd-4345-a9c6-04129af11143)

*Ref 2: Enable and Start the xrdp Service*

Use statement:

sudo systemctl enable xrdp

sudo systemctl start xrdp

sudo systemctl status xrdp

Ensure it's running without errors. If you see active (running), it's good to go.

![image](https://github.com/user-attachments/assets/97317892-702b-4d0c-b27f-d736f1cf537a)

*Ref 3: Add xrdp User to the ssl-cert Group*

Use statement:

sudo adduser xrdp ssl-cert

sudo systemctl restart xrdp

This ensures xrdp has the correct permissions.

![image](https://github.com/user-attachments/assets/48947049-a0fa-493e-866f-55c11f5a7bf9)

*Ref 4: Set XFCE as the Default Desktop for RDP Sessions*

Use statement:

echo "xfce4-session" > ~/.xsession

Then reset the xrdp service

sudo systemctl restart xrdp

![image](https://github.com/user-attachments/assets/cb9b30a9-287d-4b51-9778-4cf0651da2a0)

*Ref 5: Find Your Kali Linux IP Address*

Use statement: ip a

You'll want to look for the IP under eth0 or wlan0 (e.g., 192.168.1.100). 

![image](https://github.com/user-attachments/assets/d0c8dd58-219f-4e28-97de-b7d92c4ce71a)

