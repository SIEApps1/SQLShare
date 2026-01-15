# Users: Find by Provider ID

## ID
users_providerid

## Description
Returns records matching the provided identifier (Provider ID).

## Tags
- read-only
- users

## Query Type
SELECT

## Tables Used
- users

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| providerid | string | Yes |  |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT * FROM users WHERE providerid = {{providerid}};
```
