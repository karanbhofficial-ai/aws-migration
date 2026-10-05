# Proposed ownership and responsibility matrix

Draft — 6 October 2026. These roles are proposals, not assignments to known people. Karan and Shailesh have not been assigned project accountabilities by this document.

## Initiative roles reported in the supplied slide

| Slide role | Slide value | Boundary |
|---|---|---|
| Originating organization | SRE | Does not establish each team's delivery responsibilities |
| Primary VP | Grace Chorey | Does not establish production change authority |
| Initiative owner | Gaja Shenoy | Does not establish day-to-day migration leadership or technical ownership |
| Initiative requestor | Gaja Shenoy | Preserved as a separate slide title |

These names/titles are slide-derived; spelling and current assignments have not been separately confirmed. Approval status of the overview is unknown. Application teams are explicitly identified as participants in assessment, testing, remediation and coordinated deployment; individual owners and allocations remain TBD.

## Proposed execution roles

| Code | Proposed role | Person / team | Main responsibility |
|---|---|---|---|
| ML | Migration lead | TBD | Scope, coordination, estimates, dependency and decision tracking |
| PL | Platform lead | TBD | Offering, environments, supported migration path, configuration and vendor coordination |
| EL | Engineering lead | TBD | DAGs, shared packages, custom components and integration changes |
| TL | Test lead | TBD | Coverage, automation, evidence, defects and readiness recommendation |
| BO | Business/workload owner | TBD per workload | Business results, deadlines, tolerances, criticality and acceptance |
| OL | Operations lead | TBD | Monitoring, recovery, on-call procedures and service acceptance |
| SA | Security/access lead | TBD | Identity, access, secrets and security requirements |
| CA | Change authority / sponsor | TBD | Production authorization, material risk acceptance and retirement authorization |
| AV | Astronomer representative | TBD | Contracted platform responsibilities and supported upgrade/recovery advice |

A = accountable for the outcome; R = performs the work; C = consulted; I = informed. Each row has one proposed accountable role. A role may also perform the work. Name a specific BO for each affected workload rather than relying on a generic group approval.

| Outcome | A | R | C | I |
|---|---|---|---|---|
| Scope, plan and staffing | ML | ML | CA, PL, EL, TL, OL, BO | AV, SA |
| Offering and vendor responsibility agreement | PL | PL | AV, ML, OL | CA |
| Deployment inventory | PL | PL | AV, EL, OL, SA | TL, ML |
| DAG and dependency inventory | EL | DAG/integration engineers, names TBD | PL, BO, TL | ML, OL |
| Business criticality and requirements | BO | Workload representatives, names TBD | TL, OL, EL | ML, CA |
| Target and recovery design | PL | PL, OL | AV, EL, SA, BO, TL | ML, CA |
| Code and dependency remediation | EL | DAG/integration engineers, names TBD | PL, TL, BO | ML, OL |
| Test strategy and evidence | TL | Test contributors, names TBD | EL, PL, BO, OL | ML, CA |
| Business output acceptance | BO | Business validators, names TBD | TL, EL | ML, OL, CA |
| Access/security acceptance | SA | SA, PL | AV, OL | ML, CA |
| Cutover and recovery rehearsal | OL | OL, PL, EL | AV, TL, BO | ML, CA |
| Production go/no-go and rollback authority | CA | ML coordinates the decision | PL, OL, TL, BO, EL, AV | SA |
| Production migration execution | PL | PL, OL; AV only where contracted | EL, TL, BO | ML, CA, SA |
| Operational acceptance | OL | OL | BO, TL, PL, EL | ML, CA, AV |
| Retirement authorization | CA | ML | BO, OL, PL, SA, AV | EL, TL |
| Retirement execution | PL | PL, OL | AV, SA | ML, CA, BO |

## Vendor boundary to resolve before G0

For each activity, record the customer owner, vendor owner, who executes it, what access is required, support lead time, and written evidence of agreement. Specifically resolve environment provisioning, runtime upgrades, metadata protection/restoration, cleanup, configuration changes, monitoring, incident escalation, version eligibility, rollback execution, and retention. Do not infer that “fully managed” includes application remediation or business validation.

The ML must also confirm primary and backup operators for cutover, the person authorized to stop activation, the person authorized to invoke recovery, and coverage through the agreed observation period. Contact details belong in the controlled operational contact list.
