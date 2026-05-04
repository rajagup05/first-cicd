
## store and manage logs in bucket

### 1. Cloud Storage Buckets (Archiving)

Ideal for low-cost, long-term retention or if you need to use third-party tools like Splunk or Datadog.

**How to Configure for Cloud Build**

You can point Cloud Build logs directly to a GCS bucket in your cloudbuild.yaml file:

```
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/my-project/my-image', '.']
options:
  logsBucket: 'gs://your-unique-bucket-name'
  logging: GCS_ONLY
```

- Setup: Create a bucket with Uniform bucket-level access enabled.
- Permissions: Ensure the Cloud Build service account has the Storage Admin (roles/storage.admin) or Storage Object Creator role on that bucket.
- Management: Use Object Lifecycle Management to automatically move logs to cheaper storage classes (like Coldline or Archive) or delete them after a set period.
