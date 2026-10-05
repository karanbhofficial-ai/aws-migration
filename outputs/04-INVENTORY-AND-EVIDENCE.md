# Inventory and evidence templates

Draft — 6 October 2026. No live platform or repository inventory has been supplied or inspected. The tables below are schemas and empty templates, not populated migration records.

## Collection and reconciliation

Use approved platform exports/APIs, repository manifests, dependency files, existing monitoring, and owner review. Record extraction time, environment, version, source location, and collector. Store identifiers and secret references, never credential values, in the inventory.

Reconcile repository definitions against what each deployment loads and schedules. Include generated DAG IDs, paused workflows, infrequent workflows, externally triggered workflows, retired definitions, and old metadata-only entries. One Python file can generate several DAGs; file count is not DAG count. Investigate missing, duplicate, and unexpected entries.

Use `(environment, deployment_id, dag_id)` as the deployment-instance key. Maintain a separate logical workflow ID when the same workflow exists in several environments. Record renames and replacements explicitly. State which population each report counts. The transcript's approximate 1,500+ DAGs is a lead to investigate, not a verified denominator.

Each discovered item receives one disposition: migrate, retire with approval, exclude with reason, or unresolved. Reconcile the source population to these disjoint categories. At G1, unresolved scope discrepancies must be resolved or explicitly accepted with a bounded action. No unresolved scope items can silently disappear from final closure.

## Deployment register fields

| Field group | Required fields |
|---|---|
| Identity | Environment, organization/workspace, deployment ID, offering, region, owner, evidence timestamp; small/large classification with agreed definition and measured basis |
| Source | Airflow version, Runtime image/tag and digest where available, Python, executor, provider/package versions, repository and commit |
| Configuration | Scheduler/worker/triggerer settings, pools, queues, concurrency, environment/configuration references, plugins, custom images; Terraform repository/modules/state references and required Airflow infrastructure changes |
| Connectivity | Network boundaries, endpoints, identity bindings, secrets backend, service accounts, integration references |
| Operations | Monitoring/log destinations, access roles, service baselines, backup/recovery ownership, retention, current incidents |
| Target | Stated direction (slide: Airflow 3.2.x), separately approved exact version set, target deployment reference, configuration differences, strategy decision ID |

## DAG/workflow register fields

| Field group | Required fields |
|---|---|
| Identity and traceability | Instance key, logical workflow ID, repository/path, generator/factory, commit, deployed presence, source evidence |
| Ownership | Engineering owner, business validator, operations owner, escalation route |
| Business | Purpose, output consumers, criticality with rationale, deadline, allowed interruption, recovery time and data-loss tolerance |
| Scheduling | Schedule/timetable, time zone, catchup, start/end boundaries, manual/API/event triggers, paused state, rare business cycles |
| Dependencies | Upstream/downstream DAGs and external systems, sensors/events, shared libraries, cross-deployment dependencies |
| Implementation | Operators/providers, custom code, plugins, templates/context use, XCom use, callbacks, deferrable tasks, mapping, external jobs |
| Data effects | Input and output locations, partition keys, writes/notifications, idempotency key, retry behavior, compensation/replay procedure |
| Baseline | Run frequency, observed duration/queue delay, failure/retry pattern, peak concurrency, baseline interval and expected output evidence |
| Migration | Disposition, compatibility findings, remediation task IDs, release unit, target reference, status and evidence |
| Acceptance | Test cases, results, business tolerance, validator/sign-off, production boundary, handover evidence |

## Supporting registers

| Register | Row key | Fields to capture |
|---|---|---|
| Integration | Integration ID + environment | System owner; caller/callee; API/provider/package; endpoint; auth/secret reference; network; rate/concurrency limits; side effects; test isolation; evidence |
| Dependency edge | Producer + consumer + dependency type | Event/asset, sensor, file/table, API or trigger; ordering; partition/interval contract; boundary behavior; migration coupling; owner |
| Package/custom component | Component ID + version | Source; dependency constraints; affected DAGs; owner; compatibility finding; replacement/fix; regression evidence |
| Configuration difference | Setting + environment | Current and proposed nonsecret value/reference; reason; owner; validation; recovery action |
| Finding/defect | Finding ID | Affected inventory IDs; reproduction; severity/business impact; owner; task/commit; retest; accepted exception if any |
| Scope change | Change ID | Added/removed item; reason; approver/date; baseline revision; effect on evidence, effort and release unit |

## Reusable empty records

| Instance key | Workflow ID | Disposition | Engineering owner | Business owner | Criticality | Release unit | Status | Evidence |
|---|---|---|---|---|---|---|---|---|
| TEMPLATE | TBD | Unresolved | TBD | TBD | TBD | TBD | Unknown | TBD |

| Release unit ID | Approach / deployment | Included instances | Dependency boundary | Artifact / configuration | Acceptance owner | Recovery procedure | Planned window |
|---|---|---|---|---|---|---|---|
| TEMPLATE | TBD | TBD | TBD | TBD | TBD | TBD | TBD |

| Evidence ID | Requirement / task / inventory IDs | Environment + version | Commit / image / configuration | Inputs and intervals | Result / discrepancy | Evidence location | Reviewer / date |
|---|---|---|---|---|---|---|---|
| TEMPLATE | TBD | TBD | TBD | TBD | Not run | TBD | TBD |

## Evidence and reporting rules

Keep a chain from inventory item → compatibility finding → change → test result → business acceptance → production reconciliation → handover. Shared-component test evidence may cover several DAGs only when the affected population and coverage reasoning are explicit. Changed code, packages, configuration, or inputs require an impact review and relevant retests.

Publish counts with baseline revision, denominator, extraction date, and evidence links. Keep critical workloads and open blockers visible alongside aggregate counts. “Imported successfully,” “tested,” “business accepted,” and “running in production” are separate states. A blank evidence field is missing evidence, not a pass.
