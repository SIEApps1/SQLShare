#Standard Markdown Format

#All query files must follow this structure

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