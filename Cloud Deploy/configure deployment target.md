
## configure deployment target


### Target configuration file

Save the following content as `targets.yaml`. This file defines your staging and prod environments as separate Google Cloud Deploy targets.

```
apiVersion: ://google.com
kind: Target
metadata:
  name: staging
description: Staging environment
gke:
  cluster: projects/YOUR_PROJECT_ID/locations/YOUR_REGION/clusters/staging-cluster
---
apiVersion: ://google.com
kind: Target
metadata:
  name: prod
description: Production environment
gke:
  cluster: projects/YOUR_PROJECT_ID/locations/YOUR_REGION/clusters/prod-cluster
# Optional: Requires manual approval before deploying to production
requireApproval: true 
```


### Key steps to Apply

1. **Modify placeholders:** Replace YOUR_PROJECT_ID, YOUR_REGION, and your cluster names in the YAML definition.
2. **Register targets:** Run the following Google Cloud CLI command to create the resources in your project:


```
gcloud deploy apply --file=targets.yaml --region=YOUR_REGION --project=YOUR_PROJECT_ID
```


### Alternative runtimes; 

If you are not deploying to Google Kubernetes Engine (GKE), replace the gke block with your specific runtime:

**Cloud Run:**
```
run:
  location: projects/YOUR_PROJECT_ID/locations/YOUR_REGION
```











