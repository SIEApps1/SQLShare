# AI SQL Query Repository

This repository contains **approved, auditable SQL query templates and action definitions**
used by internal AI-powered applications in a HIPAA-regulated environment.

This library is the **single source of truth** for what SQL the AI assistant is allowed to reference.

---

## Purpose

- Provide a controlled, reviewed set of SQL queries
- Prevent AI-generated or ad-hoc SQL
- Support auditing, traceability, and change management
- Ensure HIPAA-safe access to PHI

---

## Access Model

- **Owners:** Repository administrators and DBAs
- **Editors:** Approved developers (limited)
- **Readers:** AI service accounts and auditors
- **AI assistants:** Read-only reference only

The AI assistant **cannot write to this library** and **cannot execute SQL directly**.

---

## Repository Rules (Non-Negotiable)

1. One query or action per Markdown file
2. SQL structure may not be modified by AI
3. Queries must include parameter definitions
4. `SELECT *` is discouraged and must be documented if used
5. UPDATE / DELETE / INSERT SQL must NOT be exposed to AI
6. All changes require DBA review
7. Version history must remain enabled

---

## Folder Structure

```text
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
```

# Standard Markdown Format

# All query files must follow this structure

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
```sql
-- SQL goes here (SELECT only)
```

---

## Approval & Change Management

- All changes must be reviewed by a DBA
- Version history is required
- Deprecated queries must be moved to `/DEPRECATED`
- Emergency changes must be documented in commit notes

---

## AI Usage Contract

The AI assistant may:
- Select an existing query by ID
- Supply parameters
- Explain results

The AI assistant may NOT:
- Invent new SQL
- Modify SQL structure
- Execute updates directly
- Bypass approval rules

Violations must be reported immediately.

---

## Audit & Compliance

This repository is designed to support:
- HIPAA audits
- Change traceability
- Access reviews
- Incident investigations

All usage is logged at the application layer.
