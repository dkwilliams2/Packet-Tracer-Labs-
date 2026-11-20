# 1. Scope and Methodology

## Scope

**In scope**

- Network devices at both sites: Router1, Router2, Switch1, Switch2
- How the devices are managed: SSH access, accounts, passwords, and configuration handling
- Network design: VLANs, trunking, management interfaces, and Internet connections

**Out of scope**

- End-user PCs, servers, and applications
- Physical security of the buildings
- Cloud services and third-party vendors

## Approach

1. **Identify assets.** I listed the devices and the data that passes through them.
2. **Identify threats and vulnerabilities.** I reviewed the device configurations and the problems I ran into while configuring them.
3. **Score each risk.** I used likelihood times impact, on a 1 to 5 scale for each.
4. **Map controls.** I tied each risk to NIST CSF 2.0 subcategories and NIST SP 800-53 Rev. 5 controls.
5. **Plan the treatment.** I chose mitigate, accept, transfer, or avoid for each risk and set priorities.

## Risk Scoring

**Likelihood**

| Score | Level | Meaning |
|-------|-------|---------|
| 1 | Rare | Not expected in the next 3 years |
| 2 | Unlikely | Could happen in the next 3 years |
| 3 | Possible | Could happen in the next year |
| 4 | Likely | Expected in the next year |
| 5 | Almost certain | Expected within months, or already happening |

**Impact**

| Score | Level | Meaning |
|-------|-------|---------|
| 1 | Minimal | No noticeable effect on operations |
| 2 | Minor | A short disruption at one site, under 2 hours |
| 3 | Moderate | One site down for most of a day, or limited data exposure |
| 4 | Major | Both sites disrupted, or customer or billing data exposed |
| 5 | Severe | Extended outage, or a breach requiring legal notification |

**Risk rating** = Likelihood x Impact

| Score | Rating | Required action |
|-------|--------|-----------------|
| 15 to 25 | High | Fix within 30 days |
| 8 to 14 | Medium | Fix within 90 days |
| 1 to 7 | Low | Fix when possible, or accept |

## Frameworks Used

- **NIST Cybersecurity Framework (CSF) 2.0:** Govern, Identify, Protect, Detect, Respond, and Recover
- **NIST SP 800-53 Rev. 5:** detailed controls that back up the CSF outcomes
- **NIST SP 800-30 Rev. 1:** guidance for conducting risk assessments
