# Testing and acceptance strategy

Proposed strategy — 6 October 2026. No test results have been supplied or tests executed as part of this planning work. Actual workload patterns, tolerances, observation periods, and validators remain TBD. Official compatibility checks are listed separately in the technical checks document.

The supplied slide states three objectives: migrate every in-scope deployment to Airflow 3.2.x; avoid material stability/performance degradation; and achieve a cutover with zero critical defects or unplanned business impact. These are slide-derived objectives, not achieved results. Define “material,” “critical,” the measurement window and the business-impact criteria before readiness approval. Include validation of required Terraform/infrastructure changes in environment, access, capacity and recovery checks. Lower-environment acceptance supports the stated 2026 deliverable; it does not substitute for production acceptance in 2027.

## What testing must establish

The target can load and execute the agreed workflows; processing windows and dependencies behave as intended; outputs meet business expectations; failures can be diagnosed and recovered; and the service can operate at required capacity. Successful task states alone do not prove correct outputs.

## Coverage model

Every in-scope DAG instance must be accounted for in inventory reconciliation and applicable automated checks. Business acceptance must cover every production workflow, using automated output comparisons where feasible and explicit owner review where necessary. Reuse test harnesses by pattern, but retain item-level evidence and exception visibility.

Select the pilot by observed features, integration types, complexity, side effects, and business impact. Include difficult patterns safely. A representative pilot establishes feasibility; it does not certify the rest of the population. For monthly, quarterly, annual, or event-only workflows, agree replay/simulation or observation of the real cycle. Record any limit of simulation and who accepts it.

Business criticality controls the required assurance level. Frequency is a separate attribute used to select the evidence method and observation window. An infrequent workflow can still be critical; use a controlled trigger, replay, simulation or approved exception without downgrading its business priority.

| Layer | Proposed checks | Required evidence | Proposed owner |
|---|---|---|---|
| Inventory and build | Reconcile expected IDs; resolve dependencies; build the exact candidate; scan applicable compatibility issues | Inventory diff, build/package manifest and scan findings | EL |
| Parse and structure | Parse all expected definitions; compare task IDs/dependencies and generated variants; investigate missing or changed structures | Per-item parse report and reviewed structural differences | EL |
| Components | Test changed custom operators, hooks, libraries, plugins, templates, callbacks and shared functions | Unit/component results, fixtures and affected population | EL |
| Scheduling and orchestration | Compare expected run windows, time zones, catchup, manual triggers, cross-DAG events/sensors, task ordering and concurrency | Expected versus observed interval/run ledger | TL |
| Integrations | Authenticate, authorize, connect, submit/poll jobs, retrieve secrets, read/write data, handle timeouts and callbacks | Contract results and external job/output IDs | EL |
| Business outcomes | Compare schemas, partitions, keys, row counts, aggregates, duplicates, completeness, freshness, and business rules as applicable | Input snapshot and comparison report accepted by BO | BO |
| Failure and recovery | Retry, timeout, interrupted task, rerun, backfill, partial write, lost callback, and recovery after migration/reversion | Failure injection results, replay/compensation proof | OL |
| Capacity | Replay representative peaks; measure queue delay, parsing, task duration, throughput, resource usage and downstream pressure | Measured baseline/target comparison and approved limits | PL |
| Security and operations | Verify user/service access, unauthorized-access rejection, secrets, logs, alerts, dashboards and escalation | Access tests, delivered alert evidence and operator walkthrough | SA / OL for their respective checks |
| Production acceptance | Verify controlled initial runs, deadlines, outputs and no missing/duplicate processing | Signed cutover ledger and business/operations decision | BO |

## Controlled comparison and shadow testing

Shadow testing is an option pending decision D03. Use equivalent input snapshots and processing intervals on both versions. Route test outputs to isolated destinations, suppress external notifications, and prevent duplicate job submissions or other production effects. If a write cannot be isolated, use a reviewed stub/replay approach and document what remains unproven. Do not execute two production writers for the same business interval.

Compare meaningful fields and business rules; explicitly handle timestamps, ordering, randomness, and other approved nondeterminism. Capture source data changes that could invalidate comparisons. A baseline defect is a known defect requiring a decision, not an automatic reason to reproduce the defect or silently fix it during migration.

## Scheduling and data-boundary scenarios

For each applicable workflow, cover normal scheduled execution, manual/API triggers, event-driven execution, missed intervals, delayed upstream data, retries, recovery reruns, and historical backfills. Include time-zone/DST boundaries if relevant. Validate the relationship among logical date, data interval, partition chosen, and externally submitted parameters. Compare explicit expectations against both systems rather than assuming equal DAG definitions imply equal processing windows.

At migration and recovery boundaries, identify the last accepted interval on the old system and first permitted interval on the target. Track externally running jobs even after the initiating task changes state. Determine whether partial outputs can be reused, removed, overwritten, or compensated before any replay. Record the effective code/commit, DAG bundle version where supported, Runtime image, provider set and relevant configuration for every recovery test. Confirm whether a rerun reuses an existing run or creates another and verify the code actually executed.

Containment testing must cover pause/unpause behavior, active task treatment, queued/retrying/deferred instances, external jobs, event/manual triggers, downstream publication and notification side effects. Pausing scheduled work is only one control; it does not prove that running tasks or external processes have stopped.

For backfill and replay, first classify the action as time-scheduled backfill, event replay or manual trigger. Record candidate logical dates/events, existing run states, reprocessing behavior, independent backfill concurrency, downstream capacity and duplicate safeguards. Preview the candidate range or event set and confirm the procedure is safe for the selected Airflow 3.2.x build.

## Thresholds to approve before G5

| Criterion | Proposed acceptance rule | Required decision |
|---|---|---|
| Completeness | Every release-unit item has applicable evidence and an accepted disposition | Agree baseline and release manifest |
| Compatibility | No unresolved load/build/compatibility blocker in the release unit | Agree severity and exception process |
| Correctness | Results satisfy workflow-specific business rules and tolerances | BO defines tolerances; no blanket numeric tolerance assumed |
| Processing continuity | No unexplained missing or duplicate business intervals/writes | BO and OL accept reconciliation rules |
| Performance | Deadlines, queueing and capacity remain within approved limits | PL/BO define values and peak scenarios |
| Recovery | Demonstrated recovery fits the approved time and data-loss allowances | BO/OL define limits; PL confirms supported method |
| Operational readiness | Alerts, access, runbooks, coverage and escalation demonstrated | OL/SA accept operational evidence |
| Defects | No unresolved issue that can breach agreed correctness or recovery requirements | CA accepts any bounded residual risk with BO/OL input |
| Stability | Required business cycles observed or approved alternative evidence supplied | BO/OL define period and cycle coverage |

## Evidence and defect handling

Every result records test ID, inventory IDs, candidate commit/image, configuration, inputs, processing interval, expected result, actual result, execution time, reviewer, and evidence location. Failures get an impact/severity assessment, owner, reproduction details, fix, and retest. Aggregate results must expose skipped and untested items.

Run broad automated checks for each release candidate and targeted behavioral regression for all affected workflows after shared changes. Reuse unchanged evidence only after a documented impact review. The test lead recommends readiness; business and operational owners accept their outcomes; the change authority authorizes production execution.

## Hypercare evidence timing

Use three timing classes for the post-cutover checklist: **verify now** for platform health, access, discovery, paused-state reconciliation, alert delivery and safe smoke checks; **initiate now** for continuity ledgers, long-running workflow observation and owner/deadline assignment; and **close by milestone** for the first approved run, business-output reconciliation and low-frequency/event-driven evidence. A one-hour check is a smoke-check window, not a universal proof that every critical workflow has completed.
