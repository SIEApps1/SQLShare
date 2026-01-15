# Users: Find by Login ID

## ID
users_loginid

## Description
Returns records matching the provided identifier (Login ID).

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
| loginid | string | Yes |  |

## Max Rows
N/A

## PHI Classification
Row-level PHI

## SQL / Action Definition
```sql
SELECT * FROM users WHERE loginid = {{loginid}};
```
