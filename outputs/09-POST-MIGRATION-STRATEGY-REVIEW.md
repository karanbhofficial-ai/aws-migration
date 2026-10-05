# Review of Karan's post-migration strategy

## Action status

The findings have been converted into proposed project tasks T45–T58, testing controls, cutover/recovery controls and decisions D13–D16 in the planning pack. This addresses the review at roadmap level while preserving the source PDF. The PDF should be revised only when an editable source or an explicit document-revision workflow is available and the proposed rules have been approved.

Reviewed 6 October 2026. Source: `Airflow_2x_to_3_2x_Post_Migration_Strategy_document.pdf`, 21 pages, prepared 5 October 2026. Karan explicitly confirmed that he created it; it was not supplied by the business or client. Treat its operating model, tools, roles and rules as proposals unless separately evidenced. The source PDF has not been edited or re-exported.

## Assessment

This is a useful basis for the post-cutover validation, stabilization, recovery and operational-handover part of the migration roadmap. Its strongest features are the separate proofs of platform health, workflow correctness and business-output correctness; protection of intentionally paused DAGs; reconciliation of partial/duplicate outputs; and conditional, vendor-confirmed version recovery.

It deliberately excludes pre-migration assessment and upgrade execution. That is appropriate for its stated scope; it should be a supporting strategy linked to the end-to-end roadmap, not judged as if it were the entire migration plan.

The draft needs several operational corrections before adoption. Unfilled thresholds and version choices are already acknowledged in Section 12; those are decisions to complete, not evidence that the whole strategy is flawed. Findings below separate technical issues, internal inconsistencies and unconfirmed governance assumptions. No live platform or referenced inventory workbook was inspected.

## Changes needed before operational use

### F01 — Pausing is insufficient containment

**Location:** Section 8, p.13; Section 9, p.14; Figure 3.

The containment instructions focus on pausing the DAG or publication path, but do not require confirmation that active tasks and externally submitted jobs can no longer produce harmful writes. Airflow permits running tasks to finish after a DAG is paused. The document does collect side-effect evidence; the missing step is an explicit stop/drain/contain decision for those still-active processes. [Airflow 3.2 DAG pausing](https://airflow.apache.org/docs/apache-airflow/3.2.0/core-concepts/dags.html#dag-pausing-deactivation-and-deletion)

**Suggested wording:** “Pause future scheduled work and control external/manual triggers. Inventory running, queued, retrying and deferred tasks and externally submitted jobs. Using the approved workflow-specific procedure, drain or cancel affected work and block unsafe publication where needed. Verify that uncontrolled writes have stopped before recovery or replay.”

Do not assume cancellation of an Airflow task proves cancellation of an external job. The exact actions require the installed executor/provider and integration runbooks.

### F02 — The diagrams put recovery before its decision gate

**Location:** Figure 1, p.3; Figure 3, p.14.

Figure 1 moves from “Triage and recover” to “Apply recovery gate.” Figure 3 shows a direct Recover → Reconcile path, with the recovery gate drawn below Recover rather than as a required predecessor. Section 8's text is more careful, but an operator following the figures can bypass the decision.

**Suggested change:** show Detect → Assess → Contain → Recovery decision/authorization → Execute selected action → Reconcile → Close. Keep an explicit return path for failed validation. Containment can occur immediately under pre-authorized incident procedures; it need not wait for a version-recovery decision. Show triage/recovery as a loop available throughout hypercare, not a phase that waits until stabilization ends.

### F03 — Recovery does not identify the code that the recovered run will execute

**Location:** Section 8, p.13; Section 9, pp.14–15; Appendix B2, p.20.

Retaining DAG/shared-library versions is useful, but does not establish the effective execution version after a fix or revert. Versioned bundles can keep a run on its original code; nonversioned bundles behave differently. Confirm bundle behavior before relying on a redeploy to change a cleared task. [Airflow 3.2 DAG bundles](https://airflow.apache.org/docs/apache-airflow/3.2.0/administration-and-deployment/dag-bundles.html)

**Suggested addition:** record source and intended recovery code/commit, bundle identifier/version where supported, Runtime image, provider set and configuration snapshot. State whether recovery reuses an existing run or creates another, and verify the actual code used. Airflow documents a latest-bundle clearing option as experimental; do not assume availability or approved use without testing the selected build. [Airflow 3.2 rerunning tasks](https://airflow.apache.org/docs/apache-airflow/3.2.0/core-concepts/dag-run.html#re-run-tasks)

For Astro, deploy rollback also does not restore all deployment settings or environment values; map code/image recovery and configuration restoration separately. [Astro rollback scope](https://www.astronomer.io/docs/astro/deploy-history#what-happens-during-a-deploy-rollback)

### F04 — Figure 2 omits a central execution dependency

**Location:** Figure 2, p.8.

The API Server is labelled only UI + REST API, with no worker-to-API execution path. The worker/Triggerer arrow and the single scheduler-to-logs path also have no legend distinguishing coordination from monitoring. This can misdirect dependency checks and triage. In Airflow 3, workers interact with the API server for task execution and metadata operations. [Airflow 3.2 upgrade architecture](https://airflow.apache.org/docs/apache-airflow/3.2.0/installation/upgrading_to_airflow3.html#understanding-airflow-3-x-architecture-changes)

**Suggested change:** label the task Execution API, show the worker/Task SDK connection to it, and identify the metadata and scheduling paths using the verified deployment architecture. Draw monitoring inputs from every applicable component, or explicitly label the diagram as a monitoring checklist without topology semantics. Separate installed provider/plugin packages from DAG-bundle contents; they are not interchangeable deployment artifacts. Keep the existing topology-confirmation note.

### F05 — Low frequency is incorrectly offered as a low-priority classification

**Location:** Section 3, p.6, validation-priority table.

The Low row includes ad hoc or infrequent DAGs. An annual regulatory workflow or an emergency recovery DAG can be critical despite rarely running. The introductory paragraph correctly mentions several dimensions, but the table can override that intention in practice.

**Suggested wording:** “Criticality is determined by business impact. Frequency, dependency complexity and change exposure are separate fields used to choose validation method and evidence.” Reserve Low for workflows assessed as low business impact. Retain the controlled-validation approach for infrequent workflows at every criticality.

### F06 — The first-hour checklist demands evidence that may not exist yet

**Location:** Section 11, p.16; Appendix A1, p.18.

A1 requires continuity through the first successful target run for every critical/high DAG. A multi-hour job, weekly schedule or event-dependent workflow cannot necessarily provide that evidence within 60 minutes. Forcing a run to complete the checklist can also conflict with paused-state and safe-trigger rules.

**Suggested change:** first-hour checks establish platform health, intended scheduling/paused state, safe smoke-test results, the continuity ledger and owners/deadlines for pending evidence. Complete each workflow's continuity proof when its approved run/evidence method finishes. Split checklist items into “verify now,” “initiate now,” and “close by agreed validation milestone.” The 60-minute period itself remains a proposal pending rehearsal.

### F07 — Backfill needs an explicit applicability and concurrency check

**Location:** Section 9, p.15, “Expected run(s) missing.”

The generic row prescribes backfill. The separate asset/event row is helpful, but the generic instruction should explicitly apply to time-scheduled DAGs. Airflow backfill follows a time-based schedule, and its maximum active runs is configured independently of the DAG's own limit. [Airflow 3.2 backfill](https://airflow.apache.org/docs/apache-airflow/3.2.0/core-concepts/backfill.html)

**Suggested change:** distinguish scheduled-interval backfill from approved event replay/manual triggering. Record the candidate dates, existing run states, reprocessing policy, backfill concurrency and total downstream capacity. Preview the selected date range; do not rely only on the DAG's normal concurrency setting. Retain the existing dependency-order and duplicate checks.

### F08 — Handover and entry exceptions need a consistent boundary

**Location:** document control, p.1; scope/entry gate, p.4; entry criteria, p.9; execution sequence, pp.16–17.

The scope says it begins after cutover and formal handover, but Phase 1 performs handover acceptance before cutover sign-off and a later phase transfers operations. These may be different handovers, but that distinction is not explicit. Page 4 also allows handover exceptions broadly, while p.9 makes recovery options and critical/high ownership prerequisites.

**Suggested change:** name “migration-team handover to hypercare” separately from “hypercare handover to steady-state operations.” Review required packages before production activation; begin heightened support immediately at cutover. Do not withhold monitoring because paperwork is incomplete. Specify which missing controls block release and which can be accepted with bounded exceptions, by whom and until when. Missing essential recovery authority or critical-workflow ownership must not be silently waived through the generic exception route.

### F09 — Proposed governance sometimes reads as an approved client rule

**Location:** document control, p.1; non-negotiable rules, p.4; incident system of record, p.11; source register, p.21.

The document labels itself Final for internal review, names ServiceNow as the incident system of record, and mandates a POD/ServiceNow group for each DAG. These may be good proposals, but the user confirmed this is his own draft. The existing shared-responsibility caveat and evidence-quality note are helpful; apply the same qualification throughout.

**Suggested wording:** “Author: Karan. Status: Proposed post-migration strategy for internal review; business/client approval pending.” Mark ServiceNow, POD terminology, assignment-group rules and decision roles as proposed until a source confirms them. Keep one accountable workflow owner while allowing specialist resolver teams and linked platform incidents.

Appendix D should distinguish prior authoring inputs from approved project records and official technical references. E4 mentions an inventory workbook that was not supplied for this review; no findings about its actual completeness or approved routing can be made. Replace generic A1/A2 entries with exact links, documentation versions, retrieval dates and the claims they support. The selected Astro offering determines whether vendor guidance governs platform recovery; it is not merely optional background.

### F10 — Logical date is not an automatic business-period definition

**Location:** Appendix C, p.20; related recovery/evidence fields.

The glossary says logical date drives date-templated queries and partitions. It can be used that way by a workflow, but that is not its guaranteed business meaning. The template reference describes it as identification and points to data-interval boundaries for time-range semantics. [Airflow 3.2 templates reference](https://airflow.apache.org/docs/apache-airflow/3.2.0/templates-ref.html)

**Suggested wording:** “Logical date: a run-associated logical timestamp where applicable; its relationship to the business period must follow the workflow contract. Data interval: Airflow's interval boundaries where applicable; validate the mapping to business partitions. For event/manual cases record the event or approved input range explicitly.” The main document already distinguishes expected and processed periods; make the glossary match that stronger treatment.

## Additional improvements, without treating open decisions as defects

- **Recovery time:** Section 12 correctly asks for a decision window. Also record the latest safe decision point after allowing for the actual recovery, reprocessing and business reconciliation time. Define permitted data loss or backlog explicitly where applicable. These values must come from service requirements and rehearsal, not guesses.
- **Medium/low coverage:** Sections 3 and 11 promise evidence for every DAG, while several exit measures focus on critical/high DAGs. Make the final population reconciliation explicit: every in-scope item is passed, intentionally paused with accepted evidence, or has an approved exception. Report those separately; do not count exceptions as successful execution.
- **Comparable metrics:** define the reporting window, due-time cutoff, treatment of paused workflows and late-but-successful runs, and how reruns/duplicates affect the numerator. Otherwise success/expected-run ratios can mislead. Base normal-performance comparisons on matched workload volumes and business periods.
- **New deployment versus in-place:** the p.4/p.18 metadata migration check should be conditional on the selected path. For a new deployment, require target readiness and agreed history access instead of implying source metadata was transferred. [Astro upgrade strategies](https://www.astronomer.io/docs/astro/airflow3/upgrade-af3)
- **Incident versus problem closure:** p.12 requires root cause before incident/data-gap closure. Confirm this against the organization's incident policy; service restoration, reconciled outputs and a linked owned root-cause/problem record may be distinct milestones. Do not weaken business-output acceptance.
- **Readability:** inspected pages are legible and tables are generally consistent. Figure labels/captions are small, and the figures need semantic correction more than cosmetic redesign. The contents table would be easier to use with page numbers or PDF navigation links.

## How to use it in the roadmap

Keep this as a proposed companion to P5 readiness, P6 cutover acceptance, P7 stabilization and P8 operational handover. Its own gates should use a distinct prefix, such as HC0–HC7, to avoid confusion with roadmap G0–G8. Full program closure also includes the master roadmap's retirement/retention approvals; this post-migration strategy need not duplicate the entire pre-migration plan.

Suggested revision order: fix containment and recovery diagrams; add execution-version evidence; correct the architecture view; separate criticality from frequency; split first-hour versus later evidence; clarify entry/governance and technical definitions; then obtain answers to Section 12 and rehearse the chosen procedures.

## Review limitations

Text from all 21 pages was reviewed, pages were rendered, and the key figures, tables and referenced finding locations were visually inspected. Technical checks used versioned Apache Airflow 3.2.0 documentation plus current Astro documentation, accessed 6 October 2026. The actual target patch, Runtime, providers, executor, bundle implementation and offering remain unconfirmed; verify exact-build behavior before approving commands. No production test, live-platform assessment, business approval or implementation acceptance is implied.
