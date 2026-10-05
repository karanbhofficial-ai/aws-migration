# RAID and status register seeded from S02

Updated 6 October 2026. Entries below are proposed or source-derived until an owner confirms them. Airflow remains a separate project; the shared RAID request is treated as a coordination task, not scope merging.

## Risks

| ID | Risk | Impact | Proposed treatment | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| R-S02-01 | Screenshot inventory may contain duplicate, alias or conflicting server records | Incorrect scope, missed consumers or duplicate requests | Reconcile against Data SRE/ServiceNow export using canonical IDs | TBD | Open |
| R-S02-02 | Direct or Vault-mediated consumers may be missed | Application failure after migration or retirement | Require both direct-use and Vault-use checks per server | TBD | Open |
| R-S02-03 | Vault/service-account access is not ready | Discovery and POC validation delay | Raise authorized requests and record request IDs/approvals | TBD | Open |
| R-S02-04 | Historical POD responses may not reflect current state | False completion or stale ownership | Refresh every status and retain screenshot date as historical context | TBD | Open |
| R-S02-05 | A development server may appear unused after key-pair testing while another consumer remains | Premature retirement or missed migration | Require consumer clearance and usage evidence before disposition | TBD | Open |
| R-S02-06 | Three-month full migration horizon may be constrained by incomplete discovery and access | Schedule slippage and rushed validation | Baseline scope and access early; report forecast mismatch | TBD | Open |

## Assumptions to validate

| ID | Assumption | Validation |
| --- | --- | --- |
| A-S02-01 | RHEL 8 rows are in the migration scope | Scope owner and central inventory confirmation |
| A-S02-02 | `RITM006971658` can be used as the Data SRE request template | Data SRE/request owner confirmation |
| A-S02-03 | One ServiceNow request per shared-server group is the accepted process | ServiceNow/Data SRE process confirmation |
| A-S02-04 | The application team can obtain consumer and POC details but does not provision or migrate servers | Responsibility confirmation and handoff checklist |

## Issues

| ID | Issue | Evidence | Action |
| --- | --- | --- | --- |
| I-S02-01 | Current authoritative server list is not present in this project | S02 screenshots show partial rows only | Complete WP01 |
| I-S02-02 | `npsprod-netezza-1` appears alongside different account/context labels | S02-01 and S02-09 | Reconcile canonical identity |
| I-S02-03 | One candidate server is marked “not sure” and another may be temporary | S02-08 | Obtain owner and consumer confirmation |

## Dependencies

| ID | Dependency | Needed by | Responsible party to confirm |
| --- | --- | --- | --- |
| D-S02-01 | Data SRE authoritative server list and spreadsheet format | WP01-WP02 | Data SRE/request owner |
| D-S02-02 | SRE patching contact and requirements | WP03 | SRE |
| D-S02-03 | Vault and approved service-account access | WP04-WP06 | Access/Vault authority |
| D-S02-04 | AWS POC server readiness | WP08 and later validation | Central migration/automation team |
| D-S02-05 | Application owner and business validation responses | WP04-WP05 and P07 | Consuming teams |

## Status interpretation

No screenshot status is promoted to current completion. The project-level state remains **assessment/discovery in progress**, derived from the initiative slide and chat evidence, with no gate accepted in this project. Update status only with dated evidence and an owner.

