
## defaultLogBucketBehavior field

The `defaultLogBucketBehavior` field in Cloud Build determines where build logs are stored when no custom logs bucket is specified. 

By default, Cloud Build automatically manages log storage if you do not specify a custom location. Here is the behavior for log buckets as of May 2026:

**Default Log Bucket Behavior**

- **Automatic Creation:** If no logsBucket is specified in the build config, Cloud Build automatically creates a Google Cloud Storage bucket in your project to store logs.
- **Naming Convention:** The default bucket is typically named [PROJECT_ID]_cloudbuild or follows a similar regionalized pattern (e.g., gcf-v2-logs-[PROJECT_ID]-[REGION]).
- **Location:** The bucket is located in the same region as the build.


