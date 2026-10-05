# Detailed task plan

Proposed backlog — 6 October 2026. Karan confirms investigation and planning are underway, with a planned initiative start in mid-October 2026. The slide also reports assessment and small/large deployment strategy work. These are activity-level updates; status of each detailed task remains **Unknown** until mapped to evidence. Named execution owner, task effort range, exact start/finish dates and evidence link remain **TBD** for every row.

The slide states a nine-month estimate and 2026 lower-environment/readiness work followed by 2027 production/completion work. Proposed mapping: discovery, target selection, lower-environment build/remediation and validation in T01–T32 support the 2026 objectives; remaining production rehearsal/approval and T33–T44 support 2027 execution/closure. This is not a commitment that every readiness task will finish in 2026. Reconcile the implied approximately mid-July 2027 overall finish with the applicable lifecycle deadline before baselining a production-completion date.

Role codes: ML migration lead; PL platform lead; EL engineering lead; TL test lead; BO business owner; OL operations lead; SA security/access lead; CA change authority. The ownership document defines proposed responsibility boundaries.

Dependencies describe the completion needed to close a task; preparation can overlap. G0–G8 refer to the roadmap. Conditional tasks must receive an applicability decision rather than disappearing from the plan.

| ID | Phase | Task / deliverable | Accountable role | Depends on | Acceptance evidence |
|---|---|---|---|---|---|
| T01 | P0 | Agree scope, exclusions, and business success measures | ML | None | Reviewed scope and measurable success criteria |
| T02 | P0 | Assign role holders, delegates, availability, and escalation route | ML | T01 | Accepted ownership matrix and allocation record |
| T03 | P0 | Confirm Astronomer offering and contracted responsibility split | PL | T01 | Platform evidence and vendor-confirmed support boundary |
| T04 | P0 | Reconcile mid-October start, nine-month estimate, lifecycle deadline, blackouts, budget limits and current work evidence | ML | T01 | Production/closure milestone distinction, resolved calendar assumptions and evidence-backed status baseline; G0 review |
| T05 | P1 | Inventory environments, deployment IDs, versions, executor, network, and configuration | PL | T03 | Deployment register supported by dated exports |
| T06 | P1 | Reconcile repository DAGs, generated DAGs, deployed DAGs, and historical/paused entries | EL | T05 | Unique identifiers, discrepancy log, and signed scope denominator |
| T07 | P1 | Map business ownership, criticality, schedules, output deadlines, and recovery tolerances | BO | T06 | Workload owners accept profiles and requirements |
| T08 | P1 | Map cross-DAG and external dependencies, connections, packages, plugins, and custom code | EL | T05, T06 | Dependency graph and integration/package registers |
| T09 | P1 | Capture current behavior, workload volume, latency, failures, and business outputs | TL | T07, T08 | Reproducible baseline with observation period and known defects |
| T10 | P1 | Review completeness and approve the discovery baseline | ML | T05–T09 | Inventory discrepancies resolved or explicitly accepted; G1 |
| T11 | P2 | Validate the slide's 3.2.x direction; select exact source/intermediate/target versions and confirm support | PL | T10 | Version decision, package compatibility, official references, vendor confirmation |
| T12 | P2 | Assess code, scheduling, integrations, identity, and operational compatibility | EL | T11 | Findings tied to affected inventory items and remediation owners |
| T13 | P2 | Decide history retention, migration approach, and recovery feasibility | PL | T11, T12 | Decision D02; business recovery requirements and vendor evidence |
| T14 | P2 | Design target capacity, access, connectivity, monitoring, test isolation, and required Airflow Terraform/infrastructure changes | PL | T08, T13 | Reviewed design, secrets handling, infrastructure change scope, cost estimate and operational/security acceptance |
| T15 | P2 | Approve pilot manifest and test/acceptance criteria | TL | T07, T12–T14 | Pattern coverage, expected outputs, tolerances, recovery test; G2 |
| T16 | P3 | Prepare isolated lower-environment target, required Terraform/infrastructure changes and deployment pipeline | PL | T15 | Reviewed infrastructure plan, configuration manifest, connectivity/access checks, reproducible build |
| T17 | P3 | Implement inventory reconciliation and automated compatibility/test checks | TL | T15, T16 | Reports trace every tested item to commit and target image |
| T18 | P3 | Remediate pilot code and shared components | EL | T16, T17 | Reviewed changes and passing component checks |
| T19 | P3 | Execute pilot technical and business tests | TL | T18 | Results against baseline; reviewed discrepancies; business acceptance |
| T20 | P3 | Rehearse pilot cutover and recovery, including external effects | OL | T19 | Timed recovery evidence and reconciled data outcomes |
| T21 | P3 | Update estimates and production unit design from pilot learning | ML | T19, T20 | Effort ranges, capacity assumptions, revised risks; G3 |
| T22 | P4 | Fix common libraries, providers, build dependencies, and custom extensions | EL | T21 | Shared fixes tested against their full affected population |
| T23 | P4 | Remediate DAGs in dependency-aware development batches | EL | T22 | Reviewed changes, inventory coverage, no unexplained import failures |
| T24 | P4 | Update API callers, triggers, authentication, and external integrations | EL | T21 | Integration contract tests and named external owners |
| T25 | P4 | Prepare production configuration, Terraform/infrastructure changes and operational dashboards/runbooks | PL | T14, T21 | Reviewed infrastructure/configuration changes and recovery actions, alerts, access and support routes |
| T26 | P4 | Define production manifests, release artifacts, and scope-change controls | ML | T23–T25 | Traceable release contents and stable denominator; G4 |
| T27 | P5 | Execute full applicable automated coverage for release unit | TL | T26 | Build, parse, component and integration reports; all failures dispositioned |
| T28 | P5 | Validate schedules, dependencies, retries, reruns, and recovery behavior | TL | T27 | Interval comparisons and failure/recovery scenario results |
| T29 | P5 | Compare business outputs and obtain workload-owner acceptance | BO | T27, T28 | Approved tolerances and reconciled outputs, including infrequent cases |
| T30 | P5 | Validate capacity, access, observability, and operator procedures | OL | T27 | Load results, access checks, alert delivery, trained operator evidence |
| T31 | P5 | Rehearse release-unit cutover and rollback with exact candidate artifacts | OL | T28–T30 | Timed rehearsal, restored service/data consistency, closed defects |
| T32 | P5 | Review release readiness and approve gate evidence | TL | T29–T31 | Complete evidence index, thresholds, residual-risk acceptance; G5 |
| T33 | P6 | Approve change window, staffing, support coverage, and go/no-go record | CA | T32 | Signed production authorization and recovery decision authority |
| T34 | P6 | Freeze release and capture configuration, run state, and recovery assets | PL | T33 | Verified artifacts, manifests, backup/recovery evidence and final prechecks |
| T35 | P6 | Quiesce scheduling/ingress and reconcile in-flight work | OL | T34 | Drain/cancel decisions, external jobs reconciled, last-run ledger |
| T36 | P6 | Execute selected migration and controlled workload activation | PL | T35 | Timestamped actions, one active writer per interval, smoke-check results |
| T37 | P6 | Validate production outcomes and record proceed/recover decision | BO | T36 | Business deadlines, processing ledger, operations checks; G6 |
| T38 | P7 | Monitor agreed business cycles and reconcile outcomes | OL | T37 | Cycle evidence and trend report against approved thresholds |
| T39 | P7 | Resolve incidents and maintain rehearsed recovery readiness | OL | T38 | Closed incidents or accepted actions; current recovery assets |
| T40 | P7 | Approve exit from enhanced monitoring | OL | T38, T39 | Business and operational acceptance; G7 |
| T41 | P8 | Complete support training, runbooks, ownership and known-issue handover | OL | T40 | Receiving team accepts the operational pack |
| T42 | P8 | Approve history retention and retirement of obsolete resources | CA | T41 | Retention verified, recovery window closed, all consumers cleared |
| T43 | P8 | Retire approved resources and verify access, routing, and cost closure | PL | T42 | Retirement log and no remaining required dependencies |
| T44 | P8 | Close project and record lessons and accepted residual actions | ML | T43 | Scope reconciliation, evidence archive and accepted ownership; G8 |

## Companion strategy remediation tasks

These tasks implement the review of the Karan-authored post-migration strategy. They are proposed work items; status is Unknown until evidence is supplied. Use HC0–HC7 for the companion strategy's hypercare gates so they remain distinct from roadmap gates G0–G8.

| ID | Phase | Task / deliverable | Accountable role | Depends on | Acceptance evidence |
|---|---|---|---|---|---|
| T45 | P5 | Revise recovery flow and diagrams so containment may be immediate, but recovery authorization precedes recovery execution | OL | T31 | Approved flow: detect → assess → contain → authorize → execute → reconcile → close; failed validation loops back |
| T46 | P5 | Define active-task, external-job, retry, deferred-task and downstream-publication containment procedures | OL | T45, T24 | Workflow-specific drain/cancel/fence procedures tested or formally excepted |
| T47 | P5 | Add effective recovery execution identity: DAG code/commit, bundle version, Runtime image, providers and configuration | EL | T26, T45 | Recovery record captures intended and actual execution versions; exact-build behavior verified |
| T48 | P5 | Correct Airflow 3 architecture and monitoring diagram, including worker-to-Execution-API path | PL | T14, T45 | Diagram reviewed against the selected offering/executor; monitoring sources and topology paths are labelled |
| T49 | P5 | Separate business criticality from frequency and define controlled evidence for infrequent workflows at every criticality | BO | T07, T15 | Inventory fields and validation rules approved; no frequency-only downgrade |
| T50 | P5 | Split first-hour smoke checks from later continuity evidence and assign deadlines by workflow | TL | T15, T31 | Checklist identifies verify-now, initiate-now and close-by-milestone items |
| T51 | P5 | Define backfill, event replay and manual-trigger controls, including dry run, reprocessing behavior and independent concurrency | TL | T28, T46 | Recovery record includes applicability, candidate dates/events, concurrency and duplicate safeguards |
| T52 | P5 | Separate migration-team handover into hypercare entry and hypercare-to-steady-state acceptance | OL | T25, T45 | HC0/HC6 entry and exit packages define blockers, bounded exceptions, approvers and dates |
| T53 | P5 | Replace unapproved governance mandates with confirmed or proposed labels; verify ServiceNow/POD terminology and incident policy | ML | T02, T52 | Governance decision record and approved system-of-record/assignment model |
| T54 | P5 | Correct logical-date glossary and require workflow-specific mapping to business interval/partition/event | TL | T12, T28 | Glossary, test cases and per-DAG evidence use logical date, data interval and event semantics correctly |
| T55 | P7 | Create companion hypercare evidence dashboard with population reconciliation for all criticality bands and exceptions | OL | T49, T50, T52 | HC exit report separates passed, intentionally paused, exception, failed and untested items |
| T56 | P7 | Define matched-window metrics, due-time treatment, paused-workflow handling and rerun/duplicate treatment | TL | T49, T55 | Metric definitions, denominator and reporting window approved before HC reporting |
| T57 | P7 | Confirm separate-deployment versus in-place metadata/history acceptance criteria | PL | T13, T52 | Path-specific handover and history evidence; no implied metadata transfer where not supported |
| T58 | P7 | Align incident closure with service restoration, output reconciliation and problem-management requirements | OL | T53, T55 | Closure record supports separate incident, data-gap and root-cause references where policy requires |

Repeat T23–T40 where the chosen approach permits independent production units. For an existing-deployment upgrade, G4/G5 must cover the complete deployment before T33. Keep separate task instances such as `T29 / <release-unit-id>` rather than marking a master row complete after only one wave. T45–T58 should be completed before adopting the companion post-migration strategy as an operating procedure; T55–T58 remain active through hypercare.

## Tracking fields to populate

| Task instance | Named accountable owner | Responsible contributor | Status | Low / likely / high effort | Available capacity | Planned start / finish | Actual start / finish | Blocker / dependency | Evidence and approver |
|---|---|---|---|---|---|---|---|---|---|
| TEMPLATE — not a project task | TBD | TBD | Unknown | TBD | TBD | TBD | TBD | TBD | TBD |

Status vocabulary: Unknown, Not started, In progress, Blocked, In review, Accepted, Not applicable. Accepted requires deliverable evidence and approver/date. Not applicable requires an explicit rationale. Distinguish a task that is actively blocked from a planning dependency that has not yet been reached.

## Estimation method

Use pilot-observed effort by workload pattern rather than multiplying an unverified DAG count by a guessed duration. Estimate shared work once, then per-pattern adaptations, individual exceptions, test execution, defect rework, and business review. Record person-days separately from elapsed days. Confirm allocation before converting effort to calendar duration. Waiting for an infrequent run or vendor window can dominate elapsed time even when engineering effort is small.

No task-level numerical effort, exact delivery dates or completion percentages have been assigned. Keep the slide's overall estimate and user-confirmed approximate start distinct from task estimates and approved milestones. The companion strategy review adds work but does not establish additional elapsed time until the team estimates T45–T58.
