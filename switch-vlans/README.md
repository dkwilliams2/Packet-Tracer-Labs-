# Lab: Configure Switch VLANs and an 802.1Q Trunk

Created two VLANs on two switches, assigned access ports, and connected the switches with an 802.1Q trunk so each VLAN can reach across both switches.

## Topology

```
   VPC1 (192.168.1.1)                      (192.168.1.2)
   VPC2 (192.168.2.1)                      (192.168.2.2)
        |  |                                    |  |
   Et0/0 Et0/1                             Et0/0 Et0/1
        SW1  Et0/2 ===== 802.1Q trunk ===== Et0/2  SW2
```

| VLAN | Name       | Ports (each switch) | Subnet         |
|------|------------|---------------------|----------------|
| 10   | MARKETING  | Et0/0 (access)      | 192.168.1.0/24 |
| 20   | ACCOUNTING | Et0/1 (access)      | 192.168.2.0/24 |
| -    | Trunk      | Et0/2               | Allows 10, 20  |

## What was configured

- VLAN 10 (MARKETING) and VLAN 20 (ACCOUNTING) on both switches
- Et0/0 and Et0/1 as access ports in VLANs 10 and 20
- Et0/2 as a trunk using dot1q encapsulation, allowing only VLANs 10 and 20
- VPC IP addresses for testing

The full switch config is in [`configs/switch-vlans.txt`](configs/switch-vlans.txt).

## Verification

| Check | Command | Result |
|-------|---------|--------|
| VLANs and port assignments | `show vlan brief` (SW1, SW2) | VLAN 10 on Et0/0, VLAN 20 on Et0/1. Et0/2 is not listed because it is a trunk |
| Trunk status | `show interfaces e0/2 trunk` (SW1) | Mode on, 802.1q, trunking, VLANs 10 and 20 allowed |
| Trunk details | `show interfaces e0/2 switchport` (SW2) | Operational mode trunk, dot1q, VLANs 10 and 20 enabled |
| VLAN 10 across trunk | `ping 192.168.1.2` from VPC1 | 5/5 replies |
| VLAN 20 across trunk | `ping 192.168.2.2` from VPC2 | 5/5 replies |

Screenshots are in [`evidence/Lab_Proof_Switch_VLANs.pdf`](evidence/Lab_Proof_Switch_VLANs.pdf).

## Troubleshooting log

1. **Pings failed at first ("host not reachable")**: Each VLAN only existed locally on each switch. Fix: configured Et0/2 as an 802.1Q trunk. After that, pings succeeded.
2. **"Invalid input" on trunk commands**: These were caused by typos (`dotiq` instead of `dot1q`, `confgiure` instead of `configure`). Fix: retyped the commands correctly.
3. **Wrong VPC IP**: I typed `192.186.1.1` instead of `192.168.1.1`. Fix: re-entered the address.

## Takeaways

- An access port carries one VLAN, and a trunk carries many VLANs using 802.1Q tags.
- Without a trunk, hosts in the same VLAN on different switches cannot talk to each other.
- `switchport trunk allowed vlan` limits the trunk to only the VLANs it needs.
- On some switch models, `switchport trunk encapsulation dot1q` has to be set before `switchport mode trunk`.
- Trunk ports do not appear in `show vlan brief`. Use `show interfaces trunk` to check them.
