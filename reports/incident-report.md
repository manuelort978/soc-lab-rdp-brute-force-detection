**Incident Report: RDP Brute Force Attack**

*Summary*
A brute-force attack was detected targeting a Windows 10 host via RDP.

*Timeline*
- Attack started: 11:08:39 AM
- Multiple failed logins detected
- Successful login

*Indicators of Compromise (IoCs)*
- Source IP: 192.168.56.103
- Target user: testuser

*Analysis*
- Event ID 4625 observed repeatedly
- Event ID 4624 confirms successful compromise

*Impact*
- Unauthorized access to system

*Recommendations*
- Enable account lockout policies
- Restrict RDP access
- Monitor failed login attempts
