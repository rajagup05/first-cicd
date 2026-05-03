
## timeouts

Hitting a timeout in Google Cloud Build is common, especially with large Docker images or complex deployments. By default, Cloud Build has a 10-minute timeout for many operations (like App Engine deployments), but the overall build default is 60 minutes. You can extend this up to a maximum of 24 hours.

### Increase Timeout in cloudbuild.yaml

You can set a global timeout for the entire build or specific timeouts for individual steps.

```
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/my-project/my-image', '.']
  timeout: '1200s'  # Specific timeout for this step (20 mins)

# Global timeout for the entire build
timeout: '3600s'   # 1 hour
```
