# Migration working registers

Updated 6 October 2026 with source S01 | Proposed working records, not evidence of assignment or delivery

Use with [MIGRATION-ROADMAP.md](MIGRATION-ROADMAP.md). Named owners, dates, estimates and status updates require confirmation. Keep the evidence source and verification date beside every material update.

## Program information from source S01

The [initiative photograph extraction](SOURCE-S01-INITIATIVE-OVERVIEW.md) records SRE as originating organization and Gaja Shenoy as initiative owner/requestor. It reports In Progress / Assessment and estimates 3 Months. Karan confirmed on 6 October 2026 that the estimate covers the full migration through hypercare. Slide approval and status dates remain unknown; this does not close delivery gates. Primary VP surname, detailed delivery ownership, calendar dates and 2026/2027 boundaries require confirmation. The Compliance KPI and success criteria are now mapped to proposed measures in the roadmap.

## Immediate action log

All actions below are proposed. Existing completion status is unknown. Each nominated role must accept ownership and provide a due date.

| ID | Action / concrete output | Proposed responsible role | Due date | Evidence required to close |
| --- | --- | --- | --- | --- |
| A01 | Confirm server/environment scope, exclusions, deadline and current completed/active/blocked work | Application coordinator with central migration lead | TBD | Scope list and dated status evidence |
| A02 | Name primary/backup owners, available allocation, business approvers and change decision authority | Application and migration leads | TBD | Accepted responsibility matrix |
| A03 | Confirm exact source RHEL releases, target Amazon Linux baseline, architecture and migration method | Central migration lead with source administrators | TBD | Source inventory and approved target/method record |
| A04 | Ask consuming teams to attest workloads, schedules, obsolete candidates and validation methods | Application discovery lead | TBD | Consumer-reviewed inventory |
| A05 | Confirm lnxprd0799 DB2 role/version/topology and authorized service operator | Application lead with SRE/DBA contact, to be identified | TBD | Architecture/configuration evidence and support assessment |
| A06 | Establish status of reporting access, SOP, AWS POC and Reporting COE UAT | Application coordinator with Reporting COE contact | TBD | Access confirmation, SOP and any existing test/approval evidence |
| A07 | Agree target-readiness deliverables, owners and dependency dates | Central migration lead with application team and SRE | TBD | Accepted infrastructure handoff checklist |
| A08 | Agree representative business scenarios, reconciliation tolerances and recovery limits | Workload and business owners | TBD | Approved test and recovery criteria |
| A09 | Coverage confirmed by Karan: full migration through hypercare. Confirm start/end dates, elapsed/remaining time and the 2026/2027 production boundary | Program planning contact, TBD | TBD | Approved schedule baseline; action remains open |
| A10 | Confirm slide version/approval/status date, leadership spelling and link program roles to delivery/acceptance roles | Application coordinator with program contact | TBD | Verified overview and accepted role assignments |
| A11 | Define Compliance requirement, workload denominator and measurable success thresholds | Program owner with business/control owner, assignments TBD | TBD | Approved measures, requirements and evidence owners |
| A12 | Reconcile S02 screenshot rows against authoritative Data SRE/ServiceNow server export | Discovery coordinator, TBD | TBD | Canonical server inventory with aliases and verification dates |
| A13 | Divide confirmed server groups among application-team members and record backups | Application migration coordinator, TBD | TBD | Accepted allocation matrix |
| A14 | Check direct and Vault-mediated consumers and record application meetings | Server-group owners, TBD | TBD | Consumer map, meeting notes and owner responses |
| A15 | Confirm Vault/service-account access and log approved request IDs | Authorized access requester, TBD | TBD | Access approvals and test evidence |
| A16 | Confirm AWS POC readiness and prepare repeatable application validation steps | Application test lead with central team | TBD | POC handoff and executed test evidence |
| A17 | Execute AWS-ACT-POD-001: meet each assigned POD lead, confirm direct/indirect/Vault consumers, workloads, dependencies, RHEL impact, validation scenarios and disposition | Karan / assigned server-group owners | TBD | Confirmed workload records, meeting notes, evidence links, owners and open actions |

## Initial server/workload case

Record ID: S001. This is a context-derived example; inclusion in the final migration scope remains to be confirmed.

| Field | Current entry | Evidence / next verification |
| --- | --- | --- |
| Server | lnxprd0799 | Project context, summarizing Reporting COE transcript |
| Environment | Unknown; do not infer solely from hostname | Confirm server inventory |
| Source OS/release and architecture | Unknown | Obtain source baseline |
| Target OS/image/repository/architecture | Unknown | Central team to confirm |
| Consuming group | Reporting COE discussed; complete consumer list unknown | Consumer discovery |
| Workload candidate W001 | Reporting flow with an indirect dependency involving DB2 services | Confirm exact service, executable, paths and schedule |
| Cognos location | Hosted separately, according to transcript summary | Confirm host/service and actual connection path |
| DB2 role/version/fix pack | Unknown | Determine server/client/gateway/other role before support assessment |
| Technical owner / operator / business approver | Names unknown | Confirm roles with application team, SRE/DBA and Reporting COE |
| Known operational behavior | Transcript described SRE checks or restarts of DB2 services when reporting failed | Obtain SOP and failure/recovery evidence |
| POC/UAT/access/SOP status | Discussed; completion unknown | A06 |
| Compatibility, wave and migration status | Unassessed; wave unassigned; status unknown | G04/G07 evidence required |

Candidate dependency D001: **Reporting/Cognos flow -> dependency involving DB2 services on lnxprd0799**. This is a conceptual dependency, not a verified network route. Intermediate components, endpoints, protocols, ports, credentials, database location and other consumers remain unknown. Add separate directed edges when the topology is confirmed.

## Risk log

These are proposed risks inferred from information gaps. Likelihood, severity, named owner and review dates are TBD. They are not confirmed incidents.

| ID | Risk and impact | Proposed treatment | Proposed role | Closure / acceptance evidence |
| --- | --- | --- | --- | --- |
| R01 | Undiscovered consumers or infrequent jobs may fail after cutover or retirement | Review schedules/history with every consuming team; require retirement clearance | Application discovery lead | Consumer attestation and workload coverage |
| R02 | Exact OS/product support is unknown; remediation or a different design may be needed | Complete version-specific official support assessment before wave approval | Application technical lead with central/product owners | Compatibility matrix and treatment decision |
| R03 | Shared DB2 dependency may affect multiple reporting consumers | Map callers, topology, startup/recovery order and wave coupling | DB2 service owner, TBD | Dependency review and end-to-end validation |
| R04 | Target access/connectivity or readiness delays may prevent testing | Agree central-team handoff criteria and track unmet dependencies separately | Central migration lead | Accepted G05 evidence |
| R05 | Missing business baselines or approvers may prevent reliable acceptance | Agree scenarios, outputs, tolerances and sign-off ownership before tests | Business validation owner, TBD | Approved test pack and results |
| R06 | Source/target writes or overlapping schedules may cause divergence or duplicates | Rehearse writer control, reconciliation and rollback data handling | Cutover coordinator with data/workload owners | Approved rehearsal and recovery evidence |
| R07 | Shared Airflow/AWS staffing may constrain delivery | Confirm allocations and conflicting windows while maintaining separate plans | Team leads | Accepted capacity and scheduling plan |
| R08 | Full migration through hypercare must fit the three-month estimate, but dates, capacity and 2026/2027 allocation are unresolved | Confirm calendar baseline and size the full sequence against actual scope and capacity; escalate forecast mismatch | Program planning contact, TBD | Accepted schedule and scope baseline |
| R09 | S02 screenshots may contain duplicates or conflicting account/host mappings | Reconcile with authoritative export before grouping or requesting migration | Discovery coordinator, TBD | Canonical inventory |
| R10 | Missing direct/Vault consumer information may cause post-migration failures | Require both access-path checks and consumer attestation | Server-group owners, TBD | Consumer map and validation evidence |
| R11 | POD responses may omit infrequent jobs, indirect consumers, hard-coded endpoints or shared mounts | Use the detailed POD-lead questionnaire and compare responses with approved inventory/discovery evidence | Karan / discovery coordinator, TBD | Lead confirmation plus reconciled dependency map |

## Decision log

Decisions remain open except for the user-confirmed coverage element of DEC08. That clarification does not establish approved dates or demonstrate feasibility.

| ID | Decision required | Needed before | Decision owner | Required input |
| --- | --- | --- | --- | --- |
| DEC01 | Final server/workload scope and exclusions | G01; refine with controlled changes after discovery | TBD | Inventory and consumer confirmation |
| DEC02 | Target Amazon Linux baseline/architecture and migration method | G04 and target handoff | TBD, central-team authority | Official support assessment and application requirements |
| DEC03 | DB2 role, support disposition and architecture treatment | G04 for affected workloads | TBD, product/platform authority | Exact versions/topology and vendor evidence |
| DEC04 | Retain, remediate, retire or defer each workload | Wave commitment | TBD, workload/business authority | Usage evidence, support disposition and business impact |
| DEC05 | Pilot/wave membership, order and change windows | G08 | TBD, migration/change authority | Dependency map, capacity, test results and recovery feasibility |
| DEC06 | Downtime, recovery limits, rollback thresholds and decision authority | G08 | TBD, business/change authority | Business tolerances and rehearsal evidence |
| DEC07 | Hypercare exit, source retention and retirement approval | G10/G11 | TBD, operations/business authority | Workload cycles, support acceptance and retention requirements |
| DEC08 | Partially resolved: Karan confirmed full migration through hypercare on 6 October 2026. Approved dates and 2026/2027 delivery split remain open | Dated roadmap commitment | Coverage clarified by Karan; formal schedule authority TBD | User reply; latest overview, scope, capacity and central-team milestones still required |
| DEC09 | Compliance requirement and success measurement definitions | Baseline reporting and acceptance planning | TBD, program/business/control authority | Requirement, scope denominator, criticality and disruption tolerances |
| DEC10 | Canonical server identity, grouping and treatment of possible temporary/low-load servers | P02/P03 and ServiceNow requests | TBD, Data SRE and migration authority | Reconciled export, load evidence and consumer clearance |
| DEC11 | Required discovery depth and approved programmatic tooling for server/application evidence | Before detailed assessment and POC access | Central migration/SRE and application authority | Approved tooling/access decision and data-handling boundaries |

For each resolved decision append: selected option, rationale, alternatives considered, approver, decision date, evidence link, affected workloads/waves and follow-up actions.

## Reusable record templates

Create records as discovery proceeds. Blank or TBD means unknown, not complete or not applicable. Record why a field is not applicable when that is confirmed.

### Workload and remediation record

| Field | Value |
| --- | --- |
| Workload ID / server IDs / consuming teams | TBD |
| Purpose / active-obsolete-unknown disposition / evidence | TBD |
| Technical owner / backup / business approver | TBD |
| Entry point / repository / deployed revision / paths | TBD |
| Schedule / timezone / startup mechanism / run account | TBD |
| Runtime / packages / native libraries / product versions | TBD |
| Data inputs/outputs / mounts / dependency IDs | TBD |
| Criticality / outage tolerance / recovery needs | TBD |
| Source baseline / target baseline / official compatibility evidence | TBD |
| Remediation ID / required change / owner / review / estimate basis | TBD |
| Test IDs / defects / retest evidence / approval | TBD |
| Wave / predecessor / status / blocker / due date | TBD |
| Evidence source / verified by / verification date | TBD |

### Validation evidence record

| Field | Value |
| --- | --- |
| Test ID / workload / dependency IDs / gate | TBD |
| Scenario / preconditions / steps / input data window | TBD |
| Source expected result / tolerance / approving business owner | TBD |
| Target environment / OS-image-repository / application revision | TBD |
| Execution date / tester / actual result / pass-fail-blocked | TBD |
| Logs/output/reconciliation evidence location | TBD |
| Defect ID / severity / remediation / retest evidence | TBD |
| Sign-off owner / decision / date / accepted residual risks | TBD |

### Wave and gate record

| Field | Value |
| --- | --- |
| Wave ID / servers / workloads / shared dependencies | TBD |
| Prerequisite gates and evidence links | TBD |
| Central readiness / application readiness / business availability | TBD |
| Named coordinator / operators / go-no-go authority / backups | TBD |
| Planned window / effort estimate / elapsed estimate / estimate basis | TBD |
| Cutover runbook / rehearsal evidence / rollback runbook | TBD |
| Recovery limits / latest rollback point / data reconciliation plan | TBD |
| Gate decision / approver / date / conditions | TBD |
| Production validation / hypercare criteria / handover acceptance | TBD |
| Retention decision / retirement approvals / central closure evidence | TBD |

## Maintenance rules

- Track delivery status separately from information quality. Suggested delivery states: Unknown, Not started, In progress, Blocked, Ready for review, Accepted. Use Not started only after confirmation.
- Label information as confirmed, transcript-derived, slide-derived, proposed or open; link its source and verification date. Keep source status dates separate from the dates evidence was received.
- Record defects as observed problems and risks as possible future problems. Link both to affected workloads and gates.
- Report completion only when acceptance evidence exists. Do not turn draft artifacts into a claim that migration work has completed.
- Keep the project context concise; link to these records rather than duplicating the evolving plan.
