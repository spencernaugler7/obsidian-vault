---
source: https://cloudbreak.atlassian.net/browse/WEYI-890
created: 2026-10-06
---
## Description

ETL is currently sending the ServiceSeconds field as NULL for some transactions. The existing stored procedures do not properly handle the NULL value, which can result in incorrect service item data.

Please update the following stored procedures to properly handle NULL ServiceSeconds input:

- `sp_ExternalOPITransactionInsert`
- `sp_ExternalOPITransactionInsertBasedOnClient`
- `sp_ExternalOPITransactionInsertBasedOnPIN`
- `sp_ExternalOPITransactionInsertMartti`
- `sp_ExternalOPITransactionUpdate`

### Requirements

When the ETL input ServiceSeconds is NULL:

1. The corresponding record in the ServiceItemMaster table must have:
    - ServiceItemStatusCodeId = 2 (Cancelled)
2. The corresponding record in the ServiceItemDetail table must have:
    - ServiceSeconds = 0
3. The corresponding record in the RequestReportTime table must have:
    - ServiceSeconds = 0
    - ServiceMinutes = 0

When ServiceSeconds contains a valid non-NULL value, the existing behavior should remain unchanged.

### Acceptance Criteria

- All five stored procedures correctly handle NULL ServiceSeconds.
- A transaction with ServiceSeconds = NULL results in:
    - ServiceItemMaster.ServiceItemStatusCodeId = 2
    - ServiceItemDetail.ServiceSeconds = 0
- A transaction with a non-NULL ServiceSeconds value continues to follow the existing logic without changes.
- The behavior is consistent across all five stored procedures.
- Existing transactions and functionality are not impacted.