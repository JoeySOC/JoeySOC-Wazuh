🛡️ Wazuh - Security Detection Lab

This project documents my hands-on experience using Wazuh to detect and respond to simulated security events in a virtualized SOC Lab environment. The objective is to continue enhancing and improving my skills as a SOC Analyst (blue team) by configuring and analyzing alerts generated from common cyber attacks.

---

**Skills Practiced**

* Blue team threat detection and analysis
* Rule correlation and alert validation in Wazuh
* Hands-on detection of malicious web traffic and system events
* Familiarization with MITRE ATT\&CK techniques, rule metadata, and compliance standards

---

##   Attacks Detected & Alerts Generated

### 1. **Cross-Site Scripting (XSS) Attempt**

* **Alert Message**: `XSS (Cross Site Scripting) attempt`
* **Rule ID**: 31105
* **Detection Source**: DVWA (Damn Vulnerable Web App)
* **Technique**: A malicious script was injected via a vulnerable web form input.
* **Triggered Rule Metadata**:

  * **Groups**: attack, web, accesslog
  * **Compliance**: PCI\_DSS, GDPR, NIST\_800\_53, TSC, MITRE
  * **Relevant URL Pattern**: `%3Cscript%3E...%3C/script%3E`

---

### 2. **Multiple Web Server 400 Error Codes from Same IP**

* **Alert Message**: `Multiple web server 400 error codes from same source IP`
* **Rule ID**: 31151
* **Rule Level**: 10
* **Source IP**: 192.168.56.102 (Kali Linux attacker)
* **Tool Used**: Nmap Scripting Engine (NSE)
* **MITRE**:

  * **ID**: T1595.002
  * **Tactic**: Reconnaissance
  * **Technique**: Vulnerability Scanning

---

### 3. **URL Too Long – Possible Web Attack**

* **Alert Message**: `URL too long. Higher than allowed on most browsers. Possible attack.`
* **Rule ID**: 31115
* **Level**: 13 (Critical)
* **Explanation**: Detected an abnormally long URL, a known method to trigger buffer overflow or web application parsing issues.
* **Compliance**: PCI\_DSS, HIPAA, GDPR, NIST\_800\_53, TSC, MITRE

---

### 4. **Windows User Account Created or Enabled**

* **Alert Message**: `User account enabled or created.`
* **Rule ID**: 60103
* **OS**: Windows 11 VM
* **Event Source**: Win.System.EventID (e.g., 4720)
* **Compliance**: GDPR, HIPAA, PCI\_DSS, GPG13
* **Use Case**: Tracks user provisioning activities — relevant in insider threat and persistence analysis.

---

### 5. **Web Server 400 Error Code**

* **Alert Message**: `Web server 400 error code.`
* **Rule ID**: 31101
* **Level**: 5
* **Trigger**: HTTP 400 Bad Request from the attacker machine due to malformed payloads or scan attempts
* **Tool Used**: Nmap

---

## 🛡️ Security Recommendations

1. **Input Validation**
   Apply strict input sanitization on all user-facing forms to prevent XSS, SQLi, and command injection attacks.

2. **Web Application Firewall (WAF)**
   Use a WAF to block malicious traffic and patterns before they hit the application layer.

3. **Rate Limiting and IP Blocking**
   Block or throttle IPs generating high volumes of 400/500 errors. Deploy fail2ban or similar tools to automate this.

4. **Proper Logging and Monitoring**
   Ensure real-time logging of authentication and system events. Monitor for Event IDs like 4720 (user creation).

5. **Rule Tuning in Wazuh**
   Fine-tune Wazuh rules and add custom alerts based on your environment's specific attack patterns.

6. **Security Patch Management**
   Regularly update your OS, web applications, and SIEM agents to close known vulnerabilities.

7. **Access Control**
   Limit privileged account creation to a handful of administrators. Use Role-Based Access Control (RBAC) where possible.

---

## Screenshots

All screenshots of detected alerts have been uploaded to this GitHub repo for visual reference and verification.

---

##  Notes

* Alerts were generated using real-time attack simulations from a Kali Linux attacker VM.
* Monitored systems: DVWA (Ubuntu), Windows 11 VM
* Detection and correlation were performed entirely using **Wazuh Dashboard** running on Ubuntu Server.

---

##  Status

 **Training Environment Active** | 🔧 Continuously Updating Rules & Scenarios
