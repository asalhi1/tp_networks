# Flow Test Results (Lab 2 - TP2)

| No. | Test Description | Command / Action | Observed Output | Verdict |
| :--- | :--- | :--- | :--- | :--- |
| 1 | PC-IT to ERP Server | `ping 10.42.18.50` on PC-IT | Reply from 10.42.18.50 | Permitted |
| 2 | Guest to ERP Server | Move PC-IT to VLAN 40, `ping 10.42.18.50` | Request timed out | Denied |
| 3 | PC-IT to PLC | `ping 10.42.64.50` on PC-IT | Request timed out | Denied |
| 4 | Supervision to PLC (Building A down) | Shut `CC-A` & `FW-A`, `ping 10.42.64.50` on PC-SUP | Reply from 10.42.64.50 (routed locally by CC-B) | Permitted |
| 5 | SSH to `CC-A` | `ssh -l secours 10.42.0.2` from PC-IT, then from 10.42.18.20 | Denied (PC-IT), Permitted (10.42.18.20) | Logged & Permitted |
| 6 | Rogue DHCP Server | Start DHCP service on test PC | Offers blocked by DHCP snooping | Denied |
| 7 | MAC limit violation | Set max 1, attach 2nd MAC address | Port security violation logged (restrict mode) | Denied |
| 8 | Loss of `CC-A` alone | Shut `CC-A` | OSPF & VRRP failover to CC-B (~40s) | Permitted |
| 9 | Complete loss of Building A | Shut `CC-A`, `FW-A`, `ACC-A-01` | OT local routing maintained on CC-B | Permitted |
| 10 | Guest to Admin Interface | `ssh -l secours 10.42.0.2` from VLAN 40 | Connection refused | Denied |
| 11 | Loss of `CC-B` alone | Shut `CC-B` | `CC-A` takes over Building B OT VLANs | Permitted |
