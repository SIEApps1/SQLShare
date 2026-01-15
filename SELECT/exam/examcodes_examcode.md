# ExamCodes: Find by Exam Code

## ID
examcodes_examcode

## Description
Returns records matching the provided identifier (Exam Code).

## Tags
- read-only
- exam

## Query Type
SELECT

## Tables Used
- examcodes

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| examcode | string | Yes |  |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT top 10 * FROM examcodes WHERE examcode = {{examcode}};
```
