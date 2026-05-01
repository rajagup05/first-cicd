
## create a scheduled trigger


### 1. Create a Manual Trigger

A scheduled build can only be initiated from a manual trigger.

- Go to the Cloud Build Triggers page.
- Click Create Trigger.Enter a Name and select your Source (repository and branch).
- Under Event, select Manual invocation.
- Select your cloudbuild.yaml or Dockerfile location.
- Click Create.

### 2. Set Up the Schedule

Once the manual trigger exists, you can schedule it directly from the Cloud Build console.

- In the Triggers list, find your manual trigger.
- Click the three-dot menu (⋮) at the right end of its row.
- Select Run on schedule.
- Enable Cloud Scheduler API if prompted.
- Configure the following in the Run trigger on schedule panel:
  - Name: Give the scheduler job a name.
  - Frequency: Use cron syntax (e.g., 0 6 * * * for daily at 6 AM).
  - Service Account: Use the suggested cloud-build-trigger-scheduler account.
- Click Create.
