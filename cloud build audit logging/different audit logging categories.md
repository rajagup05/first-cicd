
## different audit logging categories

The specific audit logging categories for Cloud Build are organized based on the Identity and Access Management (IAM) permission types required to perform an action.

### Cloud Build Audit Categories

- Admin Activity: Tracks "Admin Write" operations that modify resources (e.g., CreateBuild, CreateBuildTrigger, CancelBuild).

- Data Access: Tracks "Data Read/Write" or "Admin Read" operations that interact with user data or configuration metadata.
  - ADMIN_READ: Records metadata reads, such as listing builds or triggers.
  - DATA_READ: Records operations that read user-provided data (e.g., retrieving build logs).
  - DATA_WRITE: Records operations that write user-provided data.
