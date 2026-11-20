# CML Lab: Secure Remote Management with SSH

Configured SSH remote management for a two-site network in Cisco Modeling Labs (CML), then verified access from the Internet to each router and through each router to its switch.

## Topology

```
                    THE_INTERNET
                   /            \
        203.0.113.2              203.0.113.6   (DHCP)
           Router1                  Router2
        10.1.1.1/24              10.2.2.1/24
             |                        |
          Switch1                  Switch2
        10.1.1.2 (Vlan1)         10.2.2.2 (Vlan1)
        site1.lab                site2.lab
```

## What was configured

| Device  | Key settings |
|---------|--------------|
| Routers | Hostname, domain name, WAN via DHCP, LAN IP, local admin (privilege 15), SSH v2, 4096-bit RSA key, VTY lines set to SSH only with local login |
| Switches | Hostname, domain name, Vlan1 management IP, default gateway, local admin, SSH v2, RSA key |

Configs are in [`configs/`](configs/). Passwords are replaced with `<password>`.

## Verification

| Test | Command | Result |
|------|---------|--------|
| Internet to Router1 | `ssh -l admin 203.0.113.2` | `Router1#` |
| Router1 to Switch1 | `ssh -l admin 10.1.1.2` | `Switch1#` |
| Internet to Router2 | `ssh -l admin 203.0.113.6` | `Router2#` |
| Router2 to Switch2 | `ssh -l admin 10.2.2.2` | `Switch2#` |

Other checks: `show ip interface brief`, `show ip ssh`, `ping`.

## Troubleshooting log

1. **Script rejected ("Invalid input")**: I pasted the script at the `Router>` (user EXEC) prompt. Fix: run `enable` first so `configure terminal` works.
2. **Router1 to Switch1 timed out**: Switch1's Vlan1 had no IP and was administratively down. Fix: added `ip address 10.1.1.2 255.255.255.0`, `no shutdown`, and `ip default-gateway 10.1.1.1`.
3. **Saved to the wrong file**: I typed `copy running-config show-config` by mistake. Fix: ran `copy running-config startup-config`.
4. **203.0.113.6 showed a `Switch2#` prompt**: Router2 had the wrong hostname (Switch2's script had been run on it). Fix: `hostname Router2` and saved.
5. **Router1 to 10.2.2.2 unreachable**: This was expected. Each switch is reachable only through its own site's router, so the hop has to start from Router2.

## Takeaways

- Config commands need privileged EXEC (`#`), not user EXEC (`>`).
- A switch needs a management SVI (Vlan1), set to `no shutdown`, plus a default gateway before it can be reached remotely.
- SSH needs a hostname, a domain name, and an RSA key. Use SSH instead of Telnet because it encrypts the session.
- Always `copy running-config startup-config`.
