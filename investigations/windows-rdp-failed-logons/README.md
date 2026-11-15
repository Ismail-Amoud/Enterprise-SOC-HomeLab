# Windows RDP Failed-Logon Investigation — Home SOC Lab

**Project type:** Personal defensive cybersecurity laboratory  
**Status:** Documented investigation of authentication failures; certain correlation claims remain unverified  
**Primary tools:** Windows Security Event Viewer, Wazuh, Proxmox VE; Sysmon present in the lab  
**Related infrastructure:** [Enterprise SOC HomeLab](../../README.md)

## Summary

A controlled sequence of failed Remote Desktop authentication attempts was documented against a Windows 11 workstation in a personal Proxmox-based lab. The project notes record **15 failed Windows logon events (Event ID 4625)**, investigation of Wazuh log collection, and detection activity associated with **Wazuh rule 60122**.

The repeated authentication failures support analysis of a possible **MITRE ATT&CK T1110 (Brute Force)** pattern; the specific password-guessing sub-technique **T1110.001** is a plausible contextual classification for the described deliberate invalid-password attempts. Failed authentication events alone do not establish a successful compromise.

This investigation uses the same infrastructure documented in the main Home Lab repository. It is **not an additional infrastructure build**.

## Laboratory context

| Component | Role |
|---|---|
| Proxmox VE | Hosts the virtual laboratory |
| Windows Server 2022 / Active Directory | Authentication services and lab host used to initiate the described test |
| Windows 11 | Destination workstation and Windows Security log source |
| Wazuh agent | Collection of configured Windows security events |
| Ubuntu-hosted Wazuh manager | Receipt, processing and examination of the events |
| Sysmon | Windows telemetry component available in the environment |

Machine hostnames, interface identifiers, internal IP addresses and other infrastructure details have been omitted from this public case study.

## Methodology reconstructed from the original project documents

1. Deliberately generate repeated invalid Remote Desktop authentication attempts in the lab.
2. Inspect Windows Event Viewer → Windows Logs → Security for Event ID **4625**.
3. Inspect Wazuh dashboard for matching observations. The original report notes an **initial search with no matching results**.
4. Check whether the Windows Wazuh agent is connected and collecting events.
5. Investigate received Windows events on the manager, including archived event records (the original report refers to `archives.json`).
6. Compare raw Windows log events with Wazuh alert records and investigate rule **60122**.
7. Assess repeated failed authentication in the context of MITRE ATT&CK **T1110** and document defensive recommendations.

**Important distinction:** This is the workflow *described in the earlier project documents*. The currently available public source does not contain raw query results or matching logs sufficient to independently reproduce every stated intermediate outcome.

## Documented findings and confidence

| Item | What the older documentation states | Publication assessment |
|---|---|---|
| Simulated activity | Repeated RDP password failures | Described lab scenario |
| Failed authentication | **15 Windows Security Event ID 4625** records | Documented in the existing home-lab timeline; original raw export not included |
| Wazuh detection | Rule **60122** identified for failed logons | Documented investigation observation |
| Wazuh collection | Events investigated through agent/manager and `archives.json` | Reported workflow; raw export not included |
| Correlated rule **60204** | Older project says one Level 10 alert was generated | **Not independently verified; do not present as a confirmed alert** |
| MITRE ATT&CK | **T1110**, with **T1110.001** discussed | Analyst mapping based on the described behavior; automatic mapping unverified |
| Successful access | Older report says no unauthorized access occurred | Not independently demonstrated from failed-logon records alone |
| Incident severity | Older report labels the simulated event “High / Level 10” | Depends on verification of rule 60204; do not claim confirmed severity |

## Technical interpretation

- **Event ID 4625** records a failed Windows logon. It is evidence of a failure, not by itself proof of a malicious actor.
- Wazuh alerts are separate from Windows source events. A source event, a matching rule and a correlated alert are distinct artifacts requiring separate verification.
- The original documentation proposes **T1110** as a technique association for repeated authentication attempts. The exact sub-technique depends on how those attempts were conducted.
- A **60204** correlation claim remains unverified. Repeated 4625 events and 60122 observations do not by themselves prove that the SIEM generated this specific correlation alert.
- The original notes describe an initially empty dashboard query. Checking Windows source logs and manager reception before concluding that collection failed is the key troubleshooting lesson.

## Defensive recommendations derived from the investigation

- Restrict RDP exposure to trusted administrative paths; use appropriate access controls and MFA where available.
- Review logon audit settings and investigate repeated failures using source, target, username and time window.
- Apply proportionate account lockout/throttling and strong authentication policies.
- Monitor both **4625** and subsequent **4624** successful logons to establish whether a failure pattern was followed by successful access.
- Validate Wazuh rule behavior against the actual configured rules and alert records before claiming correlation.
- Use Sysmon and relevant Windows logs for additional context when investigating suspicious activity.

**These are recommendations, not claims that the measures were implemented.**

## Lessons learned

1. Do not assume a SIEM has failed because a dashboard search initially returns nothing.
2. Check the original Windows event record before making a determination from derived alerts.
3. Verify the Wazuh agent-to-manager collection path separately from alert-generation logic.
4. Distinguish a failed login, a security alert, a correlation event and a confirmed incident.
5. Describe MITRE ATT&CK mapping as an analytical classification unless the precise automated tagging has been verified.

## Scope and integrity

- The project is a **personal lab investigation**, not production SOC employment.
- No successful compromise is claimed.
- Specific internal addresses, hostnames, account names, original screenshots, and the raw source repository's detailed diagrams are intentionally not reproduced here.
- A separate [source-reconciliation document](SOURCE-REVIEW.md) preserves the important reported details and contradictions that must be checked before any stronger public statement.

## Outcome

A Windows failed-authentication scenario was documented, with **15 reported 4625 events**, Wazuh collection analysis and rule **60122**, alongside a contextual MITRE ATT&CK **T1110** assessment. The case study demonstrates investigative methodology without conflating reported or hypothetical correlation outcomes with verified telemetry.
