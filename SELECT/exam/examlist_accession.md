# ExamList: Find by Accession

## ID
examlist_accession

## Description
Returns records matching the provided identifier (Accession).

## Tags
- read-only
- exam

## Query Type
SELECT

## Tables Used
- examlist

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| accession | string | Yes | e.g., A12345 |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT * FROM examlist WHERE accession = {{accession}};
```
