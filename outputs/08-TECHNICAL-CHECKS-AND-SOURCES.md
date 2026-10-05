# Official technical checks and source register

Reviewed on 6 October 2026. These are documentation-derived checks, not observations of Karan's environment. The supplied slide states an Airflow 3.2.x target; its approval status and exact technical version set remain unresolved. Apache's moving `stable` pages displayed 3.3.2 when opened; that is a documentation snapshot, not a recommended project target. Recheck the exact selected-version documentation, Runtime release notes, provider requirements, and vendor eligibility at G2 and before execution.

## Lifecycle statement from the initiative slide

The slide describes April 2027 as End of Life. Astronomer's current table instead lists **Runtime 13 / Airflow 2.11** maintenance ending in April 2027 and Basic Support ending in April 2028. This does not establish the installed version or its contractual deadline. Confirm both before accepting the slide's terminology. [Official Runtime lifecycle policy](https://www.astronomer.io/docs/runtime/runtime-version-lifecycle-policy)

Schedule inference: nine months from the user-confirmed planned mid-October 2026 start points to approximately mid-July 2027. Resolve production-completion timing versus the applicable lifecycle deadline before approving the schedule; later stabilization/closure is a possible interpretation, not an agreed plan.

## Verified constraints to carry into discovery

### Apache upgrade checks

Apache lists Airflow 2.7+ as a prerequisite and recommends the latest 2.x before 3. Check supported Python, backup/recovery readiness, configuration changes and DAG processing errors. Ruff AIR301/AIR302 identify breaking changes; AIR311/AIR312 identify recommended updates. The guide specifies Ruff 0.13.1 or newer. Review fixes before applying them. [Apache upgrade guide](https://airflow.apache.org/docs/apache-airflow/stable/installation/upgrading_to_airflow3.html)

Assess standard-provider dependencies, removed SubDAGs/executors/SLA behavior, context variables, REST API v2 migration, authentication, plugins, and scheduler/component changes. Test catchup, cron timetable defaults, manual-run intervals and XCom retrieval explicitly. Applicability depends on actual usage and the selected release. An import scan alone does not establish behavioral equivalence. [Apache upgrade guide](https://airflow.apache.org/docs/apache-airflow/stable/installation/upgrading_to_airflow3.html)

### Public interfaces

Airflow 3 identifies `airflow.sdk` as its DAG-authoring interface. Task code must not depend on direct metadata-database access. Review private imports and custom state queries; use the documented Task Context, SDK or stable REST API appropriate to the operation. Record replacements and validate their behavior. [Apache public interface](https://airflow.apache.org/docs/apache-airflow/stable/public-airflow-interface.html)

### Astro-specific eligibility — apply only after confirming the offering

Astro documents new-deployment and in-place routes. In-place prerequisites include Runtime 13.7.0+, eligible target patches, and no metadata table over 50 GB; nonterminal runs/tasks fail during migration. A new deployment does not transfer historical task data. Providers previously bundled may need explicit installation. Airflow-2 rollback targets 2.11 on Runtime 13.7.0+, with documented Airflow-3 rollback support starting at Runtime 3.0-11. Confirm the exact version pair with Astronomer. [Astro major-version upgrade guide](https://www.astronomer.io/docs/astro/airflow3/upgrade-af3)

Do not apply hosted Astro rules automatically to Astro Private Cloud or another offering. T03 must establish which documentation and support process governs the actual platform.

### Runtime selection and release controls

Check maintained/support status, restricted versions, and supported Python images when selecting the target. Runtime lifecycle and upstream Airflow lifecycle are distinct inputs; record the vendor policy applying to this deployment. [Runtime lifecycle policy](https://www.astronomer.io/docs/runtime/runtime-version-lifecycle-policy)

The general Runtime upgrade guide covers upgrades within a major Airflow version and directs Airflow 2-to-3 work to the dedicated guide. For later changes, it also flags possible disruption during database migrations and downgrades. Record actual deployed image identity so tests can be traced to the candidate. [Runtime upgrade guide](https://www.astronomer.io/docs/runtime/upgrade-astro-runtime)

### Recovery limitations

Astro deploy rollback restores project code and Runtime, but not resource settings or environment variable values. A downgrade can erase metadata for unsupported features and fail running tasks. Remote Execution Agents, if present, need separate compatible rollback handling. Therefore, capture configuration separately and verify recovery behavior, artifact availability and external-output reconciliation in rehearsal. [Astro deploy history and rollback](https://www.astronomer.io/docs/astro/deploy-history)

## Required technical decision record

| Item | Evidence required | Current value |
|---|---|---|
| Offering and execution model | Platform export and responsibility agreement | TBD |
| Source version set | Airflow, Runtime, Python, providers, custom packages, image identity | TBD |
| Target version set | Exact compatible versions and eligible image, release-note review | Slide direction: Airflow 3.2.x; exact set TBD |
| Intermediate upgrade | Required/recommended steps for the chosen offering and source | TBD |
| Unsupported features | Usage scan mapped to exact-target release notes | TBD |
| Upgrade impact | Component/run-state/history impact and measured duration | TBD |
| Recovery support | Vendor-confirmed version pair, procedure, limitations and rehearsal | TBD |
| Metadata/history | Size evidence where relevant, retention, authorized cleanup, recovery owner | TBD |
| Approval | PL decision, vendor confirmation reference and review date | TBD |

No database cleanup, version change, downgrade or provider update has been executed. Cleanup, if needed, requires the agreed retention policy and vendor procedure. This source review cannot establish platform-specific eligibility without deployment evidence.

## Source register

| ID | Official source | Use in this draft |
|---|---|---|
| S01 | [Apache: Upgrading to Airflow 3](https://airflow.apache.org/docs/apache-airflow/stable/installation/upgrading_to_airflow3.html) | Upstream prerequisites and compatibility checklist |
| S02 | [Apache: Public interface](https://airflow.apache.org/docs/apache-airflow/stable/public-airflow-interface.html) | Supported extension and task-authoring boundaries |
| S03 | [Astronomer: Upgrade an Astro project to Airflow 3](https://www.astronomer.io/docs/astro/airflow3/upgrade-af3) | Hosted Astro migration eligibility and paths |
| S04 | [Astronomer: Deploy history](https://www.astronomer.io/docs/astro/deploy-history) | Recovery scope and limitations |
| S05 | [Astronomer: Runtime lifecycle](https://www.astronomer.io/docs/runtime/runtime-version-lifecycle-policy) | Support and version-selection checks |
| S06 | [Astronomer: Runtime upgrade](https://www.astronomer.io/docs/runtime/upgrade-astro-runtime) | Distinction between same-major and major-version upgrade guidance |

Project-context statements are sourced from PROJECT-CONTEXT.md, which summarizes earlier conversations and subsequent user clarification. The initiative-overview photograph supplied on 6 October was reviewed; its extraction and provenance are in `work/initiative-slide-extraction.md`. Other original attachments and platform exports were not reviewed. Proposed planning controls in the other documents are recommendations, not claims that the vendor requires this particular project-management structure.
