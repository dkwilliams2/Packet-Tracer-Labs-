# GRC Project: Network Risk Assessment for a Small Business

A risk assessment of a fictional two-site company. The company's network is based on the network I built in my [SSH Remote Management](../ssh-remote-management/) and [Switch VLANs](../switch-vlans/) labs. I identified the assets, scored the risks, mapped the gaps to the NIST Cybersecurity Framework (CSF) 2.0, and wrote a prioritized remediation plan.

**Note:** The company is fictional. The technical findings come from things I actually saw while configuring the lab equipment.

## Scenario

**Riverbend Supply Co.** is a fictional 40-person distributor with two offices:

- **Site 1 (main office):** Router1 and Switch1, with staff, the file server, and the billing workstations.
- **Site 2 (warehouse):** Router2 and Switch2, with inventory scanners and shipping PCs.

Each site connects to the Internet through its own router. One part-time IT administrator manages everything remotely over SSH.

## Deliverables

| # | Document | What it covers |
|---|----------|----------------|
| 1 | [Scope and Methodology](01-scope-and-methodology.md) | What was assessed, how risk was scored, and the frameworks used |
| 2 | [Asset Inventory](02-asset-inventory.md) | Network devices and data, with their owners and criticality |
| 3 | [Risk Register](03-risk-register.md) ([CSV](risk-register.csv)) | 12 risks scored by likelihood and impact |
| 4 | [Control Mapping](04-control-mapping.md) | Each risk mapped to NIST CSF 2.0 and NIST SP 800-53 controls |
| 5 | [Remediation Plan](05-remediation-plan.md) | Fixes in priority order, with owners, timelines, and IOS commands |
| 6 | [Executive Summary](06-executive-summary.md) | A one-page summary for management |

## Key Findings

| Rating | Count | Examples |
|--------|-------|----------|
| High | 4 | SSH open to the whole Internet, one shared admin password, no config backups, no logging |
| Medium | 6 | No change control, no time sync, management on VLAN 1, single point of failure at each site |
| Low | 2 | No login banner, no documented network inventory |

The top fix is restricting SSH so it only accepts connections from approved IP addresses, using an access list on the VTY lines. It's one config change, costs nothing, and lowers the highest-rated risk.

## Skills Demonstrated

- Risk identification, scoring, and treatment decisions (mitigate, accept, transfer, avoid)
- Mapping technical controls to NIST CSF 2.0 and NIST SP 800-53 Rev. 5
- Turning hands-on configuration work into business risk language
- Writing for both technical staff and management
