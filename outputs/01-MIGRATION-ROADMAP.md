# Airflow 2.x to 3.x migration roadmap

Draft v0.2 for review — 6 October 2026. Incorporates the user-provided initiative overview. Its approval status is unknown; this is not an approved schedule or a report of completed migration work.

## Outcome and scope

Move the agreed Airflow workloads toward the slide's stated Airflow 3.2.x target, preserve intended business results and delivery commitments, demonstrate recovery, and transfer the service to its operational owners. Confirm the exact supported version set before technical approval. Include Airflow-related Terraform and infrastructure changes described in the slide. Keep the RHEL-to-Amazon-Linux migration outside this plan. Track a shared staffing conflict only if it is confirmed.

The first milestone is an agreed scope, named owners, and a verified deployment and DAG inventory. Those inputs enable a defensible version choice, migration approach, estimate, and schedule.

## What we know

| Classification | Information | Planning treatment |
|---|---|---|
| Confirmed instruction | This project covers Airflow 2.x to 3.x; the AWS OS migration is separate. | Maintain a separate scope and backlog. |
| Prior user report recorded in PROJECT-CONTEXT.md | One overall team is divided between the two migrations; Shailesh reportedly confirmed their independence. | Do not assume technical coupling. Verify shared allocations. |
| Prior discussion, not verified against the platform | Airflow was described as fully managed by Astronomer. | Confirm offering, contract, and responsibility boundaries. |
| Transcript-derived, not verified | Approximately 1,500+ DAGs were mentioned. | Do not use this as the planning denominator. Reconcile actual inventory. |
| Open proposals from earlier discussions | Shadow testing and a dedicated production environment for critical DAGs. | Evaluate; neither is an approved design. |
| Open question | Databricks usage. | Include only if inventory confirms it. |
| Slide-derived | Airflow Upgrade - SRE; Marriott platform; SRE originating organization; Compliance KPI. | Use as initiative context pending confirmation of approval status. |
| Slide-derived | Airflow 3.2.x target; nine-month estimate; 2026 lower environments/readiness, 2027 production/completion. | Use as stated planning direction; exact versions, start and finish dates remain open. |
| Slide-derived | Primary VP Grace Chorey; initiative owner/requestor Gaja Shenoy. | Preserve these titles; execution accountabilities still need named assignments. |
| Slide-derived status | In Progress; Assessment; Strategy on small/large deployments. | Record reported status without asserting completed tasks or gates. |
| Slide-derived lifecycle claim | April 2027 End of Life. | Reconcile maintenance/support terminology against the actual Runtime and contract. |
| User-confirmed | Planned start in mid-October 2026; investigation and planning already underway; overview approval status unknown. | Use approximate start and activity status; exact day, task completion and schedule approval remain open. |
| Unknown | Offering, exact versions, environment inventory, execution owners, staffing, exact dates, budget amounts, and task-level progress. | Keep TBD; no readiness percentage is currently supportable. |

## Delivery periods stated in the initiative overview

| Period | Slide commitment | Roadmap mapping proposed for review |
|---|---|---|
| 2026 | Platform readiness and lower-environment upgrades across in-scope applications; application-team assessment/testing/remediation; Terraform/infrastructure changes; operational readiness and production preparation | P0–P4 and lower-environment validation/readiness work in P5. Verify current evidence before claiming a year-end milestone is achievable. |
| 2027 | Production upgrades and remaining workload migration; application-owner coordination; stability/performance validation; legacy-runtime retirement | Remaining P5 rehearsals/approvals as needed, then P6–P8. Exact production and retirement windows remain TBD. |

Karan confirmed a planned mid-October 2026 start, with investigation and planning already underway. If the slide's nine-month estimate runs from that start, the implied finish is approximately mid-July 2027. This is an inference, not an approved finish date, and extends beyond the slide's April 2027 lifecycle claim. Reconcile the applicable deadline and required production-completion milestone before baselining dates. Determine whether any remaining months are intended for stabilization/closure; that split is not yet established. The slide's April 2027 wording requires the check in the [technical source review](08-TECHNICAL-CHECKS-AND-SOURCES.md).

The slide defines success as all in-scope deployments migrated to 3.2.x, no material stability/performance degradation, and zero critical defects or unplanned business impact during cutover. Translate these objectives into measured baselines, agreed limits, severity definitions and sign-off evidence in P1/P5. Funding amounts are not visible; no budget has been inferred.

## Roadmap and approval gates

All phase-owner labels below are proposed execution roles with names TBD. Phase effort and exact dates remain TBD; the broad year split above is slide-derived. The task plan explains how to estimate them after discovery. A gate passes only with linked evidence and the accountable person's recorded acceptance.

| Phase | Work and deliverables | Proposed accountable role | Dependencies | Exit gate and evidence |
|---|---|---|---|---|
| P0 — Agree scope and responsibilities | Scope, success measures, role assignments, vendor responsibility agreement, constraints | Migration lead | None | G0: scope and roles accepted; unknowns have owners and follow-up dates |
| P1 — Establish the baseline | Deployment architecture, reconciled DAG register, dependencies, integrations, service baselines | Platform lead | G0; discovery can begin earlier | G1: every discovered item has a disposition; owners verify inventory and discrepancies are resolved |
| P2 — Choose target and approach | Exact version set, compatibility findings, target design, history requirements, migration and recovery decision | Platform lead | G1 | G2: target and approach approved; vendor confirms support; feasibility blockers resolved |
| P3 — Prove a representative pilot | Test environment, automated checks, pilot fixes, output comparisons, recovery rehearsal, measured effort | Test lead | G2 | G3: representative patterns pass, recovery is demonstrated, estimates updated from evidence |
| P4 — Prepare the complete release | Shared fixes, DAG remediation, integration changes, deployment pipeline, operations documentation | Engineering lead | G3 | G4: all workloads in the proposed release unit meet compatibility and build checks |
| P5 — Validate and rehearse | End-to-end and business validation, capacity checks, cutover rehearsal, operational readiness review | Test lead | G4 | G5: release unit has complete evidence, accepted results, agreed thresholds, and rehearsed recovery |
| P6 — Authorize and execute production change | Signed change record, run manifest, controlled switch, reconciliation, initial production acceptance | Change authority | G5 | G6: production outcomes meet agreed criteria and no unexplained missing or duplicate intervals remain |
| P7 — Stabilize the service | Enhanced monitoring, incident handling, reconciliation across agreed business cycles | Operations lead | G6 | G7: agreed observation cycles and thresholds satisfied; residual work has accepted owners |
| P8 — Handover and retire | Support acceptance, retained history and audit evidence, old service retirement, access and cost closure | Operations lead | G7; retirement approval | G8: operational ownership accepted and retirement verified without removing required recovery/history assets early |

P4–P7 can repeat by approved production release unit. For a new deployment this may be a dependency-connected group of DAGs. For an in-place upgrade, preparation can use DAG batches, but production readiness covers the entire affected deployment. Do not confuse a development batch with an independently releasable production unit.

## Migration approach decision

Evaluate a separate target environment first as a proposal: it may suit phased migration and isolated validation. Confirm cost, integration routing, retained history, and operational feasibility before choosing it. An existing-deployment upgrade remains an option. Platform eligibility must be established using the official guidance in the technical checks document; neither option is selected here.

| Decision dimension | Separate target environment | Existing-deployment upgrade |
|---|---|---|
| Proposed production unit | Dependency-connected workload group, if independently switchable | Whole affected deployment |
| History requirement | Define where old records will remain accessible | Validate required records through the upgrade rehearsal |
| Recovery proof needed | Restore routing and exclusive scheduling; reconcile external writes | Demonstrate vendor-supported recovery and reconcile external writes |
| Planning constraint | Temporary capacity, duplicated configuration, routing | Coordinated readiness and an agreed outage allowance |

## Wave design

First define workload criticality from business impact and recovery tolerance. Separately assess technical complexity, dependency coupling, data side effects, and testability. A critical workflow can be technically simple; a low-impact one can be technically complex.

The slide reports strategy work on small/large deployments. Define those categories using observed workload and capacity characteristics, then evaluate the migration approach for each deployment. Size, business criticality, and the choice of a dedicated critical-workload environment are separate decisions; the slide resolves none of them.

Use a representative pilot that covers actual patterns, including a difficult pattern in an isolated setting. Subsequent candidate groups are simple independent workflows, standard integrated workflows, and complex or critical dependency groups. These are planning categories, not committed wave counts or a fixed order. Place seasonal and infrequent workflows where their validation windows can be met. Keep producer/consumer dependencies together unless cross-environment behavior has been proven.

Each production unit needs an explicit manifest, owners, target configuration, input intervals, validation evidence, last-run/first-run boundary, rollback procedure, and acceptance record. Determine its size from pilot throughput, recovery time, test capacity, and business availability.

## How a schedule will be built

1. Confirm deployment inventory, scope, allocations, business blackouts, target date constraints, and support windows.
2. Size shared platform work separately from per-pattern and per-DAG work. Include reviews, testing, business sign-off, and rework.
3. Measure the pilot and use low/likely/high effort ranges for each remaining work category. Record assumptions and confidence.
4. Convert effort to elapsed time using confirmed available capacity. Include environment provisioning, vendor lead time, dependencies, and infrequent business cycles.
5. Baseline dates only after the critical path and recovery allowance are reviewed. Update the forecast when scope, staffing, versions, or observed throughput changes.

Likely dependency chain to validate: offering and version confirmation → inventory → strategy and recovery feasibility → pilot → remediation → business validation and rehearsal → change approval → production observation → retirement.

## Progress and acceptance

Report the baseline population alongside every metric. Show separately: inventoried, assessed, remediated, technically validated, business accepted, running on target, and handed over. Retired/excluded items require disposition evidence and are not counted as migrated. Show both unique workflows and deployment-specific instances when reporting totals.

Completion requires every in-scope item to have an accepted final disposition; all required production validations to pass; reconciliation of missing/duplicate processing; operational acceptance; and an approved retention/retirement outcome. Approved deferrals remain visible and do not become migration successes.

## First working session

Karan has confirmed the approximate start and that approval status is unknown. Next obtain the offering and exact source/target version set, resolve the production deadline versus the nine-month estimate, and collect task evidence, execution owners and allocations. Reuse the slide's 3.2.x direction and initiative titles. Collect platform exports and repository references to populate the inventory; derive business-threshold and wave questions from that evidence.

## Supporting documents

- [Detailed task plan](02-TASK-PLAN.md)
- [Proposed ownership matrix](03-OWNERSHIP.md)
- [Inventory and evidence templates](04-INVENTORY-AND-EVIDENCE.md)
- [Testing and acceptance strategy](05-TESTING-STRATEGY.md)
- [Cutover, rollback, and handover](06-CUTOVER-ROLLBACK-HANDOVER.md)
- [Risks, decisions, and questions](07-REGISTERS.md)
- [Official technical checks and sources](08-TECHNICAL-CHECKS-AND-SOURCES.md)
- [Review and remediation of Karan's post-migration strategy](09-POST-MIGRATION-STRATEGY-REVIEW.md)
