# 3. Risk Register

Scores use the 1 to 5 scales in [Scope and Methodology](01-scope-and-methodology.md). This register is also available as a [CSV file](risk-register.csv).

| ID | Risk | Assets | L | I | Score | Rating | Treatment |
|----|------|--------|---|---|-------|--------|-----------|
| R-01 | SSH on both routers accepts connections from any Internet address. Attackers can scan for it and try to guess the password. | A-01, A-03 | 5 | 4 | 20 | High | Mitigate |
| R-02 | One shared "admin" account with full access (privilege 15) uses the same password on all four devices. One leaked password exposes the whole network, and actions can't be traced to a person. | A-01 to A-04, D-02 | 4 | 4 | 16 | High | Mitigate |
| R-03 | Configurations are not backed up off the devices. In the lab, a config was saved to the wrong file ("show-config"), and no one would have noticed. | D-01 | 4 | 4 | 16 | High | Mitigate |
| R-04 | No logs are sent to a central server. Failed logins and config changes are only kept in a small memory buffer on each device and are lost on reboot. | A-01 to A-04 | 4 | 4 | 16 | High | Mitigate |
| R-05 | There is no change control. In the lab, the Switch2 script was run on Router2 and gave it the wrong hostname. This was only caught during testing. | A-01 to A-04 | 3 | 4 | 12 | Medium | Mitigate |
| R-06 | Switch management shares VLAN 1 with user traffic. Any user PC can reach the switch login. | A-02, A-04 | 3 | 3 | 9 | Medium | Mitigate |
| R-07 | Device clocks are not synced with NTP. Log timestamps won't line up during an investigation. | A-01 to A-04 | 4 | 2 | 8 | Medium | Mitigate |
| R-08 | Each site has one router and one Internet link. If either fails, that site goes offline. | A-01, A-03 | 2 | 4 | 8 | Medium | Accept (review yearly) |
| R-09 | The WAN addresses come from DHCP and can change. That breaks SSH access and any IP-based allow list. | A-01, A-03 | 3 | 3 | 9 | Medium | Mitigate |
| R-10 | There is no written incident response or recovery plan for network outages or compromise. | All | 3 | 4 | 12 | Medium | Mitigate |
| R-11 | No login banner warns unauthorized users. This weakens the legal position in a prosecution. | A-01 to A-04 | 2 | 2 | 4 | Low | Mitigate |
| R-12 | The network inventory and diagram were not documented before this assessment. | All | 3 | 2 | 6 | Low | Mitigate (done in this project) |

L = Likelihood, I = Impact

## Controls Already in Place

These lowered the scores above. Without them, several risks would be rated higher.

- SSH version 2 only, with Telnet disabled (`transport input ssh`)
- 4096-bit RSA keys
- Passwords stored as hashes (`secret`, not `password`)
- The trunk only allows the VLANs it needs (`switchport trunk allowed vlan 10,20` in the VLAN lab)

## Risk Heat Map

| Likelihood / Impact | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| **5** | | | | R-01 | |
| **4** | | R-07 | | R-02, R-03, R-04 | |
| **3** | | R-12 | R-06, R-09 | R-05, R-10 | |
| **2** | | R-11 | | R-08 | |
| **1** | | | | | |
