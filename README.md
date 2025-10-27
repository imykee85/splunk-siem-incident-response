# Splunk SIEM Incident Response Project

**Security Operations Center (SOC) Analysis | Threat Detection & Investigation**

## Project Overview

Conducted comprehensive security incident analysis using Splunk Enterprise SIEM platform to detect, investigate, and respond to a critical brute force attack that resulted in system compromise and privilege escalation. This project demonstrates hands-on experience with enterprise security monitoring tools, log analysis, threat hunting, and incident response procedures.

## Key Findings

- **Detected:** 15 failed authentication attempts from 3 distinct source IP addresses
- **Identified:** Successful breach after brute force attack (IP: 192.168.1.100)
- **Discovered:** Post-breach privilege escalation (Windows EventID 4672)
- **Blocked:** Secondary external attack from IP 203.0.113.45 (7 failed attempts)
- **Created:** Real-time SOC monitoring dashboard for ongoing threat detection

**Overall Risk Rating:** CRITICAL  
**Attack Vector:** Brute Force Password Guessing (MITRE ATT&CK T1110.001)


## Technologies & Tools

- **SIEM Platform:** Splunk Enterprise 9.1.0.2
- **Query Language:** SPL (Splunk Processing Language)
- **Data Source:** Windows Security Event Logs
- **Visualization:** Splunk Dashboard Studio
- **Operating System:** macOS Catalina 10.15.7
- **Frameworks:** MITRE ATT&CK, NIST SP 800-61r2, Security+ Domains


## Investigations Performed

### Investigation #1: Brute Force Attack Detection
**SPL Query:**

source="security_log.log" EventID=4625 | stats count by Source, User

**Results:**
- 15 failed login attempts (EventID 4625)
- Primary attacker: 192.168.1.100 (5 attempts on "admin" account)
- Secondary attacker: 203.0.113.45 (7 attempts on "administrator" account)
- Attack duration: 3 minutes 22 seconds



### Investigation #2: Successful Breach Confirmation
**SPL Query:**

source=“security_log.log” Source=192.168.1.100 | table _time, EventID, User, Status

**Critical Finding:**
- Attacker successfully authenticated as "admin" after 5 failed attempts
- Breach occurred at 08:18:45 (EventID 4624)
- Time to compromise: 3 minutes 22 seconds



### Investigation #3: Post-Breach Privilege Escalation
**SPL Query:**

source=“security_log.log” User=admin | table _time, EventID, Status, Reason

**Critical Discovery:**
- Privilege escalation detected at 09:45:33 (EventID 4672)
- Attacker gained special administrative privileges
- Time between breach and escalation: 1 hour 26 minutes
- Full system compromise confirmed

**MITRE ATT&CK:** T1068 (Exploitation for Privilege Escalation)



### Investigation #4: Secondary Attack Analysis
**SPL Query:**

source=“security_log.log” Source=203.0.113.45 | stats count by EventID, Status

**Results:**
- External attacker from IP 203.0.113.45
- 7 failed attempts targeting "administrator" account
- All attempts blocked (strong password/account lockout)
- Attack successfully contained



## Dashboard Created

**Security Incident Response Dashboard**
- Real-time monitoring of failed login attempts
- Time-series visualization of authentication events
- Interactive drill-down capabilities
- Exported to PDF for reporting



## Indicators of Compromise (IOCs)

**Malicious IP Addresses:**
- 192.168.1.100 (Internal - PRIMARY THREAT - successful breach)
- 203.0.113.45 (External - blocked attack)
- 10.0.0.55 (reconnaissance activity)

**Compromised Accounts:**
- admin (successful compromise, privilege escalation)

**Attack Signatures:**
- Multiple rapid failed authentication attempts
- Successful login following failed attempts
- Privilege escalation shortly after compromise

**MITRE ATT&CK Techniques:**
- T1110.001: Brute Force (Password Guessing)
- T1078: Valid Accounts
- T1068: Exploitation for Privilege Escalation



## Recommendations

**Immediate Actions:**
1. Block malicious IPs at firewall (192.168.1.100, 203.0.113.45)
2. Force password reset for compromised admin account
3. Implement account lockout policy (5 failed attempts)
4. Enable multi-factor authentication (MFA) on all admin accounts
5. Isolate compromised system from network

**Short-term Improvements:**
1. Deploy endpoint detection and response (EDR)
2. Implement privileged access management (PAM)
3. Create automated Splunk alerts
4. Enable enhanced audit logging

**Long-term Strategy:**
1. Implement Zero Trust Architecture
2. Regular penetration testing program
3. Security awareness training
4. User and Entity Behavior Analytics (UEBA)



## Compliance Impact

**Frameworks Affected:**
- **PCI DSS:** Failed requirements 8.1.6 (account lockout), 8.3 (MFA for admin)
- **HIPAA:** Missing MFA implementation
- **GDPR:** Breach notification required within 72 hours
- **SOX:** IT control failures over privileged access



## Project Files

- Full_Report.pdf - Comprehensive incident analysis report
- Dashboard.pdf - Security Operations Center monitoring dashboard
- screenshots/ - Evidence and investigation screenshots



## Contact

Micahel Ampo
Security Analyst | Cybersecurity Enthusiast
imykee85@gmail.com
[LinkedIn Profile]



Last Updated: October 2024
Status: Complete

































