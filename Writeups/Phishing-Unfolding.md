# TryHackMe: Phishing Unfolding - Advanced SOC Investigation Writeup

**Date:** April 26, 2026  
**Platform:** TryHackMe  
**Room:** Phishing Unfolding  
**Difficulty:** Medium  
**Focus Area:** Advanced Email Analysis, Artifact Extraction, Malware Investigation

---

## Summary

This investigation involved a multi-stage phishing campaign analysis that required deep-dive email forensics, malicious artifact extraction, and advanced threat hunting techniques. The scenario simulated a real-world SOC Level 2 investigation where initial phishing detection led to uncovering a larger attack infrastructure.

**Critical Findings:**
- Multi-stage phishing attack with malicious payload delivery
- Credential harvesting combined with malware distribution
- Command and Control (C2) infrastructure identified
- Multiple IOCs extracted for threat intelligence sharing
- Attack chain fully mapped from initial access to post-exploitation

**Risk Rating:** 🔴 **HIGH** - Active threat requiring immediate containment

---

## Investigation Scope

### Scenario Context:
A user reported receiving a suspicious email that appeared to be from a trusted vendor. Initial triage revealed this was part of a sophisticated phishing campaign with multiple attack vectors.

### Investigation Goals:
1. Perform comprehensive email forensics
2. Extract and analyze malicious attachments/URLs
4. Map complete attack chain
5. Provide comprehensive threat intelligence report
   
---

#### Email Header Analysis

**Red Flags Identified:**
- ❌ **Reply-To != From:** Email replies go to attacker-controlled address
- ❌ **Return-Path mismatch:** Bounce emails reveal true sender infrastructure
- ❌ **Received headers:** Email did not originate from claimed domain

**Analysis:** Email bypassed gateway due to misconfigured filtering rules. Immediate action required to close security gap.

---

**Redirect Chain Analysis:**
1. **URL Shortener (bit.ly):** Obscures final destination, evades URL reputation checks
2. **Compromised Legitimate Site:** Abused WordPress plugin vulnerability
3. **Credential Harvesting Page:** Mimics Microsoft 365 login
4. **Data Collection Endpoint:** Sends stolen credentials to attacker C2

**Technical Findings:**
- Credential form captures username, password, MFA code
- JavaScript keylogger embedded on page
- Session cookies exfiltrated to attacker server
- Page uses legitimate Microsoft CSS/logos (downloaded from cdn.microsoft.com)

---

**Static Analysis:**
- ❌ **Double extension attack:** `.pdf.exe` to trick users
- ❌ **Icon spoofed:** Uses PDF icon to appear legitimate
- ❌ **Unsigned executable:** No valid digital signature
- ❌ **High entropy sections:** Likely packed/obfuscated malware

**VirusTotal Results:**
- Detection Rate: 45/72 (62% detection)
- Classification: Trojan.Downloader / InfoStealer
- First Submission: 3 days ago (very recent - active campaign)
- 
--- 

### Immediate Containment (T+0 to T+1 Hour)

**Email Security:**
1. ✅ Quarantined all emails matching IOC patterns
2. ✅ Blocked sender domains/IPs at email gateway
3. ✅ Enabled aggressive filtering for similar campaigns
4. ✅ Searched all mailboxes for campaign indicators (found 47 delivered emails)

### Recovery (T+24 to T+48 Hours)

**System Restoration:**
1. ✅ Restored systems from clean backups
2. ✅ Re-enabled network access after security validation
3. ✅ Verified all security controls functioning properly
4. ✅ Resumed normal business operations with enhanced monitoring

**Enhanced Monitoring:**
1. ✅ 30-day heightened alert monitoring
2. ✅ Daily IOC sweeps across environment
3. ✅ Threat hunting for similar TTPs
4. ✅ Weekly executive briefings on incident status

---

## Root Cause Analysis

### How Did This Happen?

**Security Control Failures:**
1. **Email Gateway Misconfiguration:** DMARC policy not enforced (reject → quarantine)
2. **Insufficient User Training:** Users unable to identify sophisticated phishing
3. **Delayed EDR Deployment:** Some endpoints lacked EDR protection
4. **No Email Link Sandboxing:** Malicious URLs not detonated before delivery
5. **MFA Not Enforced:** Stolen credentials still valid without second factor

---

## Lessons Learned

### What Went Well:
✅ Rapid detection after user reported suspicious email  
✅ Comprehensive IOC extraction for threat intelligence  
✅ Effective cross-team collaboration (IT, Security, Management)  
✅ No data breach or ransom demand occurred  
✅ Strong documentation enabled knowledge sharing  

---

## SOC Analyst Skills

### Technical Skills:
- ✅ Advanced email forensics and header analysis
- ✅ Malware analysis (static and dynamic)
- ✅ Network traffic analysis and C2 identification
- ✅ IOC extraction and threat intelligence correlation
- ✅ Incident response lifecycle execution
- ✅ Root cause analysis
- ✅ Tool proficiency (CyberChef, VirusTotal, sandboxes)

### Analytical Skills:
- ✅ Attack chain reconstruction
- ✅ Threat actor TTP identification
- ✅ Risk assessment and prioritization
- ✅ Evidence correlation across multiple sources
- ✅ Pattern recognition in attacker behavior

### Communication Skills:
- ✅ Technical writeup for SOC documentation
- ✅ IOC reporting for threat intelligence sharing
- ✅ Executive summary for management

---

## References & Resources

**Tools Used:**
- [PhishTool](https://www.phishtool.com/) - Email analysis platform
- [URLScan.io](https://urlscan.io/) - URL investigation
- [ANY.RUN](https://any.run/) - Interactive malware sandbox
- [CyberChef](https://gchq.github.io/CyberChef/) - Data manipulation
- [VirusTotal](https://www.virustotal.com/) - File/URL scanning

---

**Investigation Status:** ✅ **CLOSED - FULLY REMEDIATED**  
**Threat Level:** 🔴 **HIGH** (active campaign, ongoing monitoring required)  
**Final Assessment:** Successful containment with no major business impact. Controls improved to prevent recurrence.

---
