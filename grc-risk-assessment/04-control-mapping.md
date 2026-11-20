# 4. Control Mapping

Each risk is mapped to the NIST CSF 2.0 outcome it falls short of and to the NIST SP 800-53 Rev. 5 controls that would close the gap.

| Risk | NIST CSF 2.0 | NIST SP 800-53 Rev. 5 | Gap |
|------|--------------|-----------------------|-----|
| R-01 SSH open to the Internet | PR.AA-05 Access permissions are managed and enforced. PR.IR-01 Networks are protected from unauthorized logical access. | AC-17 Remote Access. SC-7 Boundary Protection. | No source-address restriction on the VTY lines |
| R-02 Shared admin account | PR.AA-01 Identities and credentials are managed. PR.AA-03 Users are authenticated. PR.AA-05 Least privilege is applied. | AC-2 Account Management. AC-6 Least Privilege. IA-2 Identification and Authentication. IA-5 Authenticator Management. | One account for everyone, no MFA, and no individual accountability |
| R-03 No config backups | PR.DS-11 Backups of data are created, protected, maintained, and tested. RC.RP-03 Backup integrity is verified before use. | CP-9 System Backup. CM-2 Baseline Configuration. | Configs exist only on the devices themselves |
| R-04 No centralized logging | PR.PS-04 Log records are generated and made available for monitoring. DE.CM-01 Networks are monitored. | AU-2 Event Logging. AU-6 Audit Record Review. AU-9 Protection of Audit Information. | Logs are lost on reboot, and no one reviews them |
| R-05 No change control | PR.PS-01 Configuration management practices are established and applied. GV.PO-01 Cybersecurity policy is established. | CM-3 Configuration Change Control. CM-5 Access Restrictions for Change. | Changes aren't reviewed, tested, or recorded |
| R-06 Management on VLAN 1 | PR.IR-01 Networks are protected from unauthorized access. PR.AA-05 Access is enforced. | SC-7 Boundary Protection. AC-4 Information Flow Enforcement. | No separate management network |
| R-07 No NTP | PR.PS-04 Log records are generated. DE.AE-03 Information is correlated from multiple sources. | AU-8 Time Stamps. | Timestamps can't be compared across devices |
| R-08 Single point of failure | PR.IR-03 Resilience mechanisms are implemented. | CP-8 Telecommunications Services. SC-6 Resource Availability. | No backup link or device (risk accepted) |
| R-09 Changing WAN IPs | ID.AM-03 Network data flows are maintained. PR.IR-01 Networks are protected. | CM-8 System Component Inventory. SC-7 Boundary Protection. | Static allow lists will break when an IP changes |
| R-10 No IR or recovery plan | RS.MA-01 The incident response plan is executed. RC.RP-01 The recovery plan is executed. | IR-8 Incident Response Plan. CP-2 Contingency Plan. | No documented plan exists |
| R-11 No login banner | GV.PO-01 Policy is established and communicated. | AC-8 System Use Notification. | No warning shown at login |
| R-12 No inventory | ID.AM-01 Hardware inventories are maintained. ID.AM-03 Network communication is documented. | CM-8 System Component Inventory. PL-2 System Security and Privacy Plans. | Closed by this project |

## Coverage by CSF Function

| Function | Risks | Observation |
|----------|-------|-------------|
| Govern | R-05, R-10, R-11 | No written security policies, and roles are informal |
| Identify | R-09, R-12 | The inventory now exists and needs a regular update schedule |
| Protect | R-01, R-02, R-03, R-06, R-08 | Where most of the risk is concentrated |
| Detect | R-04, R-07 | There is effectively no detection capability today |
| Respond | R-10 | No plan |
| Recover | R-03, R-10 | Recovery depends on backups that don't exist |
