# Users: Create User if Missing (Admin)

## ID
users_upsert_by_loginid

## Description
Admin-only action. Updates a user if it exists (standardizes key fields). If the user does not exist, inserts a new record. Returns the resulting record for verification.

## Tags
- users
- admin
- restricted
- upsert
- maintenance

## Query Type
ACTION

## Tables Used
- dbo.Users

## Parameters
| Name | Type | Required | Description |
|---|---|---:|---|
| loginID | varchar | Yes | Login ID to upsert (unique key) |
| firstName | varchar | Yes | User first name |
| lastName | varchar | Yes | User last name |
| fullName | varchar | Yes | Full display name |
| roles | varchar | Yes | Role string (example: 012) |
| enabled | int | Yes | 1 = enabled, 0 = disabled |
| active | int | Yes | 1 = active, 0 = inactive |

## Max Rows
N/A

## PHI Classification
No PHI

## SQL / Action Definition
```sql
/*
  Users: Upsert by loginID
  - Admin-only ACTION
  - Assumes the connected database is correct (no USE statements)
*/

DECLARE @loginID   VARCHAR(100) = {{loginID}};
DECLARE @firstName VARCHAR(100) = {{firstName}};
DECLARE @lastName  VARCHAR(100) = {{lastName}};
DECLARE @fullName  VARCHAR(200) = {{fullName}};
DECLARE @roles     VARCHAR(50)  = {{roles}};
DECLARE @enabled   INT          = {{enabled}};
DECLARE @active    INT          = {{active}};

DECLARE @ActionTaken VARCHAR(20);

IF EXISTS (SELECT 1 FROM dbo.Users WHERE loginID = @loginID)
BEGIN
  IF EXISTS (
    SELECT 1 FROM dbo.Users
    WHERE loginID = @loginID
      AND ISNULL(firstName,'') = ISNULL(@firstName,'')
      AND ISNULL(lastName,'')  = ISNULL(@lastName,'')
      AND ISNULL(fullName,'')  = ISNULL(@fullName,'')
      AND ISNULL(roles,'')     = ISNULL(@roles,'')
      AND ISNULL(enabled,0)    = ISNULL(@enabled,0)
      AND ISNULL(active,0)     = ISNULL(@active,0)
  )
  BEGIN
    SET @ActionTaken = 'NO_CHANGE';
  END
  ELSE
  BEGIN
    UPDATE dbo.Users
    SET firstName=@firstName,lastName=@lastName,fullName=@fullName,roles=@roles,enabled=@enabled,active=@active
    WHERE loginID=@loginID;

    SET @ActionTaken = 'UPDATED';
  END
END
ELSE
BEGIN
  INSERT INTO dbo.Users (loginID,firstName,lastName,fullName,roles,enabled,active,insertedDt,createdDt,insertedBy,createdBy)
  VALUES (@loginID,@firstName,@lastName,@fullName,@roles,@enabled,@active,GETDATE(),GETDATE(),SYSTEM_USER,SYSTEM_USER);

  SET @ActionTaken = 'INSERTED';
END

SELECT @ActionTaken AS ActionTaken, loginID, firstName, lastName, fullName, roles, enabled, active, createdDt, createdBy
FROM dbo.Users
WHERE loginID = @loginID;




