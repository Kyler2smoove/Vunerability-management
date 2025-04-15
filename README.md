
# Vulnerability Management Program Implementation

In this project, we performedthe implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  
[Draft Policy](https://docs.google.com/document/d/1CLSWm1_9JL1oUqgyNNwtPXW6FzXJ7ddVnSAUQTyqC8I/edit?usp=drive_link)

---

### Step 2) Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.


# Remediation Policy Discussion - Transcript

**Josh:**  
Hey, good morning Jimmy. How’s everything been lately? I know it’s been a busy few weeks.

**Jimmy:**  
Good morning, Josh. Yeah, it's been a bit hectic, but we’re hanging in there—thanks for asking.  
I had a chance to review the policy draft, and overall it makes sense. However, with our current staffing levels, we won’t be able to meet the aggressive remediation timelines—especially the 48-hour window for critical vulnerabilities.

**Josh:**  
I completely understand. It is a bit aggressive, especially at the start.  
Maybe we can extend the critical window to one week as a compromise.  
Then we can reserve the 48-hour requirement for truly severe zero-day vulnerabilities.

**Jimmy:**  
That sounds reasonable. We appreciate the flexibility.  
Could we also have some leeway in the beginning as we adapt to the remediation and patching process—just for the first few months?

**Josh:**  
Absolutely. Once the policy is finalized, we’ll officially launch the program,  
but we're planning to give all departments around six months to adjust and become familiar with the new process.  
Does that sound fair?

**Jimmy:**  
Thanks, Josh. We’ll do our best.  
I appreciate you including us in the decision-making process. It really helps us feel like we're part of the solution.

**Josh:**  
Of course—we're all in this together. Thanks for working with us.

**Jimmy:**  
No problem. Thanks for keeping the meeting short.

**Josh:**  
Yeah, those are my favorite kind. Take care.

**Jimmy:**  
See you later.


---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  
[Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link)
<div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/9afcdbc1-0493-4af2-9287-1cb9b8f59b40" alt="image" width="400">
</div>

---

### Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  


# Scheduled Credential Scans Discussion - Transcript

**Josh:**  
Morning Jimmy.

**Jimmy:**  
Good morning. I heard you’re ready to conduct some scans?

**Josh:**  
Yep. Now that our vulnerability management policy is in place, I wanted to get started on conducting some scheduled credential scans of your environment.

**Jimmy:**  
Sounds good to me. What’s involved? How can we help?

**Josh:**  
We’re planning to schedule weekly scans of the server infrastructure.  
We estimate it’ll take about 4 to 6 hours to scan all 200 assets.  
We’ll need you to provide some administrative credentials, which will allow the scan engine to remotely log into the targets and better assess them.

**Jimmy:**  
Whoa, whoa—hold on there. What does scanning actually entail? I’m a bit worried about resource utilization.  
Also, you want admin credentials to all 200 machines? That doesn’t sound safe.

**Josh:**  
Those are valid concerns.  
The scan engine sends different types of traffic to the servers to check for the existence of certain vulnerabilities.  
That includes looking into the registry, checking for outdated software, and identifying insecure protocols or cipher suites—so that’s why credentials are required.

**Jimmy:**  
I see. Well, as long as it doesn’t bring the servers offline, I guess we should be okay.

**Josh:**  
Absolutely. Let’s just scan a single server for now and keep an eye on resource utilization.

**Jimmy:**  
Not a bad idea.

**Josh:**  
Great. Also, for the credentials—can you set up something in Active Directory for us?  
Maybe create Active Directory credentials and leave them disabled until we’re ready to scan.  
Then enable them during the scan and disable or deprovision the account afterward. Kind of like a just-in-time access setup.

**Jimmy:**  
That sounds good. I’ll ask Susan to get started on the automation for the account provisioning.

**Josh:**  
Awesome. Okay—talk soon.

**Jimmy:**  
Yeah, that sounds good. I’ll get back to you once the credentials are set up.

**Both:**  
See you later.


---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/937cccbd-36bb-4445-97b9-e915085cda81" style="border: 2px solid black;">

[Scan 1 - Initial Scan](https://drive.google.com/file/d/1RBPVj_azKJMwmRZ8QILlb4hxIjQU3wQ7/view?usp=drive_link)




---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

[Remediation Email](https://github.com/joshmadakor1/lognpacific-public/blob/main/misc/remediation-email.md)

---

### Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 


# 🛡️ Vulnerability Management Meeting Notes  
**Date:** April 14, 2025  
**Participants:**  
- Jimmy (Security Engineer)  
- Kyler Williams (Cybersecurity Support Analyst)  

---

## 🧠 Summary

- ✅ No performance or service disruption during the vulnerability scan.  
- ⚠️ Multiple vulnerabilities found due to:
  - Outdated software (e.g., **Wireshark**)
  - Misconfigured user permissions
  - Deprecated protocols and cipher suites

---

## 🔍 Key Findings

- **Wireshark** is severely outdated on several servers.  
- The **Guest account** is a member of the **local Administrators group** — a major security risk.  
- **TLS 1.0/1.1** and **medium-strength cipher suites** are enabled and need to be disabled.  
- A **self-signed certificate** is present — expected, low risk.  
- Some **Microsoft Edge Chromium** vulnerabilities may already be patched via Windows Update.  
- Server configurations appear **uniform**, suggesting a streamlined remediation process.

---

## 🛠️ Action Items

- ❌ Uninstall **Wireshark** from all affected servers  
- 🔐 Remove **Guest** from the **Administrators** group  
- 🔧 Disable **TLS 1.0/1.1** and weak ciphers  
- 🔄 Verify Windows Update is patching Edge and OS vulnerabilities  
- 💻 Create **PowerShell remediation scripts/packages**  
- 📝 Submit changes to the **Change Control Board (CCB)**

---

## 💬 Conversation Log

> **Jimmy:** Morning Jimmy how are you doing?  
> **Kyler:** Not bad for a Monday. And yourself?  
> **Jimmy:** I'm still alive so I can't complain. But before we get into the vulnerabilities, how did the actual scan go on your end?  
> **Kyler:** The scan went well. We were monitoring them and aside from all the open connections, we would have never known a scan was taking place.  
> **Jimmy:** Yeah, that's good news. I kind of expected that much. We can keep monitoring going forward but I don't expect we'll have any issues with resource utilization. Do you mind if I dive into the vulnerability findings?  
> **Kyler:** Yeah absolutely.  
> **Jimmy:** Cool. So basically, the majority of these vulnerabilities come from Wireshark being installed. You can see all these Wireshark ones—it’s just super out of date.  
> One interesting thing I did find is that the local **Guest account** belongs to the **Administrators group**. I'm not sure why that is.  
> Also, some of these might be automatically resolved by Windows Updates—like this Microsoft Edge Chromium one.  
> The self-signed certificate one we don’t have to worry about—it’s just the computer's default cert.  
> But the TLS 1.1 and 1.0 protocols and medium-strength cipher suites should be addressed.  
> So we’re mainly looking at: Wireshark, the protocols/cipher suites, and the guest account.  
> **Kyler:** Very interesting. The good news is I suspect most of our servers are going to have the same vulnerabilities—hopefully that makes things easier during remediation.  
> **Jimmy:** Yeah, that's actually good news. A uniform loadout. Do you foresee any issues with remediating any of these specifically?  
> **Kyler:** I highly doubt there will be any issues. We’ll run it through the next Change Control Board. Uninstalling Wireshark and fixing the guest account shouldn’t be a problem.  
> **Jimmy:** I’ll go ahead and get started on building out some remediation packages for you to kind of make your life easier.  
> **Kyler:** That sounds great. Oh, one question—do you have anything in place to fix the Windows Update-related vulnerabilities?  
> **Jimmy:** Oh yes, Windows Update is already handled. We’ve got patch management set up.  
> **Kyler:** Perfect. I’ll get started on researching and planning the remediations and I’ll follow up before the next Change Control Board.  
> **Jimmy:** Sounds good, talk to you soon.  
> **Kyler:** Cool cool, talk to you soon.

---

## 💡 Skills Demonstrated

- ✅ Vulnerability triage and analysis  
- ✅ Collaboration with senior security staff  
- ✅ Remediation planning and execution prep  
- ✅ Change Control Board process familiarity  
- ✅ PowerShell scripting for automation  
- ✅ Patch management verification  


---

### Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  


# Vulnerability Remediation Discussion – CAP Meeting Summary

### Key Topics:
- Removal of insecure protocols
- Removal of insecure cipher suites

---

**Speaker 1:**  
Next up on the list are a couple of vulnerability remediations for the server team:  
1. Removal of insecure protocols  
2. Removal of insecure cipher suites  

Josh from the Risk Department is working in conjunction with Jimmy from Infrastructure on this.

---

**Jimmy:**  
Normally I would walk through the technical aspects, but Josh actually built the solution for us and is more familiar. We're still getting used to the process.

---

**Josh:**  
Sure, I can explain.  
Insecure cipher suites and protocols on a system mean it's capable of negotiating and using deprecated algorithms. If it connects to a server that only supports insecure protocols, it might fall back to using them.

These are managed via the Windows Registry.  
We created a PowerShell script that:

- Disables all insecure protocols and cipher suites
- Enables secure, modern standards

It's a straightforward implementation.

---

**Another Attendee:**  
What if something goes wrong? Do we have a rollback plan?

---

**Josh:**  
Yes, absolutely.

- We’re doing a **tiered deployment**: pilot group → pre-production → full production.
- We also created an **automated rollback script** for each remediation, which restores original registry settings if needed.

---

**Attendee:**  
Got it. Since it's just registry updates, I’m not too concerned.

---

**Josh:**  
Exactly.

---

**Host:**  
Any more questions?  
Great — that wraps things up for this week’s CAP meeting. See you all next week!


---
### Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  

<img width="634" alt="image" src="https://github.com/user-attachments/assets/7b4f9ab2-d230-4458-ac0f-c0ff070ae79a">

[Scan 2 - Third Party Software Removal](https://drive.google.com/file/d/1UiwPPTtuSZKk02hiMyXf31pXUIeC5EWt/view?usp=drive_link)


#### Remediation Round 2: Insecure Protocols & Ciphers

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)

<img width="630" alt="image" src="https://github.com/user-attachments/assets/0e96120d-8ec9-4f76-8e42-79c752200010">

[Scan 3 - Ciphersuites and Protocols](https://drive.google.com/file/d/1Qc6-ezQvwReCGUZNtnva0kCZo_-zW-Sm/view?usp=drive_link)


#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1jVgikjfrV1YjOcL3QRT_oUB0Y82w22V7/view?usp=drive_link)


#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1tmDjeHl5uiGitRwWy8kFRi33q-nGi1Zt/view?usp=drive_link)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="https://github.com/user-attachments/assets/51f0aae8-7f36-4d90-b29f-5257e57155f9">

[Remediation Data](https://docs.google.com/spreadsheets/d/1FTtFfZYmFsNLU6pm8nTzsKyKE-d2ftXzX_DPwcnFNfA/edit?gid=0#gid=0)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
