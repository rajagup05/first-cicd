
## cloud deploy yaml file for staging and prod

To set up a staging and production environment in Google Cloud Deploy, you need to define two main components: a Delivery Pipeline that outlines the flow and individual Targets that represent your specific environments.

### 1. 1. Delivery Pipeline Configuration

This file (typically clouddeploy.yaml) defines the order of deployment. Use the serialPipeline field to list your stages, ensuring staging comes before production

```
apiVersion: deploy.cloud.google.com/v1
kind: DeliveryPipeline
metadata:
  name: my-app-pipeline
serialPipeline:
  stages:
  - targetId: staging-target
    profiles: [staging] 
  - targetId: prod-target
    profiles: [prod]
```

### 2. Target Definitions:

Targets define where application runs (e.g. cloud run, GKE). Define these with `---` separators.

















