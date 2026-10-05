# RHEL to Amazon Linux on AWS Migration

Prepared 6 October 2026 from Karan's current request and available older chat messages. This is a starting brief, not an approved migration plan.

## Objective and organization

Karan has one overall team divided into two teams, one for Airflow and one for AWS migration. He wants separate projects and complete end-to-end roadmaps. His latest request identifies the AWS migration as RHEL to Amazon Linux. Exact OS releases, hosting details and implementation approach remain unconfirmed.

In Review Migration Questions, Karan reported Shailesh's confirmation that the Airflow and AWS migrations are independent. Shared staffing and leadership reporting may require coordination.

## Responsibility boundary

The available management transcript and Karan's messages establish that his team acts as the application team. Central migration/automation teams handle AWS infrastructure provisioning and server migration. The application team's work includes workload discovery, application dependencies, required script/configuration changes, functional and regression validation, issue coordination and evidence of successful business operation. Confirm detailed ownership with migration, SRE and consuming teams.

## Discovery approach

Identify each server's consuming pods, active applications/scripts/jobs, paths, schedules, packages, runtimes, external connections, accounts, mounts, server-specific configuration, criticality, technical owner, business validation method and sign-off owner. Explicitly record obsolete workloads rather than assuming everything must migrate.

Suggested inventory relationship: Server -> Consuming pod -> Workload -> Dependencies -> Migration requirement -> Owner -> Test/evidence -> Sign-off/status.

## Known example: lnxprd0799

The Migration validation summary chat includes a Reporting COE meeting transcript. Cognos is hosted separately from the server; the reporting flow has an indirect dependency involving DB2 services on the server. Reporting failures were described as requiring SRE checks or restarts of DB2 services. Confirm the exact DB2 architecture and connectivity.

Discussed follow-ups included Cognos portal access, an SOP, DB2/connectivity details, testing on an AWS POC, and Reporting COE UAT. These are discussed actions; completion is unknown. Feasibility is not yet demonstrated by validation evidence in the retrieved material.

## Roadmap to develop

Scope and responsibility agreement; server/consumer discovery; workload and dependency inventory; source baseline and target compatibility assessment; infrastructure readiness handoff; application remediation; POC and business validation; migration waves; cutover and rollback coordination; production validation and sign-off; hypercare; operational handover; old-server decommissioning approval.

Each phase needs deliverables, owners, dependencies, estimates, acceptance criteria and evidence. Infrastructure milestones should appear as dependencies with their actual owning team.

## Initial questions

1. Team members, roles, allocation and shared resources?
2. Deadlines and current completed, active or blocked work?
3. Server list, environments, source RHEL and target Amazon Linux releases?
4. Confirmed migration-team approach and readiness milestones?
5. Discovery tracker, consuming pods, access gaps and validation owners?
6. Current status of lnxprd0799 POC, SOP, Cognos access and DB2 assessment?

## Source chats

- OpenShift To AWS Migration: 6ab51584-7f10-83ee-b0c9-f4ab252feb3c (title retained; do not infer OpenShift is in scope)
- Migration validation summary: 6abbb1b4-488c-83ee-965c-23ed34cb3b20
- Call Objective Discovery: 6ac3971b-8598-83ee-b8a8-7b9ab010f24a
- Review Migration Questions: 6abcba39-6850-83e8-91d7-e5fee83c9195
- AWS KT Planning: 6ac320a9-f428-83ec-8026-6c5422797dd5 (training context; demo resources are not evidence of production architecture)

Some source attachments were unavailable. Prior assistant technical claims and generated files have not been independently verified. The initial brief reported that this folder had not yet been registered as a local Codex project; current registration status has not been checked.

## Working roadmap and registers - 6 October 2026

Created a proposed, undated roadmap in [outputs/MIGRATION-ROADMAP.md](outputs/MIGRATION-ROADMAP.md) and starter actions, risks, decisions and evidence templates in [outputs/MIGRATION-REGISTERS.md](outputs/MIGRATION-REGISTERS.md).

The roadmap covers scope through central-team source retirement, with application validation gates and explicit central-team dependencies. Individual phase completion remains unverified; delivery roles are proposed and phase estimates are TBD. A subsequently supplied initiative slide provides program roles, a three-month estimate and reported assessment status; see S01 below. No target Amazon Linux release has been selected. lnxprd0799 is a transcript-derived discovery case, not an approved pilot or proof of compatibility.

AWS documentation was consulted for conditional AL2023 planning checks, and IBM's official Db2 requirements entry point was identified. No workload-specific compatibility assessment can be completed until exact source/target OS and product versions are confirmed. Documentation links are in the roadmap.

Questions raised for the next planning update: deadline and evidence of current progress; scoped servers/environments and exact OS releases; application/central coordinators and business validation approvers. S01 partially informs program duration, status and leadership; the detailed questions remain open.

## Source S01: initiative overview photograph - received 6 October 2026

Karan supplied a photograph titled RHEL to AWS migration - SRE. See [source extraction and roadmap mapping](outputs/SOURCE-S01-INITIATIVE-OVERVIEW.md) for provenance and limitations.

Slide-derived information: Marriott program; originating organization SRE; initiative owner and requestor Gaja Shenoy; Primary VP first name appears to be Grace, surname needs verification; enterprise KPI Compliance; estimated duration 3 Months; reported status In Progress / Assessment. The slide date and approval status are not visible, so this is not confirmed current phase progress or an approved delivery schedule.

The slide lists assessment/planning, build/remediation, lower-environment testing, phased production cutover and stabilization/transition. Its heading says 2026: Platform Readiness & Lower Environment Upgrades even though production steps are included; no separate 2027 deliverables are visible. Karan confirmed on 6 October 2026 that the three-month estimate covers the full migration through hypercare (P01-P10). Start/end dates, elapsed/remaining time and year boundaries remain open; do not start a new three-month clock from this conversation. Source retirement timing is not automatically included. Funding amounts are not visible. The Continent Impact field says NO, but its definition is unknown.

Success targets are 100% of in-scope workloads migrated and validated, critical application/service validation, business continuity with rollback readiness, and operational readiness. These targets now inform proposed roadmap measures; no achieved result is inferred. Program leadership does not replace named application, central-team, business or gate owners. Existing application-team responsibility boundaries and separate Airflow project remain in effect.

Roadmap updated to draft v0.2, with actions A09-A11, risk R08 and decisions DEC08-DEC09. DEC08 is partially resolved by Karan's answer: full migration through hypercare. A09 remains open for dates and year boundaries. No phase completion or schedule feasibility is implied by this clarification.

## Source S02: chat screenshots and partial inventory - received 6 October 2026

Karan supplied eight screenshots from project chats and inventory views. The extraction and limitations are recorded in [outputs/SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md](outputs/SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md); candidate records are in [outputs/SERVER-INVENTORY-DRAFT.md](outputs/SERVER-INVENTORY-DRAFT.md). The image files are retained under `work/sources/S02/`.

S02 provides candidate rows for `mrdw-oracle-dev-01` (`10.212.30.34`, `m4.2xlarge`, RHEL 8, development), `npsprod-netezza-1` (`172.30.33.218`, `t3.2xlarge`, RHEL 8, production context), and `mi-mdp-dpde-rev9-dp-prod` (`172.25.35.245`, `m5.2xlarge`, RHEL 8, MDP-TCS context). It also shows candidate distributed-platform records, including a development server used by Hotels Ops for key-pair testing, a production server used by SRW, and a nonproduction performance-looking record with instance `i-02ac4348aea705787` and IP `172.25.41.61`. These are leads only; apparent duplicate/conflicting mappings require reconciliation with the authoritative Data SRE/ServiceNow export.

S02 chat items ask the application team to distribute server groups, contact SRE patching, identify direct and Vault-mediated consumers, contact application teams, request Vault/service-account access, document meetings, create AWS and Airflow RAID/action trackers, and raise a Data SRE ServiceNow request using sample `RITM006971658`. The screenshots also describe grouping shared servers, one request per group, internal review for possible low-load consolidation, and preparing to replicate application steps when an AWS POC is ready. Completion, ticket status, owners and dates are unknown.

The screenshots reinforce the responsibility boundary: the application team does not provision or execute AWS server migration; the automation/migration team handles that work. The application team coordinates with owners, validates scripts, confirms connectivity/login and checks applications after migration. A screenshot includes a historical POD-lead status table; it is retained as follow-up evidence, not current progress. See [outputs/DISCOVERY-ACTION-PLAN.md](outputs/DISCOVERY-ACTION-PLAN.md) and [outputs/RAID-AND-STATUS-S02.md](outputs/RAID-AND-STATUS-S02.md).
