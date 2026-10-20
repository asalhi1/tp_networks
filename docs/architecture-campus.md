# Decision note architecture of the Atlas Industrie campus

## 1. Context and requirements
- Atlas Industrie requires network connectivity for Building A (IT/Head Office) and Building B (Production)[cite: 4].
- Production must continue uninterrupted even if Building A is destroyed or isolated[cite: 1].

## 2. Technical targets retained
- Distributed Collapsed Core Architecture across Building A (`CC-A`) and Building B (`CC-B`)[cite: 1, 4].
- Dual fiber routes with independent power (UPS A / UPS B)[cite: 1, 9].

## 3. The two architectures compared
- **S1 (Three-tier):** 2 modular cores, 4 distribution switches, 10 access switches, 2 firewalls (16 total devices)[cite: 11].
- **S2 (Distributed Collapsed Core):** 2 fixed L3 cores, 10 access switches, 2 firewalls (14 total devices)[cite: 4, 11].
- **S3 (Single-Site Collapsed Core):** 2 fixed L3 cores (both in A), 10 access switches, 2 firewalls (14 total devices)[cite: 11].

## 4. Five-year costing
*(All prices in MAD ex-VAT[cite: 10])*

* **Cost Assumptions:**
  * Access switches: $10 \times 27,000 = 270,000$ MAD[cite: 11]
  * Firewalls: $216,000$ MAD[cite: 11]
  * Core S1 (Modular): $2 \times 162,000 = 324,000$ MAD[cite: 11]
  * Core S2/S3 (Fixed): $2 \times 86,400 = 172,800$ MAD[cite: 11]
  * Distribution S1: $4 \times 54,000 = 216,000$ MAD[cite: 11]
  * Optics/Fiber: S1 = $129,600$ MAD | S2 = $108,000$ MAD | S3 = $86,400$ MAD[cite: 11]
  * Support: $10\%$ of CAPEX / year $\rightarrow 50\%$ over 5 years[cite: 11]
  * Operations: Devices $\times 1.5\text{ days} \times 5,400\text{ MAD} \times 5\text{ years}$[cite: 11]

* **Summary Table:**
| Scenario | Devices | CAPEX (MAD) | 5-Yr Support (MAD) | 5-Yr Ops (MAD) | TCO (5 Years) (MAD) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **S1 (Three-Tier)** | 16 | 1,155,600 | 577,800 | 648,000 | **2,381,400** |
| **S2 (Distributed Core)** | 14 | 766,800 | 383,400 | 567,000 | **1,717,200** |
| **S3 (Single-Site Core)** | 14 | 745,200 | 372,600 | 567,000 | **1,684,800** |

* **Financial Gaps:**
  * **S2 vs S1:** Saves **664,200 MAD** in TCO ($27.9\%$ cost reduction)[cite: 11].
  * **S2 vs S3:** S2 costs **32,400 MAD** more in TCO over 5 years (due to inter-site fiber routes)[cite: 11].

## 5. Decision and justification
- **Retained Architecture:** S2 (Distributed Collapsed Core)[cite: 1, 11].
- **Why not S3?** S3 places both core switches in Building A[cite: 11]. If Building A experiences a site outage or fire, Building B's production stops completely, violating the mandate[cite: 1, 11].
- **Downtime Justification:** S2 costs 32,400 MAD extra over 5 years (6,480 MAD/year)[cite: 11]. At an outage cost of 108,000 MAD/hour, S2 pays for itself if it prevents just **18 minutes of production downtime** over 5 years ($32,400 / 108,000 = 0.3\text{ hours} = 18\text{ mins}$)[cite: 11].

## 6. Risks and points of failure
- **Single Access Switch Failure:** End-devices attached to a single access switch are not dual-homed; access switch failure impacts local groups[cite: 11].
- **Fibre Common Cause:** Both fiber routes meet at the courtyard trench; simultaneous physical cuts stop inter-site core synchronization[cite: 9, 11].
- **Availability Ceiling:** Dual-core redundancy does not achieve 99.999% uptime due to non-redundant access switches and shared physical paths[cite: 11].

## 7. Assumptions and limits
- Inventory discrepancy resolved: `CC-B` site updated from `A` to `B`[cite: 4].
- Civil works, cabling trenching labor, room cooling, and main AC grid power are excluded from CAPEX[cite: 11].
- Fiber routing paths in `campus-physique.mmd` are based on assumed campus geography[cite: 9].
