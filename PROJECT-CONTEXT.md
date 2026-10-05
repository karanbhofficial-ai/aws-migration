# Airflow 2.x to 3.x Migration

Prepared 6 October 2026 from Karan's current request and available older chat messages. This is a starting brief, not an approved migration plan.

## Objective and organization

Karan has one overall team divided into two teams, one for Airflow migration and one for RHEL to Amazon Linux on AWS. He wants separate projects and complete end-to-end roadmaps. In the earlier chat Review Migration Questions, Karan reported that Shailesh confirmed the migrations are independent. Shared staffing and leadership reporting may still require coordination; details are unknown.

## Existing context

- Discussions describe Airflow as fully managed by Astronomer. Confirm the exact deployment offering and responsibility split.
- A meeting transcript refers to approximately 1,500+ DAGs, but transcription and the current inventory need verification.
- The planning emphasis includes compatibility assessment, scalable validation, unchanged intended business outcomes, and evidence of completeness.
- Earlier discussions raised parallel/shadow testing and a dedicated production environment for critical DAGs as questions, not approved decisions.
- Databricks was discussed as a possible integration; actual usage is not established.
- A ChatGPT project named Airflow migration 2x to 3x already exists. This folder has not yet been registered as a local Codex project.

## Roadmap to develop

Scope and responsibility agreement; inventory and current architecture; exact source/target versions; compatibility and integration assessment; target design and pilot; remediation and deployment pipeline; migration waves; automated and business validation; cutover and rollback rehearsals; production approval; hypercare; handover and retirement of the old platform.

Each phase should identify deliverables, accountable owners, dependencies, estimates, acceptance criteria and evidence. Exact dates and staffing remain TBD; the supplied initiative slide now provides a stated 2026/2027 delivery split, recorded below.

## Initial questions

1. Team members, roles, allocation and shared resources?
2. Target dates and current completed, active or blocked work?
3. Exact Airflow and Astro Runtime versions, environments, executor and deployment model?
4. Verified DAG inventory, criticality, schedules, integrations and business validation owners?
5. Astronomer responsibilities and agreed migration/rollback options?

## Source chats

- Airflow Migration Roadmap: 6ab425aa-168c-83e8-8ca7-f41e4a67ee15
- Review Migration Questions: 6abcba39-6850-83e8-91d7-e5fee83c9195
- OpenShift To AWS Migration: 6ab51584-7f10-83ee-b0c9-f4ab252feb3c (includes management discussion of both initiatives)

Some source attachments were unavailable. Prior assistant technical claims and generated files have not been independently verified. Do not treat them as approved project facts.

## Initial local planning work — 6 October 2026

- A proposed planning pack exists in `outputs/`, starting at `outputs/01-MIGRATION-ROADMAP.md`; `outputs/README.md` indexes its supporting task plan, ownership matrix, inventory/evidence schemas, testing strategy, cutover/rollback/handover runbook, risk/decision/question registers, and technical source review. It was initially v0.1 and is now v0.2 after incorporating the initiative slide.
- This is drafting progress only; no live platform, code repository, or inventory was inspected. Task-level status, delivery dates, execution-role assignments, staffing and exact technical versions remain unverified. The slide supplies the broader direction and reported status below.
- Official Apache Airflow and Astronomer documentation was reviewed for general compatibility, Astro-specific upgrade eligibility, Runtime selection and rollback limitations. References and applicability caveats are in `outputs/08-TECHNICAL-CHECKS-AND-SOURCES.md`. Exact deployment eligibility and vendor responsibilities remain unverified.
- The plan distinguishes development batches from production change units. A separate target environment is a proposal to evaluate, not a selected approach. In-place readiness must cover the affected deployment; recovery must address external data effects as well as platform state.
- Initial questions concerned offering/versions, deadline/status and ownership. The slide partially answers these; ask only for remaining details. Do not infer execution-role assignments from initiative titles.

## User-provided initiative slide — 6 October 2026

Evidence classification: slide-derived, not independently verified; slide date and approval status unknown. Full extraction and source file path: `work/initiative-slide-extraction.md`.

- Initiative: Airflow Upgrade - SRE, describing Marriott's platform. Originating organization: SRE. Enterprise KPI: Compliance.
- Stated target: Airflow 3.2.x. Source is described as legacy Astronomer 2.x; exact installed Airflow/Runtime versions, target patch, Python and offering remain unknown.
- Primary VP: Grace Chorey. Initiative owner and requestor: Gaja Shenoy. These are slide role labels, not assignments as migration lead, business validator or production change authority.
- Slide estimate: nine months, with no start date on the slide. Karan subsequently confirmed a planned start in mid-October 2026 and that investigation and planning are already underway. Exact start day, individual task completion and size definitions remain unconfirmed. Slide-reported status: In Progress; Assessment; Strategy on small/large deployments.
- Stated 2026 scope: upgrade/validate lower environments for all in-scope applications; application-team compatibility assessment, tests and remediation; required Terraform/infrastructure changes; operational readiness and production preparation.
- Stated 2027 scope: production upgrades and remaining workload migration with application owners; stability/performance validation; legacy-runtime decommissioning and completed Airflow 3.2.x adoption.
- Success objectives: all in-scope deployments migrated; no material stability/performance degradation; zero critical defects or unplanned business impact during cutover. Quantitative acceptance definitions remain to be agreed.
- Slide cites April 2027 End of Life. Official lifecycle review distinguishes maintenance from Basic Support; do not treat the slide's phrase as verified for an unidentified Runtime. See `outputs/08-TECHNICAL-CHECKS-AND-SOURCES.md`.
- Continent impact is marked NO; its meaning is unknown and does not mean zero migration risk. Funding fields for 2026/2027 and PORT# show no visible values.
- Karan confirmed approval status is unknown. Treat the overview as planning input, not an approved baseline.
- Schedule inference: if the slide's nine-month estimate starts in mid-October 2026, it points to approximately mid-July 2027. This extends past the slide's April 2027 lifecycle claim. Resolve whether production migration must finish earlier, what the applicable vendor deadline is, and whether later time is intended for stabilization/closure; no resolution is assumed.

## Karan-authored post-migration strategy review — 6 October 2026

- Karan supplied `C:/Users/Karan/Downloads/Airflow_2x_to_3_2x_Post_Migration_Strategy_document.pdf` and explicitly said he created it; it was not provided by the business or client. It is a 21-page post-cutover strategy dated 5 October 2026. Treat its content as author proposals, not approved client requirements or proof of the operating environment.
- Review saved at `outputs/09-POST-MIGRATION-STRATEGY-REVIEW.md`; extracted text/renderings are under `work/`. The PDF was not changed.
- Useful proposed content: distinct platform/workflow/business-output validation, intentionally paused DAG controls, evidence-based hypercare, incident/recovery procedures, output reconciliation and operational handover. Suitable as a companion to roadmap P5–P8 after revision/review.
- Main findings: pausing alone is insufficient containment; recovery diagrams put the decision gate after recovery; code/bundle/image identity is needed for reruns; Figure 2 omits the worker-to-Execution-API path; frequency must not determine low criticality; first-hour checks cannot demand completed continuity evidence for every long-running/infrequent workflow. Further findings cover backfill applicability/concurrency, handover/exception boundaries, proposed governance, logical-date wording and traceable references.
- ServiceNow, POD ownership, particular assignment groups, named execution roles and referenced source-workbook contents remain unconfirmed. The draft's title/status and source list do not establish approval or those facts.
- Technical checks used Apache Airflow 3.2.0 references and current Astro guidance; exact installed/target versions and offering remain open. No new client commitments, task completion or runtime changes were inferred from this document.
- Review actions have been implemented in the planning pack: T45–T58 in `outputs/02-TASK-PLAN.md`, containment/recovery/version-identity controls in `outputs/05-TESTING-STRATEGY.md` and `outputs/06-CUTOVER-ROLLBACK-HANDOVER.md`, and decisions D13–D16 in `outputs/07-REGISTERS.md`. The original PDF remains unchanged.

## AWS migration context in this repository

The repository also contains the separate RHEL-to-Amazon-Linux-on-AWS planning pack. Airflow and AWS migration remain separate projects; shared staffing and reporting are coordination concerns only.

- AWS roadmap: `outputs/MIGRATION-ROADMAP.md`
- AWS registers: `outputs/MIGRATION-REGISTERS.md`
- AWS server inventory draft: `outputs/SERVER-INVENTORY-DRAFT.md`
- AWS discovery and access plan: `outputs/DISCOVERY-ACTION-PLAN.md`
- AWS S02 RAID/status register: `outputs/RAID-AND-STATUS-S02.md`
- AWS source extractions: `outputs/SOURCE-S01-INITIATIVE-OVERVIEW.md` and `outputs/SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md`

The AWS work is an application-team planning draft. Central migration/automation teams own AWS provisioning and server migration. Screenshot-derived server rows and historical chat statuses are leads only and require reconciliation with the authoritative Data SRE/ServiceNow export. No AWS migration gate is recorded as accepted in this repository.

The reviewed AWS chats also support a focused POD-lead action: discover direct, indirect and Vault-mediated consumers; capture scripts, packages, database/Snowflake/AWS CLI connections, schedules, external endpoints, configurations, secrets references, hard-coded hostnames/IPs and RHEL-specific behaviour; then agree POC/UAT validation and migration disposition. See `outputs/ACTION-ITEM-POD-LEAD-DISCOVERY.md`. Airflow chat material remains in the Airflow planning pack and is not part of this AWS action.
