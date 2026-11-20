# 6. Executive Summary

**To:** Riverbend Supply Co. leadership
**Subject:** Network risk assessment results

## Bottom Line

The network works and has a solid technical base: encrypted remote access, strong encryption keys, and protected passwords. However, **4 high-rated risks** could let an outsider take control of the network or slow down recovery from an outage. All four can be fixed within 30 days at **little or no cost**.

## Top 4 Risks

1. **Remote login is open to the whole Internet.** Anyone can try to guess the admin password. *Fix: only allow logins from the IT office.*
2. **Everyone shares one admin password.** One leak exposes every device, and we can't tell who made a change. *Fix: give each admin their own account.*
3. **There are no backups of the device settings.** If a device fails or is misconfigured, it would have to be rebuilt from memory. *Fix: automatic daily backups.*
4. **There is no record of who logs in.** We couldn't detect or investigate a break-in. *Fix: send login records to a central server.*

## What Happens After the Fixes

- The 4 high risks drop to low.
- The remaining medium risks are addressed within 90 days through process changes: change control, time sync, and an incident plan.
- One risk is accepted: each site has only one Internet connection. This will be reviewed every year.

## Decisions Needed

| Decision | Recommendation |
|----------|----------------|
| Approve Phase 1 fixes | Approve. No cost, about 4 hours of IT time |
| Approve a small syslog/backup server | Approve. It can run on existing hardware |
| Accept the single-Internet-link risk | Accept for now, and review in 12 months |
