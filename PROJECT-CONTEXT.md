# RHEL to Amazon Linux on AWS migration

This repository is the AWS operating-system migration project. The Airflow 2.x to 3.x planning pack was moved to the dedicated `airflow-migration` repository.

## Scope

The repository contains the working strategy and planning documentation for the RHEL-to-Amazon-Linux migration. Airflow and AWS migration remain separate projects; shared staffing and reporting are coordination concerns only.

## AWS planning pack

- AWS roadmap: `outputs/MIGRATION-ROADMAP.md`
- AWS registers: `outputs/MIGRATION-REGISTERS.md`
- AWS server inventory draft: `outputs/SERVER-INVENTORY-DRAFT.md`
- AWS discovery and access plan: `outputs/DISCOVERY-ACTION-PLAN.md`
- AWS S02 RAID/status register: `outputs/RAID-AND-STATUS-S02.md`
- AWS source extractions: `outputs/SOURCE-S01-INITIATIVE-OVERVIEW.md` and `outputs/SOURCE-S02-CHAT-AND-INVENTORY-EXTRACTION.md`

The AWS work is an application-team planning draft. Central migration/automation teams own AWS provisioning and server migration. Screenshot-derived server rows and historical chat statuses are leads only and require reconciliation with the authoritative Data SRE/ServiceNow export. No AWS migration gate is recorded as accepted in this repository.

## Repository boundary

Airflow migration files, Airflow-specific context, and the post-migration strategy review are maintained in the dedicated Airflow repository. Local intermediate evidence belongs in `work/` and is excluded from the repository deliverables.
