# Patient: Find by MRN

## ID
patient_mrn

## Description
Returns records matching the provided identifier (MRN).

## Tags
- read-only
- patient

## Query Type
SELECT

## Tables Used
- patient

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| mrn | string | Yes | e.g., 123456 |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT * FROM patient WHERE mrn = {{mrn}};
```
