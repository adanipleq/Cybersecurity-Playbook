# Cisco Lab 3.1.4: Threat Intelligence Report Comparison

> **Course Context:** Week 6 Resource Guide — Five-Step Report Comparison  
> **Sources Analyzed:** Cisco Talos 2025 Year in Review & CISA Cybersecurity Alerts and Advisories
## AI CLARIFICATION: I used Claude to format this markdown template with my answers from the 3.1.4 updated lab.
---

## Step 1 & Step 2: Source Records and Cited Claims

### Source 1: Cisco Talos 2025 Year in Review

* **Title:** *2025 Talos Year in Review: Speed, Scale, and Staying Power*
* **Author / Publisher:** Cisco Talos (Cisco Systems, Inc.)
* **Publication Date:** March 23, 2026
* **Source Type:** Vendor Annual Threat Intelligence Report
* **URL:** <https://blog.talosintelligence.com/2025yearinreview/>

#### Key Claims
1. **Zero-days and legacy tech are both major pain points:** Attackers hit organizations from opposite ends of the software lifecycle in 2025. On the new side, the *React2Shell* flaw (`CVE-2025-55182`) became the single most targeted vulnerability of the entire year just three weeks after its December disclosure. On the old side, nearly 40% of the top 100 exploited vulnerabilities succeeded simply because companies were still running unsupported, end-of-life (EOL) hardware.
2. **Attackers are logging in rather than breaking in:** Rather than relying solely on custom malware, threat actors leaned heavily on identity abuse. Fraudulent MFA device registrations jumped 178% over the previous year—with admin-managed enrollment flows targeted three times more often than standard user flows—while over a third of observed phishing emails came from inside compromised organizational accounts.

---

### Source 2: CISA Cybersecurity Alerts & Advisories Collection

* **Title:** *Cybersecurity Alerts & Advisories* (specifically Advisory AA26-237A: *A Tale of Two SOCs: Insights From Two Red Team Assessments* and the November 20, 2026 KEV Catalog Update)
* **Author / Publisher:** Cybersecurity and Infrastructure Security Agency (CISA)
* **Publication Date:** Ongoing rolling feed (featured advisories published August 25, 2026 – November 20, 2026)
* **Source Type:** Government / National CERT Operational Advisories
* **URL:** <https://www.cisa.gov/news-events/cybersecurity-advisories>

#### Key Claims
1. **Alert fatigue and cloud blind spots are slowing down SOCs (AA26-237A):** During red team assessments across critical infrastructure organizations, CISA observed that untuned security tools buried analysts in false positives, communication gaps between teams slowed down containment, and poorly monitored cloud environments gave attackers easy paths for lateral movement.
2. **Enterprise edge and core apps are under active attack (KEV Update, Nov 20, 2026):** CISA added four actively exploited vulnerabilities to its Known Exploited Vulnerabilities (KEV) Catalog on November 20, 2026, warning defenders to patch hard-coded credentials in Cisco Expressway (`CVE-2026-76466`), an authentication bypass in VMware vCenter (`CVE-2026-123890`), deserialization in Apache Roller (`CVE-2026-129448`), and JNDI injection in SAP NetWeaver (`CVE-2025-42884`).

---

## Step 3 & Step 4: Comparing the Two Sources

| Criteria | Cisco Talos 2025 Year in Review | CISA Cybersecurity Advisories |
| :--- | :--- | :--- |
| **Purpose** | Gives security leaders and defenders a big-picture look at how attacker tactics shifted over the past year to help guide long-term strategy, budgeting, and architecture upgrades. | Gives federal agencies and critical infrastructure teams urgent, actionable warnings so they can patch active exploits and fix immediate gaps in their detection workflows. |
| **Evidence Base** | Global telemetry from Cisco firewalls, endpoint agents, and email gateways, combined with sinkhole data and hands-on Cisco Talos Incident Response cases. | Direct findings from CISA red team assessments and incident response engagements, intelligence from federal and international partners, and verified exploit tracking for the KEV catalog. |
| **Currency** | **Annual retrospective:** Covers all of 2025 and was published in March 2026. Great for spotting broader trends, though it naturally doesn't cover brand-new threats emerging later in 2026. | **Rolling real-time updates:** Published multiple times a week (with KEV updates current through November 2026). Very timely for active defense, though each alert focuses narrowly on specific bugs or assessments. |
| **Limitations** | **Vendor perspective:** Data skews toward organizations using Cisco hardware and software, and the recommendations naturally align with Cisco's product ecosystem (network edge, identity, and lifecycle management). | **Sector focus and redacted details:** Geared primarily toward U.S. government and critical infrastructure networks; operational security rules often prevent CISA from sharing full attribution or every technical indicator publicly. |

---

## Step 5: Locally Testable SOC Question & Investigation Plan

### SOC Question to Investigate
> *"Over the last 30 days, have any user or admin accounts registered a new MFA device from an unusual IP or location—or started forwarding/sending spikes of internal email—and do we have any internet-facing appliances still running end-of-life or unpatched firmware?"*

### What We Need to Check Locally

- [ ] **1. Identity & MFA Logs (Entra ID, Okta, or Duo)**
  * Look for new MFA enrollment events (`Register security info` or `MFA factor added`), paying extra attention to registrations pushed through administrator or help-desk workflows.
  * Check the source IP, ISP/ASN, geolocation, and browser User-Agent on those events to catch impossible travel or social-engineered MFA resets.

- [ ] **2. Email & Mailbox Audit Logs (Microsoft 365 / Exchange or Google Workspace)**
  * Search for newly created inbox rules (`New-InboxRule` / `Set-InboxRule`) that quietly hide, delete, or forward incoming mail, alongside sudden spikes in internal-to-internal emails sent by a single user.
  * Tie any suspicious mailbox activity back to the user's sign-in session ID to see if an attacker is using a hijacked account to phish coworkers.

- [ ] **3. Asset Inventory & Vulnerability Scans (CMDB, Nessus, or Nmap)**
  * Pull a list of all public-facing edge devices and web apps—especially VPN gateways, collaboration servers like Cisco Expressway, and apps running React or Next.js.
  * Cross-check their firmware and package versions against vendor End-of-Life (EOL) dates and CISA's KEV list (`CVE-2025-55182`, `CVE-2026-76466`, etc.).

- [ ] **4. SIEM Alert Volume & Tuning Health (Applying CISA AA26-237A)**
  * Review the past 30 days of high-severity identity and cloud-control-plane alerts to compare total alerts fired against confirmed true positives, making sure noisy rules aren't burying real MFA or session-hijacking alerts.
