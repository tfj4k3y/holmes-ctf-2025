# Challenge - The Card

## 📌 Introduction

- **Category:** log analysis, using provided platforms like CTI.
- **Difficulty:** Easy.
- **Points:** 1500.
- **Files and platforms provided:** access.log, application.log, waf.log, platforms such as Cyber Threat Intelligence platform.<br><br>

## 📝 Description

This challenge simulates a cyber incident at Cogwork-1. The attacker leaves digital traces across different log files, and the player needs to extract 12 flags related to the intrusion.<br><br>

## 🎯 Objective

Analyze logs to identify the attacker’s activities and retrieve 12 flags.<br><br>

## 🚩 Flags

### Flag #1 – First User-Agent

- **Objective:** Identify the first User-Agent used by the attacker against Nicole Vale’s honeypot by analyzing the provided logs.
- **Approach:** Review the `access.log` file and look at the last column, which contains User-Agent strings. Extract the earliest one associated with attacker activity.
- **Result:** [REDACTED]
- **Notes:** Learned to quickly locate User-Agent headers within web server logs and distinguish them as potential indicators of attacker tools or browsers.

---

### Flag #2 – Web shell filename

- **Objective:** Identify the filename of the web shell deployed after the WAF was bypassed.
- **Approach:** Examined `application.log` for suspicious entries. Found a line containing the phrase “Web shell created”, followed by the path to a file. That filename corresponded to the flag.
- **Result:** [REDACTED]
- **Notes:** Learned to leverage keyword searches in logs (e.g., “web shell”) to quickly pinpoint attacker actions and extract filenames.

---

### Flag #3 – Exfiltrated database

- **Objective:** Determine the name of the database exfiltrated by the attacker.
- **Approach:** Inspected `waf.log` for evidence of data exfiltration. Focused on .sql files and keywords such as “DATABASE_DOWNLOAD”, which led to the correct database file.
- **Result:** [REDACTED]
- **Notes:** Reinforced the importance of searching for file extensions and relevant keywords in log files when investigating data theft.

---

### Flag #4 – Recurring meaningless string

- **Objective:** Identify the recurring meaningless string that appears in the logs.
- **Approach:** Reviewed all provided logs and noticed a non-standard string repeatedly attached to filenames and entries, as shown in the screenshots.
- **Result:** [REDACTED]
- **Notes:** Recognized that attackers may leave consistent markers or signatures across multiple artifacts, which can serve as useful indicators.

---

### Flag #5 – Number of linked campaigns

- **Objective:** Count the number of campaigns linked to the honeypot attack on the CTI platform.
- **Approach:** Logged into the CTI platform and searched using the suspicious string discovered in the previous flag. The results displayed the total number of related campaigns.
- **Result:** [REDACTED]
- **Notes:** Practiced correlating observed indicators with threat intelligence platforms to pivot from raw data to campaign-level insights.

---

### Flag #6 – Tools and malware linked to campaigns

- **Objective:** Find the total number of tools and malware linked to the identified campaigns.
- **Approach:** Accessed each campaign individually on the CTI platform. Navigated to the Links section and counted all entries for tools and malware.
- **Result:** [REDACTED]
- **Notes:** Gained experience in manually correlating campaign data with linked tools and malware in CTI systems.

---

### Flag #7 – Malware SHA-256 hash

- **Objective:** Identify the SHA-256 hash of the malware consistently used in the campaigns.
- **Approach:** Exported campaign data to JSON and analyzed all listed indicators. Found multiple hashes, but only one SHA-256 value was repeated across campaigns.
- **Result:** [REDACTED]
- **Notes:** Learned to validate recurring IOCs across multiple sources and highlight those as high-confidence indicators.

---

### Flag #8 – Malware C2 IP address

- **Objective:** Use the CogWork Security Platform to find the IP address that the malware connects to.
- **Approach:** Logged into the platform using provided credentials (nvale/CogworkBurning!). Queried the previously identified SHA-256 hash in the search bar, which revealed the C2 IP address.
- **Result:** [REDACTED]
- **Notes:** Practiced pivoting from malware hashes to infrastructure details using a security platform.

---

### Flag #9 – Persistence file path

- **Objective:** Identify the full file path created by the malware to maintain persistence.
- **Approach:** Opened the Details section for the malware on the platform. Scrolled through the information until finding the persistence mechanism, which included the file path.
- **Result:** [REDACTED]
- **Notes:** Understood how malware often creates or modifies files for persistence and how to retrieve this data from platform reports.

---

### Flag #10 – Number of open ports

- **Objective:** Find the number of open ports on the attacker’s server using the CogNet Scanner Platform.
- **Approach:** Logged into the CogNet Scanner Platform and ran the provided scan against the identified server. The platform displayed the number of open ports directly in the results.
- **Result:** [REDACTED]
- **Notes:** Reinforced knowledge of network scanning basics and how CTI platforms summarize infrastructure exposure.

---

### Flag #11 – Organization linked to the IP

- **Objective:** Identify the organization associated with the attacker’s IP address.
- **Approach:** Accessed the details section for the IP on the CogNet Scanner Platform. Found the organization name listed in the report.
- **Result:** [REDACTED]
- **Notes:** Learned to attribute infrastructure to organizations using enrichment data in CTI tools.

---

### Flag #12 – Cryptic banner message

- **Objective:** Discover the cryptic message displayed in the banner of an exposed service.
- **Approach:** On the CogNet Scanner Platform, navigated to the Services tab and inspected the details of each exposed service. Found a unique banner string under TCP port 7477.
- **Result:** [REDACTED]
- **Notes:** Recognized how unusual service banners can provide additional intelligence about attacker infrastructure.<br><br>

---

## 📶 Summary

- **What I learned:** Improved my ability to correlate artifacts across different log sources, pivot IOCs into CTI platforms, and validate findings with supporting evidence. Also practiced structured documentation of investigation steps.  
- **Most useful tools/techniques:** Wireshark, grep, jq, CyberChef, and CTI platforms (for enrichment and campaign linkage).  
- **Biggest difficulty:** Correlating recurring meaningless strings across multiple logs and ensuring that each IOC was properly mapped to the right campaign or malware entry.  
- **Key takeaway:** Effective log analysis is not only about finding single indicators but about connecting them across systems and platforms to build a bigger picture of the attacker’s activity. Clear documentation of each step makes results easier to verify and share.  
