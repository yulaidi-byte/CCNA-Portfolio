# Lab 01: Basic Topology Setup with VLAN Routing

## Objective

Set up a basic network topology with one router and two Layer 2 switches, configure VLANs, and route between them using router-on-a-stick (subinterfaces) since the switches are Layer 2 only and can't route.

## Topology

![Topology diagram](topology-diagram.png)

| Device | Interface | VLAN | IP Address |
|---|---|---|---|
| PC1 | F0 | — | 10.10.10.11/24 |
| SW1 (2960-24TT) | F0/1 | VLAN 10 | 10.10.10.10/24 |
| SW2 (2960-24TT) | F0/1 | VLAN 20 | 10.10.20.10/24 |
| R1 (1941) | G0/0.10 | VLAN 10 | 10.10.10.1/24 |
| R1 (1941) | G0/1.20 | VLAN 20 | 10.10.20.1/24 |

## What I Did

- Connected PC1 to SW2, and both switches to R1
- Created VLAN 10 on SW1 and VLAN 20 on SW2
- Assigned switch ports to their respective VLANs
- Configured router subinterfaces (`G0/0.10` and `G0/1.20`) on R1, each tagged with 802.1Q encapsulation to match its VLAN
- Assigned IP addressing per the table above
- Verified connectivity between VLANs through the router (inter-VLAN routing)

## Files

- `topology.pkt` — Packet Tracer file, open to view/interact with the full config
- `topology-diagram.png` — topology diagram (screenshot)

## Notes / What I Learned

Since the switches are Layer 2 only, they can't route between VLANs on their own. Router-on-a-stick solves this by using a single physical router interface, split into subinterfaces (one per VLAN), each configured with 802.1Q trunking and its own IP on that VLAN's subnet. This let traffic move between VLAN 10 and VLAN 20 through the router.
