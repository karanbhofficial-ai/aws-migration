# Server inventory draft

Updated 6 October 2026 from source S02 screenshots. These are candidate records for reconciliation, not an authoritative inventory. `Unknown` means not established; it does not mean absent.

| ID | Account/context as visible | Environment | Host / alias | IP | Instance type | Source OS | Workload / consumer clue | Inventory status | Next verification |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| S02-SRV-01 | Not visible; development row | Development | `mrdw-oracle-dev-01` | `10.212.30.34` | `m4.2xlarge` | RHEL 8 | Oracle-related name only; workload unconfirmed | Candidate, unverified | Confirm account, region, architecture, consumers, owner and scope |
| S02-SRV-02 | `marriott distributed platform prod-654607264796` appears in one view | Production | `npsprod-netezza-1` | `172.30.33.218` | `t3.2xlarge` | RHEL 8 | Netezza-related name only; consumer unconfirmed | Candidate, conflicting context | Reconcile account/host identity with authoritative export |
| S02-SRV-03 | `marriott distributed platform prod-654607264796` / MDP-TCS context | Production | `mi-mdp-dpde-rev9-dp-prod` | `172.25.35.245` | `m5.2xlarge` | RHEL 8 | Message says a participant uses the server; exact app unknown | Candidate, unverified | Identify participant/team, app, service accounts and dependencies |
| S02-SRV-04 | `mariott distributed platform dev-279139051182` | Development or test (label not explicit) | Host not shown | Not shown | `r5.xlarge` | Unknown | Hotels Ops tests key-pair authentication; use may end after test | Candidate, possible retirement | Confirm whether test is complete and obtain consumer clearance |
| S02-SRV-05 | `mariott distributed platform prod-654607264796` | Production | Host not shown in this view | Not shown | `t3.2xlarge` | Unknown in this view | SRW application uses server | Candidate, consumer clue | Confirm hostname/IP/OS and SRW owner |
| S02-SRV-06 | `mariott distributed platform nonprod-521221133174` | Nonproduction | `zook1-perf1-aws-us-east-1` | `172.25.41.61` | `m5.2xlarge` | Unknown | Participant marked “not sure”; possible performance environment | Candidate, unverified | Confirm existence, owner, consumers, region and scope |

## Required canonical fields

For each confirmed record add AWS account ID, region, instance ID, hostname, private IP, environment, RHEL release, architecture, patch contact, application/consumer, technical owner, business owner, service accounts/Vault references, mounts, schedules, dependencies, criticality, proposed wave, migration disposition, evidence source and verification date.

## Reconciliation rules

Use the authoritative Data SRE/ServiceNow export as the source for server identity. Use application-owner responses and access evidence for consumer ownership. Treat screenshot rows as leads only. Link aliases to one canonical server ID after validation; keep the original labels in an alias field. Do not merge or retire records based on low load or a single person’s response.

