# Discovery and access action plan

This plan turns the S02 chat tasks into application-team work. The chat messages are project evidence; they do not authorize this assistant to raise ServiceNow, Vault or access requests. A named team member with the required authority must execute those actions.

## Work packages

| WP | Work | Owner | Inputs | Output / closure evidence | Status |
| --- | --- | --- | --- | --- | --- |
| WP01 | Obtain authoritative in-scope server list and spreadsheet format from Data SRE | Assigned application-team member, TBD | ServiceNow sample `RITM006971658` and current request process | Export with canonical server IDs, account, environment, OS and verification date | Unknown |
| WP02 | Divide servers into accountable discovery groups; record primary and backup | AWS migration application coordinator, TBD | WP01 list | Accepted allocation matrix | Unknown |
| WP03 | Contact SRE patching contact and confirm patch/access prerequisites | Assigned team member, TBD | Server list | Contact record, requirements and unresolved gaps | Unknown |
| WP04 | Identify direct and Vault-mediated consumers | Each server group owner with app teams | Server list, Vault/service-account access | Consumer map and access-path evidence | Unknown |
| WP05 | Hold application-owner meetings and record notes | Server group owner | Consumer map | Meeting notes, workload records, owner and validation contact | Unknown |
| WP06 | Submit required access/Vault/service-account requests | Authorized requester, TBD | WP04 gaps | Request IDs, approvals and access test evidence | Unknown |
| WP07 | Identify shared servers and review whether low-load consolidation is feasible | Migration/automation and SRE teams with application input | WP01/WP04 evidence | Grouping proposal, load evidence and decision log | Unknown |
| WP08 | Prepare AWS POC replication steps and test access when the POC is ready | Application test lead, TBD | WP04/WP06; central POC readiness | Reproducible test procedure and test evidence | Unknown |
| WP09 | Review discovery findings internally and update RAID/action trackers | Application coordinator, TBD | WP02-WP08 | Reviewed inventory, RAID and action status | Unknown |

## Contact and status follow-up

The S02 status table is historical and needs a fresh confirmation pass. Contact names/usernames should be verified before assignment. The visible statuses are retained in [SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md](SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md).

| Contact/status lead | Screenshot status | Follow-up |
| --- | --- | --- |
| `g.a.muruganantham` | Team does not work on AWS | Confirm out-of-scope disposition and whether any shared server remains |
| `radha.madugula` | Will upload to provided path | Confirm upload and record file/evidence location |
| `r.a.kanth` | Will update today | Request current update |
| `b.b.kumar.m` | Working on it; separately requested for details | Request current workbook and consumer details |
| `shaikh.shaikh.samad` | Yet to respond; separately named for follow-up | Send through approved project channel; record response or escalation |
| `anjini.devi.kolla` | On leave due family emergency | Do not treat as a blocker without checking backup/contact route |
| `aravind.v.aravind.v` | Will update today | Request current update |
| `sandeep.vurimella` | Working on it | Request workbook/status |
| `c...amamoorthy` | Needs more time; Excel lacks team hosts | Provide canonical host list/template and record revised date |
| `rajalaxmi.kumari` | Working on it | Request workbook/status |

## Definition of discovery complete

Discovery is complete for a server only when its authoritative identity is reconciled, every direct and Vault-mediated consumer has responded or been dispositioned, active and infrequent workloads are recorded, access and owner gaps are logged, application validation contacts are named, and an explicit retain/remediate/retire/defer decision exists. A spreadsheet upload alone is insufficient.

