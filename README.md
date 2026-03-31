**SOC SIMULATION: RDP BRUTE FORCE DETECTION LAB**\
\
\
*OVERVIEW*\
This project simulates a brute-force attack against a Windows 10 machine via RDP using Hydra from an Ubuntu attacker machine.\
The objective is detect, analyze, and document the attack as a SOC analyst would.\
\
\
*OBJECTIVES*\
-Simulate a real-world brute-force attack\
-Analyze Windows Security Event Logs\
-Identify indicators of compromise (IoCs)\
-Document the incident lifecycle\
\
\
*ARCHITECTURE*\
-Attacker: Ubuntu (Hydra)\
-Victim: Windows 10 (RDP enabled)\
-Monitoring: Windows Event Logs & Wazuh SIEM\
\
\
*TOOLS USED TO ATTACK SIMULATION*\
Hydra (Comand executed):\
hydra -l testuser -P passwords.txt rdp://192.168.1.20\
\
\
*LOGS ANALYSIS*\
Events ID:\
-4625: Failed login attempts\
-4624: Successful login\
\
Findings:\
-Multiple failed login attempts from the same IP\
-Logon Type 10 confirms RDP attack\
-Source IP identified as attacker machine\
\
\
*DETECTION LOGIC*\
Use Case: Detect RDP brute-force attack\
\
Rule: If more than 5 failed login attempts (Event ID: 4625) occur whitin 1 minute from the same IP --> Trigger Alert\
\
\
*RESULTS*\
-Successfully simulated brute-force attack\
-Detected attack via log analysis\
-Identified attacker IP and compromised account\
\
\
*INCIDENT RESPONSE*\
-Detection: Multiple failed login attempts detected\
-Analysis: Correlated events (Event ID 4625 & 4624)\
-Containment: Recommendation to block attacker IP\
-Lessons Learned: Importance of account lockout policies\
\
\
*EVIDENCE*\
-Screenshots of logs and attack\
-Sample logs included\
-Incident report available in **/reports**\
\
\
*SKILLS DEMOSTRATED*\
-Security Monitoring\
-Log Analysis (Windows Event Logs)\
-Threat Detection\
-Incident Investigation\
\
\
*FUTURE IMPROVEMENTS*\
-Automate detection rules\
-Add threat intelligence enrichment
