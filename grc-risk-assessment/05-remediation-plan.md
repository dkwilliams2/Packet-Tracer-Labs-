# 5. Remediation Plan

The fixes are ordered by risk score and effort. Most of the High-rated risks can be fixed with configuration changes that cost nothing.

## Phase 1: Within 30 Days (High Risks)

### R-01: Restrict SSH to approved addresses

Only allow SSH from the IT admin's office IP or a VPN range. The address below is an example.

```
ip access-list standard MGMT-ONLY
 permit 198.51.100.10
 deny any log
!
line vty 0 4
 access-class MGMT-ONLY in
 exec-timeout 10 0
!
ip ssh time-out 60
ip ssh authentication-retries 3
login block-for 120 attempts 3 within 60
```

**Verify:** SSH works from the allowed IP and is refused from any other address. `show access-lists` should show hits on the deny line.

### R-02: Give each admin their own account

```
username jsmith privilege 15 secret <unique-password>
no username admin
```

- Use a separate account for each person, with a password of at least 15 characters.
- Long term: move to central authentication (TACACS+ or RADIUS) with MFA.

**Verify:** `show users` shows a named account for each session.

### R-03: Back up configurations

```
archive
 path tftp://10.1.1.50/$h-
 write-memory
 time-period 1440
```

- The device sends a copy of its config every time it's saved, and once a day.
- Do a test restore every quarter.

**Verify:** a backup file appears for each device, and `show archive` lists the copies.

### R-04: Send logs to a central server

```
logging host 10.1.1.50
logging trap informational
service timestamps log datetime msec
login on-failure log
login on-success log
```

**Verify:** a failed login shows up on the syslog server.

## Phase 2: Within 90 Days (Medium Risks)

| Risk | Action |
|------|--------|
| R-05 | Adopt a simple change process: request, peer review, maintenance window, record. Before every change, check the hostname with `show running-config \| include hostname`. |
| R-06 | Move switch management to a dedicated management VLAN (for example VLAN 99) and allow SSH only from the admin subnet. |
| R-07 | Point every device to the same NTP source with `ntp server <ip>`. Check with `show ntp status`. |
| R-09 | Ask the ISP for static WAN addresses, or put remote management behind a VPN. |
| R-10 | Write a one-page incident response plan and a recovery checklist, then test them once a year with a tabletop exercise. |

## Phase 3: When Possible (Low Risks)

| Risk | Action |
|------|--------|
| R-11 | `banner login ^Authorized access only. Activity is monitored.^` |
| R-12 | Done. Review the inventory every quarter. |

## Accepted Risk

**R-08 (single point of failure):** A backup Internet link costs about $50 to $100 a month per site. Management accepts this risk for now, and it will be reviewed every year or after any outage longer than 4 hours.

## Expected Residual Risk

| Risk | Before | After | Change |
|------|--------|-------|--------|
| R-01 | 20 High | 4 Low | Only approved addresses can reach SSH |
| R-02 | 16 High | 6 Low | Individual accounts make actions traceable |
| R-03 | 16 High | 4 Low | Tested backups allow fast recovery |
| R-04 | 16 High | 6 Low | Login events are kept and can be reviewed |
| R-05 | 12 Medium | 6 Low | Changes are reviewed before they go live |
