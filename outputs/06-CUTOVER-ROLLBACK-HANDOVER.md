# Cutover, rollback, and operational handover

Draft procedure — 6 October 2026. This is a planning runbook, not an executable production command sheet. Exact deployment IDs, versions, commands, owners, windows, thresholds, and the vendor-supported recovery method must be filled in and rehearsed before G5. No infrastructure change is authorized by this document.

The initiative slide places production migration and legacy-runtime retirement in 2027. Exact windows remain unapproved. Resolve the lifecycle deadline and the nine-month schedule implication before selecting cutover dates. Include approved Airflow-related Terraform/infrastructure changes and their recovery procedures in the release manifest. Initiative-owner/VP titles in the slide do not by themselves name the cutover decision authority.

The companion post-migration strategy uses HC0–HC7 hypercare gates. Treat “migration-team handover to hypercare” and “hypercare handover to steady-state operations” as separate transitions. Monitoring begins at cutover even if nonessential paperwork is still being completed; essential ownership, recovery authority, access and alerting remain release blockers unless an authorized exception explicitly records owner, due date, workaround and monitoring.

## Release record required before execution

Record the release-unit ID, approved approach, source/target deployments, exact code/image/package/configuration versions, affected DAG instances and integrations, window/time zone, operator and backup, decision authority, vendor contact, evidence index, stop thresholds, recovery time allowance, data-loss allowance, and business validators.

Include protected configuration exports, vendor-confirmed metadata recovery evidence where applicable, history-retention requirements, artifact availability, and the last accepted processing interval for each workflow. Establish a recovery decision deadline from measured recovery time and the permitted outage; its value is TBD until rehearsal. Document any irreversible external effect and its compensation before the production decision.

## Cutover checklist

| Step | Action | Proposed responsible role | Hold point / evidence |
|---|---|---|---|
| C01 | Review G5 evidence, change authorization, support coverage and current incidents | ML, CA | Signed go/no-go record; no missing mandatory acceptance |
| C02 | Verify exact release artifacts, platform eligibility, configuration and recovery assets | PL | Artifact IDs, configuration diff, vendor evidence; repeat affected checks after any change |
| C03 | Freeze the release; capture run states, external job IDs, routing and processing boundaries | PL, OL | Timestamped pre-change manifest |
| C04 | Pause scheduled activation and control external/manual/event ingress for the unit | OL, integration owners | Confirm no uncontrolled new work; preserve events that need replay |
| C05 | Drain or explicitly disposition in-flight, queued, retrying and deferred work; reconcile remote jobs and partial writes | OL, EL, BO | Per-run disposition and a stable boundary; pausing alone is not a drain |
| C06 | Perform the rehearsed migration branch below | PL, AV where contracted | Record every action and actual time; hold if platform checks fail |
| C07 | Validate platform health, configuration, access, connectivity, expected DAG population, logs and alerts | PL, OL, TL | Smoke-check evidence before business writes resume |
| C08 | Activate the approved initial workload set; enforce one production writer for each interval | OL, EL | Routing and scheduler ownership recorded; no catchup/retry storm |
| C09 | Compare outputs, deadlines and expected run intervals; examine missing and duplicate processing | TL, BO | Business acceptance and ledger reconciliation |
| C10 | Record proceed, hold, or recover decision; start the agreed observation period only after acceptance | CA, OL | Decision and rationale; G6 when criteria pass |

### Branch A — separate target deployment

Prepare the target configuration and integrations before the window and keep production effects disabled until C08. At C06, apply the approved routing and activation changes while the old system remains fenced for the affected unit. Preserve the old deployment and its required access until recovery/retention conditions are satisfied. Do not assume old history appears on the target; fulfill the retention design in D05.

### Branch B — existing-deployment upgrade

Treat the affected deployment as one production change unit. At C06, use the exact vendor-approved upgrade process and monitor its completion. Capture the treatment of run state and metadata during rehearsal. Do not improvise database migration, cleanup, or downgrade commands in a managed environment. The technical checks document records the Astro-specific eligibility questions to resolve.

## Stop and recovery decisions

Proposed stop conditions include unexpected output corruption, uncontrolled duplicate processing, loss of essential access or connectivity, unexplained missing workflows, breach of a critical deadline, or insufficient time remaining to recover within the agreed outage. Fill in measurable performance/error limits and the decision deadline before approval.

The operator stops further activation when a stop condition is met. The named change authority decides recovery versus a bounded repair using the pre-agreed escalation route. Before production approval, establish an authorized fallback decision-maker and maximum decision delay if the primary is unavailable.

## Recovery checklist

1. Stop target scheduling, external ingress, retries and writers as required. Capture logs, run IDs, external job IDs and output partitions before further changes.
2. Classify each affected interval: no side effect, completed and accepted, partially committed, externally still running, or unknown. Inventory running, queued, retrying and deferred Airflow work and externally submitted jobs. Resolve unknowns and unsafe writers before replay.
3. The named recovery authority authorizes the selected action after technical and business assessment. Containment may be pre-authorized for immediate harm prevention; version recovery, replay and publication changes require the defined decision record.
4. Execute the rehearsed infrastructure branch. For a separate deployment, restore old routing and approved old artifacts/configuration. For an in-place upgrade, invoke only the recovery method confirmed for the exact offering and versions. Record metadata-loss and configuration-restoration implications identified in rehearsal.
5. Record the intended recovery code/commit, DAG bundle identifier/version where supported, Runtime image, provider set and configuration snapshot. Verify the actual code/version used by each recovered run; do not assume a redeploy changes an existing run's code.
6. Reconcile external effects separately from platform recovery. Deduplicate, compensate, or retain accepted outputs using the workflow's reviewed procedure. A platform rollback does not reverse an external write.
7. Prove source health and exclusive scheduling, then resume only approved intervals. Control backlogs and downstream load. Preserve accepted target outputs rather than blindly replaying everything.
8. Validate business correctness, service deadlines, access, logs and alerts. Record actual recovery time and observed loss/duplication against requirements.
9. Obtain business and operational acceptance; record the incident, data-gap and failed gate. A new migration attempt requires remediation and applicable retesting.

Code, configuration, metadata, identity/routing, and business data are separate recovery concerns. Each requires an owner, evidence, and a tested procedure. Use the official rollback caveats in the technical checks document when completing this runbook.

## Run reconciliation ledger

| Workflow / interval | Old run and external job IDs | State before switch | Output/commit evidence | Target run and external job IDs | Accepted writer | Replay/compensation action | Validator |
|---|---|---|---|---|---|---|---|
| TEMPLATE | TBD | TBD | TBD | TBD | TBD | TBD | TBD |

## Stabilization and handover

Enhanced monitoring lasts for the business cycles and duration agreed at G5; no fixed number of days is assumed. Review correctness, freshness, latency, queueing, retries, incidents and capacity. Continue to keep recovery assets usable until their agreed expiry. Progress to G7 only when required cycles are evidenced and any residual issue has explicit acceptance and ownership.

The receiving operations team must accept:

- Architecture, deployment/version/configuration manifest, workload and integration ownership, and support boundaries.
- Monitoring, delivered alerts, logs, dashboards, service objectives and escalation contacts.
- Procedures for retries, reruns, backfills, partial writes, dependency failures and supported platform recovery.
- Access and secret-reference ownership, routine change/deploy procedure, maintenance and upgrade responsibilities.
- Known issues, accepted exceptions, open actions, training/walkthrough evidence and retained test results.
- History access, audit evidence, retention dates, backup/recovery responsibilities and retirement conditions.

Use the following hypercare timing split:

- **Verify now:** platform components, access, discovery/parse state, paused-state reconciliation, alerts, logs, dashboards and safe smoke workflows.
- **Initiate now:** continuity ledgers, active/queued/deferred-work review, long-running workflow observation, external-job tracking and owner/deadline assignment.
- **Close by milestone:** first approved production run, output reconciliation, low-frequency/event-driven evidence and downstream acceptance.

The first-hour checklist must not require a completed run for every critical or infrequent workflow. It must establish the evidence owner, safe method and closure deadline.

Retirement requires a separate recorded authorization after operational acceptance and closure of the required recovery window. Verify all consumers and triggers have moved, retained evidence/history is accessible, and no required dependency remains. Remove only approved resources/access/routing, verify resulting cost closure, and record what was retained and why. For an in-place strategy, retirement may concern obsolete artifacts or settings rather than an old deployment.
