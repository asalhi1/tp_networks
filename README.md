# Atlas Industrie -- network architecture repository

Design of the Atlas Industrie network, the fictitious company of the
"Advanced Network Architectures" course. One folder per object type;
the addressing plan is authoritative in `data/vlans.yml`.

Local check: `python3 scripts/check_vlans.py` from the repository root.
Does not validate IPv6 prefixes, presence of mandatory fields, nor consistency
between VLAN, zone and subnet.

IPv6 prefix: fd9b:63af:5b8e::/48

To ensure local compliance checks run automatically before every commit, configure the versioned Git hook after cloning:

```bash
git config core.hooksPath hooks
```
