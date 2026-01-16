# Users: Create User if Missing (Admin)

Admin-only action. Creates a new user in dbo.Users if it does not already exist.

Inputs:
- {{loginID}}, {{firstName}}, {{lastName}}, {{fullName}}, {{roles}}, {{enabled}}, {{active}}

```sql
USE [Primordial];

-- Try UPDATE first (in case user exists but needs standardization)
UPDATE dbo.Users
SET
  firstName   = {{firstName}},
  lastName    = {{lastName}},
  fullName    = {{fullName}},
  roles       = {{roles}},
  enabled     = {{enabled}},
  active      = {{active}}
WHERE loginID = {{loginID}};

-- If no row was updated, INSERT
INSERT INTO dbo.Users
(
  loginID,
  firstName,
  lastName,
  fullName,
  roles,
  enabled,
  active,
  insertedDt,
  createdDt,
  insertedBy,
  createdBy
)
SELECT
  {{loginID}},
  {{firstName}},
  {{lastName}},
  {{fullName}},
  {{roles}},
  {{enabled}},
  {{active}},
  GETDATE(),
  GETDATE(),
  SYSTEM_USER,
  SYSTEM_USER
WHERE NOT EXISTS (
  SELECT 1 FROM dbo.Users WHERE loginID = {{loginID}}
);

-- Return the resulting record for verification
SELECT loginID, firstName, lastName, fullName, roles, enabled, active, createdDt, createdBy
FROM dbo.Users
WHERE loginID = {{loginID}};
