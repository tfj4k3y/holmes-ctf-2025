# Challenge – The Watchman's Residue

## Introduction

- **Category:** packet capture and disk image analysis.  
- **Difficulty:** Medium.  
- **Points:** 1900.  
- **Files provided:** PCAPNG capture and disk image inside the provided ZIP.  

## Description

This challenge simulates the compromise of a Managed Service Provider (MSP) connected to the city’s financial core. According to the storyline, the attacker manipulated the MSP’s AI servicedesk bot into leaking remote access credentials, a known technique of Moriarty’s.

## Objective

Analyze the packet capture and disk image to reconstruct the attacker’s actions and retrieve 8 flags.

## Flags

### Flag #1 – Attacker’s IP address

- **Objective:** Identify the IPv4 address of the decommissioned machine used to start a chat session with `MSP-HELPDESK-AI`.  
- **Approach:** Used Wireshark’s *Statistics → Conversations* and *Endpoints* to find IPs exchanging large amounts of data. Verified by filtering HTTP traffic and following the session where the attacker’s conversation dominated the exchange.  
- **Result:** [REDACTED]  
- **Notes:** Learned to combine “top talker” analysis with protocol-level filtering to isolate suspicious connections.

---

### Flag #2 – Hostname of the decommissioned machine

- **Objective:** Determine the hostname of the attacker’s decommissioned machine.  
- **Approach:** Filtered packets by the attacker’s IP. Observed NBNS traffic clearly revealing the machine’s hostname.  
- **Result:** [REDACTED]  
- **Notes:** Reinforced how legacy protocols (e.g., NetBIOS) often leak hostnames and can provide quick attribution.

---

### Flag #3 – First message to the chatbot

- **Objective:** Identify the first message sent by the attacker to the AI chatbot.  
- **Approach:** Traced the HTTP stream of the attacker’s conversation with the chatbot. Located the initial JSON payload containing the attacker’s first message.  
- **Result:** [REDACTED]  
- **Notes:** Practiced extracting and interpreting application-layer payloads from captured network traffic.

---

### Flag #4 – Prompt injection timestamp

- **Objective:** Determine when the attacker’s prompt injection caused the chatbot to leak remote management tool information.  
- **Approach:** Reviewed the HTTP conversation to find the attacker’s crafted prompt disguised as an IT technician request. Noted the timestamp when the chatbot responded with sensitive data.  
- **Result:** [REDACTED]  
- **Notes:** Understood how social engineering tactics can be embedded in prompt injections, leading to sensitive disclosures.

---

### Flag #5 – Remote management tool credentials

- **Objective:** Extract the Device ID and password obtained from the chatbot.  
- **Approach:** Observed the chatbot’s response to the attacker’s injection. The reply included both the Device ID and password.  
- **Result:** [REDACTED]  
- **Notes:** Learned how sensitive credentials may be exposed through prompt injection vulnerabilities.

---

### Flag #6 – Last message to the chatbot

- **Objective:** Identify the last message sent by the attacker to the AI chatbot.  
- **Approach:** Followed the full HTTP stream of the attacker’s conversation and reviewed the last JSON entries to find the attacker’s final message.  
- **Result:** [REDACTED]  
- **Notes:** Reinforced the importance of examining entire conversations chronologically to capture start-to-end attacker actions.

---

### Flag #7 – Remote access timestamp

- **Objective:** Find the time when the attacker remotely accessed Cogwork Central Workstation.  
- **Approach:** Analyzed logs inside the provided disk image, specifically TeamViewer-related files. Located entries showing login time and username shortly after the prompt injection attack.  
- **Result:** [REDACTED]  
- **Notes:** Gained experience in correlating network compromise with host-based artifacts such as remote access tool logs.

---

### Flag #8 – RMM Account name

- **Objective:** Identify the RMM Account name used by the attacker.  
- **Approach:** From the same TeamViewer log file, extracted the RMM account name tied to the remote session.  
- **Result:** [REDACTED]  
- **Notes:** Understood how RMM software logs can be used to attribute attacker actions to specific accounts.

---

## Summary

- **What I learned:** Improved skills in analyzing PCAPs and disk images together, correlating network and host-based evidence, and identifying prompt injection techniques in chatbot interactions.  
- **Most useful tools/techniques:** Wireshark (Conversations, Endpoints, Follow TCP Stream), NBNS analysis, HTTP payload inspection, disk log analysis (TeamViewer).  
- **Biggest difficulty:** Distinguishing legitimate chatbot messages from attacker-injected prompts and correlating network evidence with host logs.  
- **Key takeaway:** Combining network forensics with host-based artifacts provides a fuller picture of attacker activity and strengthens attribution.  
