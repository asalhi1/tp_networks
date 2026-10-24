# Diagnostic report Lab 2

## 1. What was implemented
- OSPF Area 0 running in the global routing table between CC-A and CC-B with MD5 authentication and `passive-interface default`.
- VRF-Lite network segmentation across four VRFs (GESTION, IT, INVITES, OT) with localized VRRP gateways and static subinterface default routing towards firewalls.
- Hardened management plane: RADIUS AAA with local break-glass `secours` account, SSH v2 enforced, restricted management ACL (`ADMIN`), SNMPv3, NTP, and Syslog logging over GESTION VRF.
- Port protections on access switches: DHCP Snooping, Dynamic ARP Inspection, BPDU Guard, and MAC limiting.

## 2. The eleven tests and their results
Refer to `tests/resultats-tp2.md` for individual command outputs and verdicts across all 11 positive and negative test cases.

## 3. The fault diagnosed
- **Symptom observed:** OSPF neighbor state stuck in `ExStart` / `Exchange` state and never reaching `FULL`. Ping between inter-core addresses succeeds.
- **Diagnostic command:** `show ip ospf interface GigabitEthernet0/0` compared on both cores.
- **Cause:** Mismatched MTU settings on the inter-core link interfaces.
- **Fix applied:** Configured identical MTU (`ip mtu 1500`) on both `CC-A` and `CC-B` interfaces and ran `clear ip ospf process`.
- **Validation test:** `show ip ospf neighbor` returned to `FULL/-` state.

## 4. Measurements, and what they really measure
- Dead-timer expiration (~40 seconds) measures failure detection time and route withdrawal duration.
- **Critical Note:** Because there is a single physical inter-core link in this topology, this timer measures route withdrawal, NOT path reconvergence onto a backup link.

## 5. Accepted limits
1. **Firewall Pair HA:** High-availability state synchronization, failover timers, and split-brain scenarios between FW-A and FW-B were not simulated.
2. **OT Port Security:** 802.1X is not deployed in OT zones; static MAC limiting is an accepted weak control to prioritize operational continuity.
3. **Compliance Script Scope:** `scripts/check_compliance.py` performs static regex pattern matching on configuration files and does not validate active runtime network behavior.
