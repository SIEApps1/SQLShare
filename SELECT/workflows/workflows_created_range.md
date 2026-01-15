# Workflows: Created Date Range

## ID
workflows_created_range

## Description
Approved query template for internal troubleshooting and support workflows.

## Tags
- read-only
- workflow

## Query Type
SELECT

## Tables Used
- Workflows

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| startDate | date | Yes |  |
| endDate | date | Yes |  |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT
    createDateTime AS [Date Created],
    eid AS [Patient Accession],
    pid AS [MRN],
    MPI AS [MPI],
    patientName AS [Patient Name],
    custom42 AS [Exam],
    modality AS [Modality],
    PtClass AS [Patient Class],
    custom15 AS [Status],
    facility AS [Facility],
    org AS [Organization],
    performingResource AS [Performing Resource]
FROM Workflows
WHERE TRY_CONVERT(datetime, createDateTime, 100) >= {{startDate}}
  AND TRY_CONVERT(datetime, createDateTime, 100) <  {{endDate}};
```
