# Resubmit Errors to ACR (LCS) — Clear Error Flags

## ID
workflow_resubmit_lcs

## Description
Clears ACR error flags for Workflow 14 to allow resubmission, either for a single accession or for all items matching an error message.

## Tags
- LCS
- Innovation
- ACR
- Resubmit
- Workflow14
- Maintenance

## Query Type
ACTION

## Tables Used
- Workflows

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| Accession | varchar | No | Leave blank to use Error Message |
| ErrorMessage | varchar | No | Used when Accession is blank |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
/*
*Resubmit to Errors to the ACR
*
* This script allows you to resubmit messages to the ACR after they've errored out.
* Works on both Innovation LCS and GA LCS
*
* Script version 1.0
* Last Modified 2020/12/5
*
*  Workflow |   LCS   |    FM    |  Innovation
*           |    X    |          |       X
****************************************************************************************/

DECLARE @Accession VARCHAR(100), @ErrorMessage VARCHAR(MAX)

/* Accession: set to resubmit a single accession */
SET @Accession = {{Accession}}

/* Error message: used when accession is blank */
SET @ErrorMessage = {{ErrorMessage}}

IF (@Accession IS NOT NULL AND @Accession <> '')
BEGIN
  UPDATE Workflows SET
    customDate9 = NULL,
    customDate10 = NULL,
    customDate11 = NULL,
    custom54 = NULL,
    custom55 = NULL
  WHERE eid = @Accession
    AND wdefid = '14'
END
ELSE
BEGIN
  UPDATE Workflows SET
    customDate9 = NULL,
    customDate10 = NULL,
    customDate11 = NULL,
    custom54 = NULL,
    custom55 = NULL
  WHERE eid IN (
    SELECT eid FROM Workflows
    WHERE custom55 = @ErrorMessage
      AND wdefid = '14'
  )
END
```
