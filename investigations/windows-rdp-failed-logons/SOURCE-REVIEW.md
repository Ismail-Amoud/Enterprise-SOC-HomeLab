# Source Review — Consolidation Before Retiring the Standalone RDP Repository

**Source repository:** `SOC-Lab-001-Windows-Brute-Force-Investigation` (reviewed on 2026-11-15).  
**Destination:** Enterprise SOC HomeLab → `investigations/windows-rdp-failed-logons/`.

This is a **consolidation and source-attribution record**, not a claim that all original artifacts have been independently reproduced. The original repository contains **12 Markdown documents and two PNG diagrams**. This summary preserves their substantive technical topics, but **does not replace a full backup of all original files, images or Git history**.

## Source document inventory (12 Markdown files)

| Original path | Essential content preserved here |
|---|---|
| `README.md` | Scenario, environment, workflow, detection and MITRE overview |
| `01-Documentation/1-Executive_summary.md` | 15 failures; claimed Wazuh 60122/60204 behavior; impact statement |
| `01-Documentation/2-Investigation-Report.md` | Investigation procedure, agent and manager checks, archive lookup, findings |
| `01-Documentation/3-Attack-Timeline.md` | Reported order and time window of failed logons and Wazuh processing |
| `01-Documentation/4-Lessons-Learned.md` | Dashboard troubleshooting, source-event verification, SIEM correlation concepts |
| `01-Documentation/5-Roadmap.md` | Proposed future detection investigations (not evidence of completion) |
| `02-Technical-Analysis/1-Detection-Rules.md` | Wazuh 60122 and claimed 60204, rule levels, claimed correlation mechanism |
| `02-Technical-Analysis/2-MITRE-Mapping.md` | T1110, possible T1110.001, discussion of other brute-force variants |
| `02-Technical-Analysis/3-Indicators-of-Compromise.md` | Source/target, 4625, attempted RDP authentication, indicators and timestamps |
| `02-Technical-Analysis/4-Recommendations.md` | MFA, RDP restriction, account lockout, auditing, monitoring |
| `02-Technical-Analysis/5-Security-Implementation-Status.md` | Claimed implemented controls and plans; some claims unverified |
| `03-Lab-Environment/1-Lab_Environment.md` | Proxmox, Ubuntu/Wazuh, Windows Server AD, Windows 11, Sysmon, network |
 
## Two source image files — preserve independently

- `03-Lab-Environment/2-Network Diagram.png`
- `03-Lab-Environment/3-Architecture Diagram.png`

**These PNG files have not been copied into this repository**, in accordance with the public infrastructure privacy policy. They should be preserved in a private local backup prior to deleting the source repository.

## Source-reported details requiring verification

| Topic | Historical source statement | Why not adopted as independently verified |
|---|---|---|
| Rule 60204 | One high-severity / level 10 correlated alert | No actual 60204 alert record or matching verified query output in available public repository |
| Rule 60122 | Individual failed-logon alerts | Documented in the original and existing home-lab timeline, but no raw verified alert export published |
| Wazuh archive | Fifteen records in `archives.json` | Report narrative only; raw archive/query evidence absent |
| MITRE mapping | Automatic T1110 tagging by Wazuh | Analytical mapping plausible, but automatic tagging needs actual alert fields |
| 15 failures | Fifteen Windows 4625 records | Repeated in project docs; raw Windows EVTX not included |
| Source timestamps | Old timeline shows failed attempts from approximately 20:48:08–20:48:40 EDT | Timeline has no raw event references; do not publish exact timestamps as verified |
| UTC conversion | One source claims `2026-07-13T01:48` UTC corresponding to 20:48 EDT | **Contradiction:** 20:48 EDT on July 12 corresponds to **00:48 UTC on July 13** |
| Experiment date | Executive summary says July 12; other HomeLab materials date observed 4625 events July 13 | Needs event timestamps and timezone confirmation before harmonizing |
| Network isolation | Original environment says “isolated private network” | Later Windows VM could access Internet; full isolation not proven |
| No compromise | Original report asserts no unauthorized access | A set of failed logons does not independently establish the absence of successful access elsewhere |
| Raw artifacts | Source repeatedly says end-to-end confirmed | Actual raw logs and independently checkable evidence are not available in the source repository |

## Source-specific fields intentionally excluded from public case study

- Real internal IPs and original machine hostnames, administrator account name, and topology identifiers.
- Personal/alternate analyst identification that differs from the public portfolio identity.
- Raw screenshots, diagrams, exact firewall paths and access configurations.

Keep these values in private backup if relevant; they are not needed to communicate the public findings.

## Detected presentation problems in the source

1. The README describes a different file layout from what the repository actually contains.
2. The source repeatedly calls rule 60204 a confirmed correlated incident, although no raw proof is published.
3. The use of **“Indicators of Compromise”** for controlled failed-logon observations risks suggesting an actual compromise. “Detection indicators / observed artifacts” is more appropriate.
4. “Attack simulation”, “Wazuh alert”, “correlation event” and “incident” are sometimes conflated.
5. Some implementation statuses (including correlation and monitoring claims) are stated more broadly than the visible evidence supports.
6. The timeline and UTC representation are inconsistent.
7. The content duplicates the main Enterprise SOC HomeLab's infrastructure and RDP case study.
8. Parts of the report suggest an entire enterprise-like SOC was fully validated; this is broader than the confirmed evidence.

## Future investigation ideas from original roadmap — **not yet performed in this case study**

- PowerShell execution monitoring
- Windows process creation events
- Scheduled-task persistence
- Service creation
- Registry modification
- File integrity monitoring
- Local user creation
- Active Directory authentication anomalies
- Lateral movement
- Sysmon-based hunting
- Ransomware-style detection simulation

The original roadmap also mentions MFA, Suricata, Zeek, TheHive, SOAR, threat intelligence, Sigma and YARA as planned capabilities. **None are represented here as completed because they appear in the original as future improvements.**

## Before deleting the source repository

- [ ] Download GitHub's **Download ZIP** of the original repository and keep it offline.
- [ ] If retaining Git history is important, make a complete `git clone --mirror` backup.
- [ ] Preserve the two diagrams privately; do not publicly transfer them without review.
- [ ] Confirm the key documented result is present in the consolidated [investigation](README.md).
- [ ] Review any website/portfolio links pointing to the old repository.
- [ ] Consider making the old repository private or archived first as a reversible alternative to deletion.

No deletion or changes to the source repository were performed during consolidation.
