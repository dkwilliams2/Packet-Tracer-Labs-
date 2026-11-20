# 2. Asset Inventory

## Hardware

| ID | Asset | Site | Role | Management IP | Owner | Criticality |
|----|-------|------|------|---------------|-------|-------------|
| A-01 | Router1 | Site 1 | Internet edge and LAN gateway | 203.0.113.2 / 10.1.1.1 | IT Admin | High |
| A-02 | Switch1 | Site 1 | Access switch for the office | 10.1.1.2 (Vlan1) | IT Admin | High |
| A-03 | Router2 | Site 2 | Internet edge and LAN gateway | 203.0.113.6 / 10.2.2.1 | IT Admin | High |
| A-04 | Switch2 | Site 2 | Access switch for the warehouse | 10.2.2.2 (Vlan1) | IT Admin | Medium |

## Data and Information

| ID | Asset | Location | Sensitivity | Owner |
|----|-------|----------|-------------|-------|
| D-01 | Device configurations | Running and startup config on each device | Confidential (contains password hashes and the network layout) | IT Admin |
| D-02 | Admin credentials | Local accounts on each device | Restricted | IT Admin |
| D-03 | Billing and customer data | Crosses the Site 1 LAN | Confidential | Finance Manager |
| D-04 | Inventory and shipping data | Crosses the Site 2 LAN | Internal | Warehouse Manager |

## Network Segments

| Segment | VLAN | Subnet | Purpose |
|---------|------|--------|---------|
| Site 1 LAN | 1 | 10.1.1.0/24 | Users and switch management share one VLAN |
| Site 2 LAN | 1 | 10.2.2.0/24 | Users and switch management share one VLAN |
| Internet | - | 203.0.113.0/24 | Public addresses assigned by DHCP |

## Criticality Definitions

- **High:** If it goes down, the whole site stops working.
- **Medium:** If it goes down, work slows down but continues.
- **Low:** It can be down for several days with little effect.
