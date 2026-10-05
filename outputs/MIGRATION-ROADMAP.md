# RHEL to Amazon Linux on AWS: migration roadmap

Draft v0.2 | Updated 6 October 2026 with initiative overview photograph | For scope and planning review

This roadmap covers application readiness and validation through operational handover. Central migration/automation teams own infrastructure provisioning and server migration. Airflow version migration remains a separate project.

The supplied initiative slide reports **In Progress / Assessment**, estimates **3 months**, and lists program leadership. Karan confirmed on 6 October 2026 that the three-month estimate covers the **full migration through hypercare**. The slide's status date and approval status remain unknown. Individual phase completion, target release, calendar dates, application delivery owners and effort estimates remain unconfirmed. Proposed roles and gates below require agreement; they are not assignments or approvals.

## 1. Planning baseline

| Classification | What we know |
| --- | --- |
| Confirmed project direction | RHEL to Amazon Linux on AWS; maintain an end-to-end roadmap within the application-team scope. |
| Context-derived responsibility | Application team handles discovery, dependencies, application changes, testing and evidence. Central teams handle infrastructure and server migration. Detailed division with SRE and consumers needs confirmation. |
| Prior-message information | Karan reported Shailesh's confirmation that AWS and Airflow migrations are independent. Shared people may still constrain delivery. |
| Transcript-derived example | Cognos is hosted separately from `lnxprd0799`; its reporting flow has an indirect dependency involving DB2 services on that server. Exact topology is unconfirmed. |
| Discussed, completion unknown | Cognos access, SOP, DB2/connectivity assessment, AWS POC testing and Reporting COE UAT. |
| Slide-derived program context | Marriott initiative named RHEL to AWS migration - SRE; originating organization SRE; enterprise KPI Compliance. Gaja Shenoy is listed as initiative owner and requestor. Primary VP name needs spelling verification. |
| Slide-derived estimate/status | Estimated duration 3 Months; status In Progress / Assessment. Baseline date and approval are unknown. |
| User-confirmed estimate coverage | Karan confirmed on 6 October 2026: full migration through hypercare. Source retirement timing remains separate and unconfirmed. |
| Slide-derived targets | 100% of in-scope workloads migrated and validated; critical applications/services pass validation; business continuity and operational readiness. These are success criteria, not results. |
| S02 screenshot-derived discovery inputs | Candidate rows include RHEL 8 development/production servers, MDP/TCS context, possible SRW/Netezza/Oracle/Hotels Ops/Zook performance consumers, and a partial POD-lead response table. Treat as leads requiring reconciliation. |
| Open | Server scope, environments, OS releases beyond visible RHEL 8 rows, CPU architecture, product versions, migration method, delivery ownership, capacity, dated schedule and evidence of phase progress. |

Project evidence comes from [PROJECT-CONTEXT.md](../PROJECT-CONTEXT.md), which summarizes older messages and a transcript, and the user-supplied initiative photograph documented in [source S01](SOURCE-S01-INITIATIVE-OVERVIEW.md). Older attachments and technical evidence have not been revalidated. AWS and IBM documentation below informs assessment checks, not claims about this estate.

New S02 screenshots are extracted in [SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md](SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md), with a candidate server table in [SERVER-INVENTORY-DRAFT.md](SERVER-INVENTORY-DRAFT.md), discovery work packages in [DISCOVERY-ACTION-PLAN.md](DISCOVERY-ACTION-PLAN.md), and a seeded RAID register in [RAID-AND-STATUS-S02.md](RAID-AND-STATUS-S02.md). S02 supports the discovery approach and responsibility boundary; it does not establish current completion or canonical server identity.

The slide's five delivery stages map to this roadmap: Assess & Plan (P01-P04), Build & Remediate (P05-P06), Validate & Test (P06-P07), Migrate & Cutover (P08-P09), and Stabilize & Transition (P10). Source retirement (P11) is an additional proposed closure step. The slide's program-wide provisioning scope does not reassign central-team work to the application team.

## 2. Roadmap and approval gates

Run these phases per dependency group or wave after the overall scope is agreed. A gate passes only when its acceptance evidence is linked and its designated approver records a decision. Infrastructure readiness alone does not establish application readiness.

| Phase | Deliverable and work | Proposed lead / acceptance role | Prerequisites | Acceptance gate and evidence | Effort and elapsed time |
| --- | --- | --- | --- | --- | --- |
| P01 Scope and ownership | Scope baseline, exclusions, named responsibility matrix, environments, business priorities and decision authority | Application coordinator with central migration lead; sponsor accepts scope | Stakeholder input | G01: scope and responsibilities agreed; approval record linked | TBD after scope and availability are known |
| P02 Server and consumer discovery | Server list; every consuming pod/team; active and dormant workloads; access gaps; migration/retirement candidates | Application discovery lead with server and consumer contacts; consumer leads attest coverage | G01; authorized discovery access | G02: every scoped server has consumer review, including infrequent jobs; unresolved discovery gaps explicitly dispositioned | TBD from server count and discovery complexity |
| P03 Workloads, dependencies and source baseline | Workload inventory, directed dependency map, operating procedures, source configuration and representative business outputs | Workload owners with SRE and consumers; application lead reviews | P02 findings; representative execution history | G03: every retained workload has an owner, dependency record, baseline, criticality and validation method | TBD from workload count and observation cycles |
| P04 Compatibility and remediation design | Exact source/target matrix, official vendor support evidence, application change backlog, unsupported-component decisions | Application technical lead; central team confirms target; product specialists confirm support | Source versions and central team's proposed target | G04: every workload has a documented compatibility disposition and approved treatment for gaps; no unexplained support assumption | TBD after versions and product roles are established |
| P05 Target readiness handoff | Central team's target build and server migration approach; access, connectivity, storage, identity, observability and recovery evidence | Central migration/automation lead owns delivery; application team accepts test readiness with SRE | Agreed target and infrastructure requirements from P03/P04 | G05: required paths, identities, endpoints and recovery facilities are demonstrated; handoff record accepted | Central team to estimate; application acceptance effort TBD |
| P06 Application remediation | Versioned script/configuration/package changes, repeatable deployment instructions, peer review and component tests | Workload owners; application technical lead accepts changes | P04 treatment plan; G05 for integrated target tests | G06: approved changes deployed to test target; component checks pass; defects recorded and triaged | TBD from remediation backlog |
| P07 POC and business validation | End-to-end regression, reconciliation, performance and recovery evidence; consumer UAT | Application test lead; consuming business owner approves results; SRE validates recovery | G03 baseline; G05/G06 | G07: agreed critical scenarios pass, outputs reconcile within approved tolerances, blocking defects closed, residual risks explicitly accepted | TBD from scenarios, defect retests and business cycles |
| P08 Wave and cutover readiness | Dependency-aware wave list, change window, rehearsed cutover/rollback runbook, named operators, decision deadlines and communications | Migration coordinator with application, SRE and consumer leads; designated change authority approves | G07 for wave workloads; external dependency commitments | G08: approved go/no-go pack includes rehearsal evidence, rollback feasibility and business availability | TBD after wave size and rehearsal results |
| P09 Production cutover and validation | Central team's server migration; coordinated application actions; smoke checks, business reconciliation and incident decisions | Central team owns server actions; application team owns workload checks; named cutover authority decides | G08; live prerequisites rechecked | G09: agreed production checks pass and business owner accepts, or rollback is executed and verified | Approved window and recovery limits TBD |
| P10 Hypercare and handover | Monitoring review, scheduled-job evidence, defect follow-up, SOP/KT, support contacts and acceptance | Application team and SRE; receiving operations owner accepts | Successful G09 | G10: agreed observation cycles complete, operating team can support service, residual issues have accepted owners and dates | Duration TBD from workload cycles and service criticality |
| P11 Source retirement and closure | Consumer clearance, retention/restore evidence, asset and dependency updates; central team decommissions source | Central team owns execution; business, operations and designated retention authority approve as applicable | G10; agreed rollback/retention period expired | G11: source has no remaining required consumers, rollback release approved and central retirement evidence linked | Central team to estimate after retention decision |

Discovery, baseline capture and compatibility assessment can overlap as reliable workload records arrive. Infrastructure preparation and application changes can proceed in parallel once requirements and the target are agreed. Integrated testing requires target readiness. These are sequencing proposals, not a dated schedule.

## 3. Responsibility agreement

Replace each role with a named primary and backup. Confirm one accountable approver for each gate and each wave. Do not assume Karan is the formal approver.

S01 lists Gaja Shenoy as initiative owner and requestor and SRE as originating organization. Record these program roles separately from delivery assignments. The photograph does not establish that the initiative owner is the cutover authority, business UAT approver or application coordinator.

| Work area | Proposed delivery responsibility | Required acceptance or coordination |
| --- | --- | --- |
| Scope, workload inventory and dependencies | Application team, with each consuming pod/team | Application coordinator; consumers attest their workloads |
| AWS provisioning, OS build and server migration | Central migration/automation teams | Central infrastructure acceptance; application test-readiness handoff |
| Application scripts, runtime requirements and configuration | Application workload owners | Application technical lead; central team installs/manages OS components as agreed |
| DB2 services and database recovery | Ownership unresolved: identify SRE/DBA/product owner | Confirm operator, support authority and recovery responsibility before testing |
| Business test cases and UAT | Consuming teams with application testers | Named business sign-off owner |
| Network, storage, identity, monitoring and backup | Central/platform teams and SRE, exact split TBD | Application team supplies requirements and verifies its paths |
| Cutover and rollback decisions | Named migration/change authority, TBD | Application and business input; central and SRE operators execute their steps |
| Production support and decommissioning | Receiving operations team; central team retires servers | Business clearance, support acceptance and rollback-release approval |

## 4. Discovery and dependency model

Track **Server -> consuming team -> workload -> dependencies -> remediation -> test/evidence -> approval**. Use stable IDs so one shared dependency can link to several workloads.

- Server record: hostname, environment, source OS/release, architecture, location, target OS/image/repository version, central migration contact, proposed wave, evidence source and last verification date.
- Workload record: consuming pod/team, purpose, technical and business owners, active/obsolete/unknown disposition, repository/path, entry point, service or schedule, timezone, run account, runtime/packages, configuration, input/output locations, criticality and recovery needs.
- Dependency edge: calling workload, destination service or workload, direction, endpoint/port/protocol, authentication reference, mount/data dependency, schedule/order, owning team, shared consumers and failure impact. Record references to credentials, not secret values.
- Validation link: baseline output, business scenario, expected result/tolerance, target build, tester, evidence, defect, retest and approver.

Include monthly, quarterly and ad hoc workloads. Absence of a running process is not proof that a workload is obsolete. Retirement requires consumer confirmation and a recorded decision.

## 5. Compatibility assessment

The target Amazon Linux release is not yet selected in this project. These checks are conditional and must be repeated against the exact source and proposed target. AWS documentation recommends AL2023 for migration from another Linux distribution; this does not prove that any particular product is supported. [AWS Amazon Linux guidance](https://docs.aws.amazon.com/linux/al2/ug/)

| Area | Required assessment and evidence |
| --- | --- |
| Target baseline | Central team records exact OS release, AMI/build, repository version, architecture and update policy. If AL2023 is selected, test and deploy a specific release version; AWS cautions against using `latest` for production updates. [AWS update guidance](https://docs.aws.amazon.com/linux/al2023/ug/updating.html) |
| Product support | For each database, driver, agent and commercial product, capture edition/component/version/fix pack, target OS/architecture and official support evidence. IBM directs Db2 users to its system requirements reports. Db2 compatibility here is **unassessed** until its exact role and version are established. [IBM Db2 requirements](https://www.ibm.com/support/pages/system-requirements-ibm-db2-linux-unix-and-windows) |
| Packages and runtimes | Inventory installed and actually used packages, interpreter paths, native libraries and build dependencies. Verify target availability and product compatibility; do not infer support from RHEL compatibility alone. |
| Scheduling and services | Inventory cron, timers, boot scripts, service units, run accounts, timezone, environment variables, restart behavior and logging. AL2023 does not install cron by default; agree and test how each required schedule will run. The AWS comparison is against AL2, not a complete RHEL migration guide. [AWS preparation guidance](https://docs.aws.amazon.com/linux/al2/ug/prepare-for-al2023.html) |
| Paths, identity and security | Test hard-coded hostnames and paths, file ownership, permissions, mounts, authentication, certificates, TLS connections and required integrations against the actual target configuration. |
| Support lifecycle | Capture OS and package support horizons for the selected baseline. AWS documents separate support treatment for core and non-core AL2023 packages, so OS support alone is insufficient evidence for every dependency. [AWS lifecycle guidance](https://docs.aws.amazon.com/linux/al2023/ug/release-cadence.html) |

Assessment outcomes: **unassessed**, **supported with evidence**, **change required**, **unsupported**, or **exception pending/approved**. A successful POC proves tested behavior; it does not replace vendor support evidence. An unsupported component needs an explicit treatment decision before a wave is approved.

## 6. Validation and production readiness

Agree the business scenarios and tolerances before execution. For each critical workload, collect source and target evidence for connectivity/authentication, outputs/data reconciliation, schedule execution, restart/recovery and representative runtime/throughput. Add failure and retry cases where duplicate or missed processing can affect the business.

Each evidence record must identify workload, test case, environment/build, application revision, data/time window, expected and actual results, tester/date, evidence location, defect/retest links and approval. A service showing as running is only one technical check.

For `lnxprd0799`, first confirm what DB2 component runs there, its version, its callers and downstream connections. Obtain the SOP and reporting access; agree representative reports and source baselines with Reporting COE. Then validate the full reporting path on the approved target, including a controlled recovery test with the authorized operator. No restart or migration is authorized by this planning document.

## 7. Wave, cutover and rollback design

Proposed wave approach: begin with a representative workload whose dependencies are understood and whose recovery is practical. Group shared dependencies deliberately; use rehearsal findings to size later waves. A shared DB2 dependency must be assessed before separating its consumers across waves. `lnxprd0799` is a discovery example, not an approved pilot.

Every wave runbook needs these ordered steps, each with a named operator, predecessor, expected duration, success check, evidence link and reversal action:

1. Confirm scope, approvers, support availability, target readiness, backups/restore evidence and change approval.
2. Confirm source baseline, freeze application changes as agreed, and stop or drain jobs/writers where needed. Prevent simultaneous processing on source and target.
3. Have the responsible central/data team perform the agreed transfer, synchronization and routing actions. Record the data checkpoint and any write freeze.
4. Apply application configuration, start dependencies in the agreed order, then enable consumers and schedules deliberately.
5. Run technical checks and business reconciliation. Compare actual results with the pre-approved thresholds.
6. Record the continue/rollback decision before the agreed latest safe rollback point, then verify whichever outcome is executed.

Before G08, agree measurable rollback triggers: failed critical business checks, unreconciled data beyond tolerance, unresolved service failure, or a time limit that leaves insufficient time to recover. Thresholds, outage allowance, recovery time and acceptable data loss remain TBD.

Rollback must explain who stops target writes, how post-cutover data is preserved/reconciled, how source consistency is restored, who reverses endpoint changes, how duplicate processing is avoided and who validates recovery. If reversal becomes unsafe after a particular operation, identify that point and approve a recovery/forward-fix plan before cutover. Keeping the old server is not, by itself, a tested rollback plan.

## 8. Hypercare and handover

Set the observation period around actual workload cycles; agree how infrequent jobs will be covered. Handover includes service/dependency map, deployment and restart SOPs, access references, monitoring and alert ownership, restore/recovery instructions, support escalation, known defects and evidence links. Operations must explicitly accept the service before G10 closes.

Retire the source only after all consumers are cleared, the rollback and retention decisions allow it, and the responsible teams approve. Central teams execute decommissioning and provide closure evidence.

## 9. Scheduling and reporting

S01 provides a **three-month program estimate**. Karan confirmed that it covers the **full migration through hypercare**, corresponding to P01-P10 in this roadmap. This is the planning horizon, not three additional months starting from receipt of the photograph. The start date, elapsed time, remaining time and calendar deadline are unknown. P11 retirement timing depends on separate retention and approval decisions.

The slide's delivery section is headed **2026: Platform Readiness & Lower Environment Upgrades**, but also lists production cutover and stabilization; no separate 2027 deliverables are visible. Do not assign phases to calendar dates or years until the baseline date and year boundary are clarified. Fit the detailed plan to the full three-month horizon only after checking scope, capacity, readiness and validation cycles; escalate a forecast mismatch explicitly.

Build a dated plan after P01/P02 establish scope and team allocation. Estimate application effort by workload, central-team readiness separately, and elapsed time for access, vendor responses, UAT and business cycles. Use rehearsal throughput to revise later wave estimates. Record estimate author/date, basis, confidence and dependencies. Phase estimates remain TBD; the slide estimate has not been validated against workload scope or capacity.

### Proposed measures aligned to the slide

| Slide target | Proposed measurable acceptance | Evidence / open definition |
| --- | --- | --- |
| 100% migration completion | Migrated workloads with accepted validation divided by the approved in-scope workload population | Count workloads, not just servers. Establish the denominator and track every approved scope change. Report retirements/deferrals separately; they are not migrated workloads. Current counts unknown. |
| Application compatibility | Each critical application/platform service has accepted functional, integration, regression and production results | Agree criticality and required scenarios; link test evidence and business approvals at G07/G09. |
| Business continuity | Cutover meets agreed outage and data-reconciliation tolerances, with demonstrated rollback readiness and stable post-cutover operation | Define material disruption and observation period before G08; retain actual cutover/hypercare evidence. |
| Operational readiness | Receiving operations owner accepts monitoring, support procedures, documentation and named ownership | G10 handover evidence and acceptance. |
| Compliance KPI | Trace the applicable requirement to migration scope and acceptance evidence | Requirement, deadline and compliance acceptance owner are still unknown; the KPI label alone is not a control definition. |

Proposed coordination: a regular application/central/SRE/consumer review during discovery and remediation, with a cadence agreed by the leads; a dedicated cutover bridge during approved changes. Report scope coverage, evidence-backed gate completion, open blockers, decisions required and next accepted milestone. Keep unknown progress visible rather than treating it as zero or complete.

Immediate actions and working record templates are in [MIGRATION-REGISTERS.md](MIGRATION-REGISTERS.md). The first planning priorities are scope and current status, named ownership, exact OS/product baselines, and central-team migration approach/readiness.
