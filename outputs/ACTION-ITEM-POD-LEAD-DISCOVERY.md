# Action item AWS-ACT-POD-001: POD-lead discovery and validation

Prepared 6 October 2026 | Owner: Karan, unless the application coordinator assigns another owner | Status: Not started / current status unknown | Due date: TBD

## Purpose

Connect with each POD lead or consuming application owner and produce a verified record of what each in-scope server supports, how it is used, what can be affected by RHEL-to-Amazon-Linux migration, and how the application will be validated afterward.

This is an application-team discovery and validation activity. It does not ask the POD lead or Karan's team to provision EC2, build VPCs, perform OS migration, or execute server cutover. The central automation/migration team owns those infrastructure actions.

The screenshots and prior chats are leads for this action. Do not treat a screenshot status, an unverified server name, or a historical “working on it” response as completion.

## Inputs to collect before contacting leads

1. The authoritative Data SRE/ServiceNow server export and the required spreadsheet format. `RITM006971658` is a screenshot-derived sample request reference; confirm its current applicability.
2. The server-group allocation, with a primary and backup contact for each group.
3. The SRE patching contact, approved Vault/service-account access path, and POC readiness contact.
4. The current inventory draft and aliases, including the candidate rows for `mrdw-oracle-dev-01`, `npsprod-netezza-1`, `mi-mdp-dpde-rev9-dp-prod`, and the distributed-platform records.
5. The meeting-note and workload-record template in this document.

If an access request is needed, request the Vault path or service-account reference and approval/request ID. Do not ask people to paste passwords, tokens, private keys or other secrets into chat, email, spreadsheets or this repository.

## Opening script

> “The purpose of this discussion is to identify every application, script, job and service that uses the assigned server group, directly or through Vault or another shared service. We are collecting the information needed for the RHEL-to-Amazon-Linux migration, application changes and post-migration validation. Our team is not provisioning or migrating the AWS servers. We need your help to confirm usage, dependencies, owners, test scenarios and evidence.”

Confirm the agenda:

> “Are we covering the server identity, the applications and jobs using it, dependencies and access paths, operational and business criticality, required application changes, and how your team will validate the workload on the AWS POC and after production migration?”

## Questions to ask the POD lead

### 1. Server identity and scope

- Which exact hostname, instance ID, AWS account, region, private IP and environment are you referring to?
- Does the name in our list have aliases or a different CMDB/ServiceNow identity?
- Is this server in scope for RHEL-to-Amazon-Linux migration? If not, why: duplicate, retired, temporary, shared platform, wrong owner or another program?
- Is it development, test, performance, nonproduction or production? What evidence supports that classification?
- Is it shared with other PODs or teams? Who else should be interviewed?

### 2. Consumers and ownership

- Which POD, application, service, script, job or platform component uses the server?
- Is the use direct, through a Vault/service account, through another application, or through a shared mount/service?
- Who is the technical owner, backup owner, operator and business validation/sign-off owner?
- Which support team receives an incident when it fails? Who can restart or recover it?
- Are there users or teams who use it only occasionally, monthly, quarterly or during an ad hoc process?

### 3. Workload execution

- What is the exact executable, script, service, job or process name?
- Where is the source repository, deployed path and current revision? Capture a link or reference, not credentials.
- How is it started: systemd, cron, timer, scheduler, pipeline, manual command, application call or another service?
- What run account, service account, Vault reference, environment variables and configuration files does it use?
- What are the schedule, timezone, duration, concurrency, retry and restart behaviours?
- What input files, output files, logs, reports, tables or messages does it read or create?
- Which directories and mounts are required? What is the underlying storage: local disk, NFS/shared filesystem, object storage or another service?

### 4. Dependencies and connectivity

- Which databases, schemas, drivers and connection methods are used? Ask specifically about DB2, Oracle, Netezza or other databases where the server name suggests one.
- Which applications, APIs, queues, file shares, DNS names, certificates, proxies or external endpoints are called?
- For each connection, what is the destination, direction, protocol, port, authentication reference, owner and failure impact?
- Are any hostnames, IP addresses, mount paths, ports, certificates or credentials hard-coded in scripts or configuration?
- Does the workload depend on AWS CLI, SDKs, Snowflake, S3, another cloud, a corporate network, VPN or a private endpoint?
- Does it depend on another server starting first, a database service being restarted, or a specific maintenance/patching order?

For the `lnxprd0799` reporting case, ask the Reporting COE to demonstrate the Cognos portal and package/report flow, identify the exact DB2 instance/service and connection path, provide the SOP, and name the UAT approver. Cognos was described in prior chat as hosted separately with an indirect DB2 dependency; confirm this rather than describing Cognos as installed on the RHEL server.

### 5. RHEL-to-Amazon-Linux impact

- Which RHEL-specific packages, repositories, commands, libraries, shells, interpreters, compilers or agents are required?
- Does the workload rely on `yum`, `dnf`, `amazon-linux-extras`, `rpm` behaviour, `cron`, `systemd`, SELinux settings, file ownership or a particular kernel feature?
- What exact Python, Java, Perl, DB2 client, Oracle client, Netezza client, AWS CLI or native library versions are used?
- What changes are expected if the hostname, private IP, OS user, filesystem path, package name, runtime version, certificate or service start order changes?
- Are there binary, architecture, vendor-support or licensing constraints? Which official support evidence is available?
- What application remediation is required, and who will implement and peer-review it?

### 6. Criticality, operations and recovery

- What is the business purpose and criticality? Is it revenue-generating, customer-facing, regulatory, operational, or a supporting service?
- What is the allowed outage, recovery time objective, recovery point objective and acceptable data loss?
- What backup, restore, monitoring, alerting, logging, patching and capacity evidence exists?
- What is the normal start/stop/restart procedure and what is the known failure procedure?
- What happens if the workload runs twice, runs late, misses an input, or produces partial output?
- Which operational team accepts the handover after hypercare?

### 7. POC, testing and business acceptance

- What can be tested on the AWS POC without affecting production data or users?
- Which technical checks are required: login/authentication, connectivity, package/runtime checks, service startup, schedule execution, logs, retries and recovery?
- Which business scenarios must pass? What source output or baseline will be compared, and what tolerance is acceptable?
- Who will execute the test, provide test data, review results, retest defects and sign off UAT?
- What evidence can be retained: redacted logs, result files, screenshots, run IDs, reconciliation reports, defect links and approvals?
- What is the test rollback or cleanup procedure for the POC?

### 8. Disposition and wave readiness

- Should this workload be migrated, remediated first, retired, deferred or handled with another workload because of a shared dependency?
- Which other servers or applications must be in the same migration wave?
- What predecessor activities, access approvals, vendor responses or business windows are required?
- What is the latest safe rollback point and what condition would trigger rollback?

## Evidence to request

Ask the lead to provide or point to these artifacts, subject to approved access and redaction:

- Current architecture or dependency diagram.
- Application/service inventory and deployed version.
- Runbook or SOP, including failure and restart procedures.
- Scheduler/job list and representative run history.
- Package/runtime/client inventory and relevant configuration references.
- Mounts, input/output locations and interface/endpoint list.
- Vault/service-account reference and approved access/request ID; never secret values.
- Representative source output and target validation baseline.
- Test cases, UAT approver and existing defect/evidence links.

## Meeting-note template

| Field | Record |
| --- | --- |
| Meeting ID / date / attendees / POD | TBD |
| Server group and canonical server IDs | TBD |
| Confirmed aliases, environment and source OS | TBD |
| Consumer applications, scripts, jobs and services | TBD |
| Direct/Vault-mediated/shared-service use | TBD |
| Technical owner / backup / operator / business approver | TBD |
| Runtime/packages/clients/configuration | TBD |
| Schedules/run accounts/mounts/inputs/outputs | TBD |
| Dependencies and connection evidence | TBD |
| Criticality/RTO/RPO/outage/data-loss tolerance | TBD |
| RHEL-specific impact and remediation | TBD |
| POC scenarios, baseline, tester and UAT approver | TBD |
| Proposed disposition and wave coupling | TBD |
| Open questions / action / owner / agreed date | TBD |
| Evidence links and lead confirmation date | TBD |

## Follow-up message template

> Subject: AWS migration discovery confirmation – [POD] / [server group]
>
> Thank you for the discussion. Please confirm the attached/linked record for [server/application]. We captured: [servers and aliases], [applications/jobs], [direct or Vault-mediated access], [dependencies], [owners], [operational procedure], [RHEL impact], and [POC/UAT scenarios].
>
> Please correct any item marked unknown and provide the missing evidence for [open items]. Please also confirm the business validation approver and whether the workload should migrate, be remediated first, be retired, or be deferred. Do not send passwords, tokens or private keys; provide approved Vault/service-account references and request IDs only. We will record unresolved items in the action and RAID registers.

## Definition of done

Close AWS-ACT-POD-001 for a server group only when:

1. The canonical server identity is reconciled with the authoritative export.
2. Direct, indirect, Vault-mediated and infrequent consumers are identified or explicitly dispositioned.
3. Each retained workload has an owner, purpose, execution method, schedule, runtime/package baseline and dependency record.
4. Criticality, recovery expectations, operating procedure and support owner are recorded.
5. Required application remediation and official compatibility evidence are identified.
6. POC/test scenarios, expected results, evidence location and business approver are agreed.
7. Migration disposition, wave coupling, rollback constraints and open actions have owners and agreed dates.
8. The POD lead confirms the record or the disagreement is documented and escalated.

## Useful official guidance

These links are planning references, not permission to deploy agents or collect data. Central migration/SRE approval is required for any discovery tooling or access change.

- [AWS application portfolio assessment guide](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/introduction.html) — separates portfolio-level inventory from detailed application assessment.
- [AWS baseline application portfolio guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/baseline-application-portfolio.html) — recommends mapping application-to-infrastructure, component and application-to-application dependencies and combining tooling with stakeholder input.
- [AWS detailed application assessment](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/detailed-application-assessment.html) — provides stakeholder prompts for resiliency, security, databases and dependencies, and recommends validating static knowledge with programmatic discovery.
- [AWS complete assessment data requirements](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/understanding-complete-assessment-data-requirements.html) — useful field checklist for application, infrastructure, network and migration data.
- [AWS Systems Manager Inventory](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html) — can collect metadata such as applications, files, network configuration, system properties and services from managed nodes; it collects metadata, not proprietary data.
- [AWS Application Discovery Service](https://docs.aws.amazon.com/application-discovery/) — an option for automated application/dependency discovery and migration planning where the central team approves it.
- [AWS application design and migration strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/aws-application-design-and-migration-strategy.html) — connects discovered information to target design, operational readiness, cutover considerations and RAID ownership.

