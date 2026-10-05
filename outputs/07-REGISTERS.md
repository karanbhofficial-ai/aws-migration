# Risks, decisions, and open questions

Draft — 6 October 2026. Risk scenarios below are proposals for assessment, not reports of incidents. Probability, quantified impact, named owners, and review/due dates are TBD. Role allocations are proposed. Decisions are open unless explicitly marked otherwise.

## Risk register

| ID | Risk / cause | Possible consequence | Proposed accountable role | Preventive action and evidence | Contingency / gate |
|---|---|---|---|---|---|
| R01 | Inventory omits generated, paused or rare workflows | Missing business processing | EL | Reconcile repository, deployment and history populations; owner review | Hold affected release; G1/G5 |
| R02 | Offering or supported version path is misunderstood | Upgrade or recovery is unavailable | PL | Written vendor confirmation for exact environment and versions | Replan strategy before G2 |
| R03 | Shared code/provider incompatibility has broad reach | Many workflows fail together | EL | Map affected population; pilot common components; regression evidence | Hold dependent units; G3/G4 |
| R04 | Scheduling or processing interval behavior differs | Wrong partitions or missed/duplicate runs | TL | Explicit interval comparisons and cutover ledger | Stop activation; reconcile/replay; G5/G6 |
| R05 | Two environments or retries produce external side effects | Duplicate writes, jobs or notifications | OL | Isolated tests, exclusive scheduling, idempotency/compensation proof | Fence writers and reconcile external jobs; G5/G6 |
| R06 | Green task states mask business-output differences | Incorrect or incomplete data | BO | Output contracts, matched inputs, business-rule comparisons | Hold acceptance and repair outputs; G5/G6 |
| R07 | Metadata/history or recovery assets are inadequate | Unrecoverable service state or missing records | PL | Retention decision and measured recovery rehearsal | Use approved recovery branch; hold G5 if infeasible |
| R08 | Access, secrets, API callers or networking are missed | Integration or operator access fails | SA | Integration/access inventory and contract tests | Restore reviewed configuration/routing; G5 |
| R09 | Peak load or backlog exceeds capacity | Deadlines missed or downstream overload | PL | Peak tests, capacity limits and controlled activation | Reduce activation; bounded backlog recovery; G5/G6 |
| R10 | Rare business cycles cannot be observed within the desired window | Acceptance lacks representative evidence | BO | Identify early; approve replay/simulation limitations | Adjust schedule or retain explicit deferral; G5/G7 |
| R11 | Business validators or shared staff are unavailable | Remediation or acceptance stalls | ML | Confirm allocations, delegates and review windows | Resequence units and revise forecast |
| R12 | Scope/configuration changes invalidate test results | Production differs from the tested candidate | ML | Baseline revisions, artifact traceability and impact review | Re-test affected scope; G5/G6 |
| R13 | Vendor work or environment lead time is unknown | Schedule cannot be met | PL | Confirm responsibility, lead time and booked support windows | Revise critical path before date commitment |
| R14 | Old resources are retired before retention/recovery needs end | Recovery or history access is lost | CA | Separate retirement approval and dependency checks | Delay retirement; G8 |
| R15 | Nine months from planned mid-October 2026 start implies roughly mid-July 2027, beyond the slide's April 2027 lifecycle claim | Production migration could miss the applicable maintenance/support deadline | ML | Confirm installed Runtime/contract deadline and separate production completion from later closure; reconcile estimate | Rephase scope/capacity or formally resolve support arrangements before schedule approval |

For each assessed risk add likelihood, consequence, exposure rating under the team's agreed method, trigger, mitigation owner, due date, evidence, residual risk, and accepting authority. Do not assign a numerical risk score without an agreed scale and supporting assessment.

## Decision log

| ID | Decision required | Options / considerations | Proposed decision owner | Needed by | Status |
|---|---|---|---|---|---|
| D01 | Exact source, intermediate and target versions | Slide states Airflow 3.2.x; validate Runtime/Python/providers, support and eligible path | PL | G2 | Target family stated in slide; exact technical decision open |
| D02 | Migration and recovery approach | Separate target vs existing-deployment upgrade; coupling, cost, history, recoverability | PL with CA acceptance | G2 | Open |
| D03 | Validation approach by workflow | Isolated replay, shadow comparison, simulation, real-cycle observation | TL with BO acceptance | G2; refine before G5 | Open |
| D04 | Critical workload placement | Existing target structure vs dedicated production environment; cost and operational value | PL with BO/OL input | G2 | Open; earlier discussion was a question |
| D05 | History and audit retention | What to retain, where, for how long, and how to retrieve it | CA with BO/OL input | G2 | Open |
| D06 | Criticality and acceptance/recovery thresholds | Business deadlines, tolerances, recovery limits and stop conditions | BO with OL input | Requirements at G1; final values before G5 | Open |
| D07 | Production unit boundaries and order | Dependency-connected groups or entire deployments; staff and cycle constraints | ML with PL/TL/BO input | G3 | Open |
| D08 | Production change and recovery authority | Named primary/delegate, trigger thresholds, decision deadline | CA | G5 | Open |
| D09 | Stability observation and retirement conditions | Business cycles, unresolved issues, history access, recovery expiry | OL with CA acceptance | G5 | Open |
| D10 | Retire/exclude workflows from migration scope | Business owner evidence and dependency review | ML with BO acceptance | G1; controlled updates thereafter | Open |
| D11 | Schedule baseline and applicable lifecycle deadline | User-confirmed mid-October start; slide's nine months and 2026/2027 split; distinguish production completion, closure, maintenance and support dates | ML with PL/CA input | Before schedule baseline | Open; overview approval status unknown |
| D12 | Small/large deployment classification and strategy | Define sizes using measured characteristics; evaluate approach by deployment, separately from business criticality | PL | G2/G3 | Slide reports strategy investigation; no choice evidenced |
| D13 | Companion hypercare gate names and handover boundaries | HC0–HC7; migration-team handover to hypercare versus hypercare-to-steady-state handover | OL | Before adopting post-migration strategy | Open |
| D14 | Effective recovery execution identity | Code/commit, DAG bundle version, Runtime image, providers and configuration recorded and verified | EL/PL | Before recovery rehearsal | Open |
| D15 | Incident system and ownership terminology | ServiceNow/POD/group terminology and closure policy confirmed or retained as proposal | ML/OL | G0 / before operating procedure | Open |
| D16 | Continuity evidence timing | Verify now, initiate now, close by milestone; first-hour checks are not universal workflow completion | TL/OL | Before cutover rehearsal | Open |

Record each decision with the actual options evaluated, evidence links, rationale, approver, approval date, conditions, affected tasks, and review triggers. Reopen a decision when its version, scope, support, or workload assumptions change.

## Focused questions and evidence requests

Information now available:

- Slide: Airflow 3.2.x target; SRE originating organization; Grace Chorey as Primary VP; Gaja Shenoy as initiative owner/requestor; nine-month estimate; 2026 readiness/lower-environment scope and 2027 production/completion scope.
- Karan: start planned for mid-October 2026, investigation and planning already underway, approval status unknown.

Next unresolved inputs, requested in small batches:

1. Exact Astronomer offering and installed Airflow/Runtime versions, so the applicable lifecycle and upgrade path can be established.
2. Required production-completion milestone and reconciliation of the nine-month estimate with the lifecycle deadline (D11).
3. Named execution owners, allocations and evidence of the current investigation/planning work; initiative titles do not fill every responsibility in the matrix.

Then obtain deployment/environment exports and repository references, workload/business-owner register and Astronomer's upgrade/recovery responsibilities. Resolve output deadlines, criticality, recovery tolerances, actual integrations, size categories and blackouts from those records. Databricks remains unconfirmed. Do not re-ask the answered start-month and approval-status questions unless new information changes them.

The PDF review adds a concrete evidence request: confirm the effective code/bundle/image/configuration identity used by a recovered run; confirm active-task and external-job containment; and define whether the organization's incident system, POD terminology and ServiceNow routing are approved project standards or proposed operating choices.

## Initial issues and assumptions

There are no verified execution incidents recorded. Missing exact versions, inventory, staffing and task-level evidence are planning gaps; do not present them as active project failures. Investigation/planning are user-confirmed as underway. The schedule/lifecycle mismatch is an unresolved planning risk, not evidence that a deadline has already been missed.

The plan assumes only that a reviewed migration will need discovery, compatibility work, validation, change control and handover. Every architecture-specific choice is conditional. The roadmap's roles, gates, categories and acceptance rules are proposed for review.

## Status update template

Record reporting date, baseline revision, accountable lead, current gate and its evidence, scope counts by distinct disposition, validation coverage, production acceptance, material changes since the prior report, active blockers, decisions needed, forecast range and confidence. Until evidence is supplied, use “Unknown,” not a guessed completion percentage or green/amber/red rating.
