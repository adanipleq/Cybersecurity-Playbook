# ***SOC Analyst Casebook — Milestone 2***

**Author:** Ada Niple  
**Course:** Cisco CCNA / Cybersecurity coursework  
**Status:** Working analysis draft - not final product  
**Date:** November 22, 2026
**AI USE:** I used ChatGPT Edu to organize and input my work into a markdown format that could be read and used as reference with an index.

**Scope notes:** This draft uses evidence from separate course activities. The Splunk sign-in walkthrough, Wireshark protocol lab, and Cyber Hygiene report research are different scenarios. They are not evidence of one shared incident. They are examples of multiple incidents.

## 1. Revised purpose, scope, and success criteria

### Purpose

This casebook shows how an entry-level SOC analyst can review security evidence, explain what it supports, and identify what to check next. It uses course activities to practice careful analysis and clear handoffs. It does not claim that the lab activity findings describe a real attack against the student or one organization.

### Scope

This draft uses three completed activities:

- **Week 4 Splunk Activity 4.2:** a supplied walkthrough of Azure sign-in events for fictional Frothly accounts.
- **Week 5 Wireshark Lab 2.4.8:** packet captures I made in the CSE-LABVM virtual machine to compare browser, Telnet, and SSH traffic.
- **Week 6 Cyber Hygiene report research:** findings in a sample report and related vulnerability research.

The activities stay separate. The Splunk evidence is from a vendor-provided guided view, and I did not run the searches myself. The Wireshark captures are from my own lab work. The Cyber Hygiene findings come from a sample report and public reference pages; they are not proof that a live system is currently vulnerable.

### Success criteria

This casebook will be successful when it:

- Has at least six evidence items from at least two completed activities.
- Records the source, context, file or link, relevant fact, and limitation for each item.
- Connects each analysis conclusion to evidence IDs.
- Includes an alternative explanation and a next check for each analysis entry.
- Gives a cautious follow-up recommendation and identifies unresolved facts.
- Separates public, sanitized evidence from private raw files and sensitive information.

### Response to Milestone 1 feedback

**Milestone 1 feedback:** [Add the actual feedback here.]  
**What I changed:** [Explain the change you made in response.]  

For example, if the feedback asked for a narrower scope, I could explain that this draft focuses on interpreting course evidence and documenting next checks. I would keep that example only if it matches the feedback I actually received.

## 2. Evidence index

The evidence IDs below are used in the analysis entries. The source documents should be placed in the repository under `evidence/` only after reviewing them for private information. The `.pcapng` files contain raw traffic and should remain private.

| ID | Source/activity and observation context | File or link | Relevant fact | Limitation |
|---|---|---|---|---|
| **SPL-01** | Week 4 Activity 4.2, supplied Splunk guided view. The walkthrough searched Azure sign-in events for `199.66.91.253` with `sourcetype=ms:aad:signin`. | `evidence/Niple_W4_Activity42.docx` | The supplied view showed 51 events on August 20, 2018: 11 for `klagerfield@froth.ly` and 40 for `fyodor@froth.ly`. | Counts are events, not necessarily separate sessions. I interpreted the walkthrough and did not run the search myself. The accounts are part of a fictional training scenario. |
| **SPL-02** | Week 4 Activity 4.2, expanded event for Kevin’s account in the supplied Splunk view. | `evidence/Niple_W4_Activity42.docx` | One event showed a failed sign-in at 11:42:37 UTC. The failure reason indicated an invalid username or password. The event listed the Office 365 Portal, macOS, and Chrome 67.0.3396. | It does not identify who made the attempt, prove all attempts failed, or show whether the account was later disabled. |
| **WS-01** | Week 5 Wireshark Lab 2.4.8, personally captured browser traffic in CSE-LABVM. Display filter: `http or tls`. | `evidence/Niple_W5_Wireshark-v2.docx`; raw capture `Part1_Browser_2026-11-22.pcapng` (private) | The capture had 167 packets. The TLS 1.3 handshake was visible, but application data after the handshake was encrypted. | The encrypted payload does not reveal the exact webpage content or user actions. This was one lab session, not evidence of malicious activity. |
| **WS-02** | Week 5 Wireshark Lab 2.4.8, personally captured Telnet traffic on loopback `127.0.0.1`. Filter: `telnet`; Follow TCP Stream used to inspect the lab session. | `evidence/Niple_W5_Wireshark-v2.docx`; raw capture `Part2_Telnet_2026-11-22.pcapng` (private) | The capture had 633 packets; 48 matched the Telnet filter. The login text and typed commands appeared in plain text. | This was localhost traffic inside a lab VM, not traffic across a physical network. The raw capture included sensitive lab credentials, which were redacted from the submitted evidence. |
| **WS-03** | Week 5 Wireshark Lab 2.4.8, personally captured SSH traffic on loopback `127.0.0.1`. Filter: `ssh`. | `evidence/Niple_W5_Wireshark-v2.docx`; raw capture `Part3_SSH_2026-11-22.pcapng` (private) | The capture had 60 packets and no dropped packets. It showed SSH version banners and key exchange, followed by encrypted traffic. | It does not show the password, commands, or whether the login succeeded. This was a local practice session. |
| **VULN-01** | Week 6 Cyber Hygiene report research. Review of the sample report dated February 4, 2024. | `evidence/Niple_W6_427LAB.docx`; [sample Cyber Hygiene report](https://mccmeetingspublic.blob.core.usgovcloudapi.net/mangumok-meet-4e68e0eeaa63422eba40bf865ed5bbf1/ITEM-Attachment-001-53fe281a5382435b88a0fbb825f6fed9.pdf) | The report lists an Ivanti Connect Secure multiple-vulnerability finding as High, with a CVSS score of 7.8, affecting three hosts. | This is a finding in a dated sample report, not evidence of a current vulnerability on a real system. In the linked PDF, the vulnerability table appears in Section 10 as Table 7; Table 6 is the severity count table. |
| **VULN-02** | Week 6 research, Tenable reference for the Sun ONE JSP source disclosure finding. | `evidence/Niple_W6_427LAB.docx`; [Tenable reference](https://www.tenable.com/plugins/nessus/11658) | Tenable lists CVE-2003-0411. A specially changed request could expose JSP source code that may contain sensitive information. | The reference applies to a specific older product. The report does not show that anyone accessed source code. |
| **VULN-03** | Week 6 research, Tenable reference for the SSH Terrapin finding. | `evidence/Niple_W6_427LAB.docx`; [Tenable reference](https://www.tenable.com/plugins/nessus/187315) | Tenable lists CVE-2023-48795. The weakness may let a man-in-the-middle attacker interfere with SSH integrity checks. Tenable recommends an update with key-exchange protections or disabling affected algorithms. | A scanner finding does not prove an attack occurred. Tenable notes that this check looks at supported algorithms and does not check software versions. |

## 3. Analysis entries

### Analysis 1 — Failed Azure sign-in event in the supplied Splunk walkthrough

- **Question:** What does the evidence show about the sign-in attempt for Kevin’s account from `199.66.91.253`?
- **Method:** Reviewed the supplied Splunk walkthrough, including the IP search and Kevin’s expanded event. The search used `sourcetype=ms:aad:signin`. I did not run the search myself.
- **Evidence IDs:** SPL-01, SPL-02.
- **Supported conclusion:** The supplied view shows multiple sign-in events associated with the IP on August 20, 2018. One expanded event for Kevin’s account failed because the username or password was invalid. The available event does not show a successful sign-in for Kevin.
- **Alternative explanation:** A saved password on an old device or application could have caused a failed attempt. The evidence does not identify who initiated it.
- **Next check:** Review all events for Kevin’s account around that time. Compare timestamps, results, devices, and applications. Check account status and whether the IP was an approved network or VPN. Confirm any new facts in the actual authorized log source before taking action.

### Analysis 2 — What packet captures show about HTTP, TLS, Telnet, and SSH

- **Question:** Which traffic contents were readable in the lab captures, and what could an analyst infer from encrypted traffic?
- **Method:** Captured traffic in CSE-LABVM and used Wireshark display filters. For the browser capture I used `http or tls`; for the local Telnet capture I used `telnet`; for SSH I used `ssh`. I compared packet details and streams. Raw captures were kept in my private course workspace.
- **Evidence IDs:** WS-01, WS-02, WS-03.
- **Supported conclusion:** In this lab, HTTP and Telnet content appeared in plain text, while HTTPS/TLS application data and SSH session content were encrypted after setup. An analyst can still observe some metadata, such as endpoints, ports, packet sizes, timing, and protocol banners, but the encrypted captures did not reveal the page contents or SSH commands.
- **Alternative explanation:** Encrypted traffic is normal for HTTPS and SSH. Encryption by itself is not evidence of malicious activity. The lab captures also represent controlled localhost and browser exercises, not a production incident.
- **Next check:** For an actual alert, correlate network metadata with authorized endpoint, authentication, or server logs. Confirm the destination, user or process, and timing before deciding whether traffic is suspicious.

## 4. Proposed escalation or follow-up note

**Audience:** Tier 1 SOC analyst or identity administrator reviewing the supplied Frothly sign-in scenario.  
**Reason:** The supplied Splunk view shows repeated events from one IP involving two accounts, including one failed attempt for Kevin’s account.  
**Urgency rationale:** The evidence supports timely review, but it does not show a successful sign-in or prove account compromise. Treat this as a follow-up item rather than a confirmed incident until the rest of the authorized sign-in records are checked.  
**Unresolved facts:** Whether any sign-in succeeded; whether the events were separate sessions; who controlled the source IP; whether the device and application were expected; and whether the account was active at the time.  
**Suggested follow-up:** Review the complete sign-in history, compare device and application details, verify account status, and check whether the source IP belongs to an approved service. Record the result and escalate further if successful or otherwise suspicious activity is found.

## 5. Milestone 3 revision plan and evidence map

### Revision plan

For Milestone 3, I plan to:

1. Replace the Milestone 1 feedback placeholders with the actual feedback and the specific changes I made.
2. Add any missing screenshots or source notes needed to let a reader retrace my observations.
3. Keep the Splunk walkthrough, Wireshark lab, and Cyber Hygiene report in separate case sections.
4. Check each conclusion against its evidence IDs and keep unsupported claims out of the final version.
5. Improve readability by defining acronyms such as CVE, CVSS, TLS, and SSH when they first appear.
6. Review every public file for credentials, personal information, private comments, and unredacted network or account details.

### Public/private evidence map

| Evidence | Public repository use | Keep private or remove |
|---|---|---|
| Week 4 Splunk activity | A sanitized summary of the supplied view, clearly labeled as vendor-provided walkthrough evidence. | Any unredacted screenshots, private course information, or account data not needed for the analysis. |
| Week 5 browser capture | A short sanitized summary or redacted screenshot showing the filter and relevant packet details. | Raw `.pcapng` file if it contains cookies, tokens, browsing details, or other sensitive data. |
| Week 5 Telnet capture | A sanitized explanation that Telnet exposed lab session text; credentials must remain hidden. | Raw `.pcapng`, passwords, username, and unredacted Follow TCP Stream output. |
| Week 5 SSH capture | A sanitized summary or redacted screenshot showing the SSH filter and encrypted packet details. | Raw capture and any local credentials or private host details. |
| Week 6 report research | Public report link and concise findings with source links and report date. | Any private instructor notes or course-only comments. Do not present sample report findings as live organizational exposure. |
| Milestone feedback | Include only a brief summary of feedback relevant to the revision, if permitted. | Private peer messages or classmates’ work unless permission is given. |

## Source files used

- `Niple_W4_Activity42.docx` — Week 4 Splunk guided-view record.
- `Niple_W5_Wireshark-v2.docx` — Week 5 personally performed Wireshark lab and verification notes.
- `Niple_W6_427LAB.docx` — Week 6 Cyber Hygiene report research.
