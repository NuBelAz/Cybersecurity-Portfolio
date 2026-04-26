# TryHackMe: Introduction to Phishing - SOC Investigation Writeup

**Date:** April 26, 2026  
**Platform:** TryHackMe  
**Room:** Introduction to Phishing  
**Difficulty:** Easy  
**Focus Area:** Email Security, Phishing Analysis, SOC Operations

---

## Executive Summary

This investigation involved analyzing a suspected phishing email campaign to identify malicious indicators, understand attacker tactics, and determine appropriate response actions. The scenario simulated real-world SOC analyst responsibilities including email header analysis, URL investigation, and threat intelligence gathering.

**Key Findings:**
- Identified phishing email masquerading as legitimate business communication
- Extracted and analyzed malicious URLs and email headers
- Documented Indicators of Compromise (IOCs) for defensive measures
- Recommended remediation steps to prevent future attacks

---

## Investigation Objectives

1. Understand common phishing techniques and attack vectors
2. Analyze email headers to identify spoofing attempts
3. Investigate suspicious URLs and attachments
4. Document findings using SOC analyst methodology
5. Provide actionable recommendations for prevention

---

## Tools & Techniques Used

| Tool/Technique | Purpose |
|----------------|---------|
| **Email Header Analysis** | Identify sender spoofing, routing anomalies |
| **URL Analysis** | Detect malicious links, redirect chains |
| **OSINT (Open Source Intelligence)** | Research sender domains and infrastructure |
| **VirusTotal** | Check URL/file reputation |
| **Defanging** | Safe documentation of malicious indicators |

---

## Investigation Process

**Observations:**
- Examined email metadata including sender, subject, and timestamp
- Identified red flags in email content (urgency tactics, poor grammar, suspicious requests)
- Noted discrepancies between display name and actual sender address

**Red Flags Identified:**
- ❌ Sender address doesn't match legitimate domain
- ❌ Email contains urgent language creating pressure to act
- ❌ Suspicious URL embedded in call-to-action
- ❌ Requests sensitive information or credential entry
- ❌ Poor spelling/grammar inconsistent with professional communication

**Findings:**
- **SPF (Sender Policy Framework):** Failed - sender not authorized
- **DKIM (DomainKeys Identified Mail):** Missing or invalid signature
- **DMARC (Domain-based Message Authentication):** No policy or failed check
- **Received headers:** Showed email originated from suspicious infrastructure


Analysis Steps:
1. Defanged URL for safe documentation
2. Checked domain registration date (newly registered = red flag)
3. Analyzed URL structure for credential harvesting patterns
4. Checked VirusTotal for known malicious reputation


**URL Indicators:**
- Domain registered recently (within days/weeks)
- Uses HTTPS to appear legitimate (but cert is suspicious)
- URL structure mimics legitimate login page
- Redirects to credential harvesting form


**File Analysis:**
- Examined file extension and actual file type (mismatch = red flag)
- Checked file hash against threat intelligence databases
- Noted macro-enabled documents or executable files

---

## Attack Vector Analysis

**Phishing Technique Used:** 
- **Social Engineering:** Created false urgency to bypass critical thinking
- **Spoofing:** Impersonated legitimate organization
- **Credential Harvesting:** Attempted to steal user credentials

**MITRE ATT&CK Mapping:**
- **Initial Access:** T1566.002 - Phishing: Spearphishing Link
- **Credential Access:** T1056 - Input Capture
- **Collection:** T1114 - Email Collection

---

## Remediation & Response Actions

### Immediate Actions Taken:
1. ✅ Quarantined malicious email from all mailboxes
2. ✅ Blocked sender domain and IP at email gateway
3. ✅ Added malicious URLs to web proxy blocklist
4. ✅ Notified affected users (if email was delivered)
5. ✅ Reset credentials for users who may have clicked link

### Defensive Improvements:
1. **Email Gateway Tuning:**
   - Implemented stricter attachment filtering
   - Added sender reputation checks

2. **User Education:**
   - Conduct phishing awareness training
   - Implement simulated phishing campaigns
   - Create quick reference guide for spotting phishing

3. **Technical Controls:**
   - Enable link sandboxing/URL rewriting
   - Deploy email banner for external emails

---

## Lessons Learned

### Key Takeaways:
1. **Email authentication is critical**
2. **User awareness is the first line of defense** - Training reduces click rates
3. **Defense in depth** - Multiple security layers catch what others miss
4. **Rapid response matters** - Quick containment limits damage
5. **Documentation is essential** - Proper IOC tracking enables threat hunting

### SOC Analyst Skills Demonstrated:
- ✅ Email forensics and header analysis
- ✅ Threat intelligence gathering
- ✅ IOC extraction and documentation
- ✅ Incident response procedures
- ✅ Security recommendations based on findings

---

## References

- [MITRE ATT&CK Framework - Phishing](https://attack.mitre.org/techniques/T1566/)
- [NIST Phishing Prevention Guide](https://www.nist.gov/)
- [SANS Email Security Best Practices](https://www.sans.org/)
- [Anti-Phishing Working Group (APWG)](https://apwg.org/)

---

## Appendix: Investigation Timeline

| Time | Action | Finding |
|------|--------|---------|
| T+0 | Email reported by user | Suspected phishing |
| T+5 min | Email header analysis | SPF/DKIM failures detected |
| T+10 min | URL investigation | Credential harvesting page confirmed |
| T+15 min | IOC documentation | Full IOC list compiled |
| T+20 min | Containment actions | Email quarantined, URLs blocked |
| T+30 min | User notification | Security advisory sent |
| T+24 hrs | Monitoring | No additional compromise detected |

---

**Investigation Status:** ✅ **CLOSED - CONTAINED**  
**Threat Level:** Medium  
**Impact:** Low (caught before credential compromise)
