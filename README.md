# Security Assessment Reports

This repository contains sample penetration test and vulnerability assessment reports from my home lab. All testing was performed in isolated environments I own, with no impact to production systems. The goal: demonstrate end-to-end VAPT methodology, technical depth, and executive-level reporting.

## **Reports**

### **1. Legacy Corp – Network MITM via ARP Spoofing** 
`[LegacyCorp_MITM_Report.pdf](./LegacyCorp_MITM_Report.pdf)`

**Scope**: Layer 2 security of simulated enterprise network `10.0.1.0/24` 
**Key Findings**: 
- CVSS 8.8 – ARP Spoofing due to lack of Dynamic ARP Inspection
- Flat network allows Guest WiFi to reach Domain Controller
- Plaintext HTTP/SMB/LDAP traffic captured

**Impact**: Full domain compromise in <60 seconds with $0 tools. Fails NDPA 2023 + PCI-DSS 11.4.

**Remediation Highlights**: 
1. Enable DAI on access switches – 7 day fix
2. VLAN segmentation: Guest/Corp/Server – 30 days 
3. Force SMB signing + disable SMBv1 – 30 days

**Standards Used**: PTES, OWASP WSTG, NIST 800-53, CIS Controls

---

### **2. Legacy Corp – Web Application RCE via Apache Struts2** 
`[LegacyCorp_Struts_RCE_Report.pdf](./LegacyCorp_Struts_RCE_Report.pdf)` *[Upload when ready]*

**Scope**: External web app assessment of legacy customer portal 
**Key Findings**:
- CVSS 9.8 Critical – CVE-2017-5638 Apache Struts2 RCE
- Achieved remote code execution as `www-data`
- Post-exploit: Found `NOPASSWD: ALL` sudo misconfig → root escalation

**Impact**: Unauthenticated attacker gains full server control. Customer PII + payment data exposed.

**Remediation Highlights**:
1. Emergency patch to Struts 2.5.10.1+
2. WAF rule to block `Content-Type` OGNL payloads
3. CIS Ubuntu Hardening: remove NOPASSWD, enforce key-based SSH

**Standards Used**: PTES, OWASP Top 10 2017, NIST CSF

---

## **Methodology**
All engagements follow the **Penetration Testing Execution Standard PTES**:
1. **Pre-engagement**: Scope defined, rules of engagement documented
2. **Intelligence Gathering**: Network mapping, service enumeration
3. **Threat Modeling**: Attack paths prioritized by business impact
4. **Exploitation**: Controlled, reversible attacks with evidence capture
5. **Post-Exploitation**: Risk demonstration without data destruction
6. **Reporting**: Executive summary + technical findings + CVSS scoring + remediation roadmap

## **Tools Used**
`Nmap` `Burp Suite` `Metasploit` `Wireshark` `Arpspoof` `LinPEAS` `Autopsy` `Semgrep` `Python` `Bash`

## Contact
chijioke chukwuemeka lewis 
VAPT | Network Security | Forensics 
lewis4chi@yahoo.com| | | GitHub: [lewisdebug1024][LinkedIn][Nigeria]

*Open to VAPT, Red Team, and Security Analyst roles in Nigeria. Hybrid/Onsite.*

---
**Disclaimer**: These reports are from isolated lab environments built for educational purposes. No real client data was accessed. Names like "Legacy Corp" are fictional.