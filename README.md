# SQL Query Repository

This repository contains **approved, auditable SQL query templates and action definitions** used in a HIPAA-regulated environment.  

This library serves as the **single source of truth** for authorized SQL queries and actions.

---

## Purpose

- Provide a controlled, reviewed set of SQL queries  
- Prevent ad-hoc or unapproved SQL usage  
- Support auditing, traceability, and change management  
- Ensure HIPAA-safe access to PHI

---

## Access Model

- **Owners:** Repository administrators and DBAs  
- **Editors:** Approved developers (limited)  
- **Readers:** Auditors and service accounts with read-only access  

The repository is **read-only for general users** and **SQL must not be executed directly** from this library.

---

## Repository Rules (Non-Negotiable)

1. One query or action per Markdown file  
2. SQL structure may not be modified arbitrarily  
3. Queries must include parameter definitions  
4. `SELECT *` is discouraged and must be documented if used  
5. UPDATE / DELETE / INSERT SQL must NOT be exposed in this repository  
6. All changes require DBA review  
7. Version history must remain enabled

---

## Folder Structure

## ```text
/
├── README.md
├── SELECT/
│   ├── demo/
│   ├── exam/
│   ├── patient/
│   ├── users/
│   ├── workflows/
│   └── settings/
│
├── ACTIONS/
│   └── workflow_resubmit_lcs.md
│
└── DEPRECATED/
---
# <Query Title>

## ID
<stable_query_id>

## Description
Plain-English description of what the query does.

## Tags
- read-only
- domain

## Query Type
SELECT | ACTION

## Tables Used
- table_name

## Parameters
| Name | Type | Required | Description |

## Max Rows
<number or N/A>

## PHI Classification
Aggregate | Limited | Row-level PHI

## SQL / Action Definition
## ```sql
-- SQL goes here (SELECT only)

---

## Approval & Change Management

- All changes must be reviewed by a DBA  
- Version history is required  
- Deprecated queries must be moved to `/DEPRECATED`  
- Emergency changes must be documented in commit notes

---

## Audit & Compliance

This repository is designed to support:

- HIPAA audits  
- Change traceability  
- Access reviews  
- Incident investigations  

All usage is logged at the application layer.
