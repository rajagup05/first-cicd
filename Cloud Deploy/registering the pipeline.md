
## registering the pipeline

To create your pipeline, you need a definition file that outlines the deployment sequence from staging to prod.

### 1. create pipeline configuration 

```
apiVersion: ://google.com
kind: DeliveryPipeline
metadata:
  name: my-cloud-run-pipeline
description: Main delivery pipeline for Cloud Run services
serialPipeline:
  stages:
    - targetId: staging
    - targetId: prod
```

### 2. run the registeration command

Execute this single gcloud command to register your delivery pipeline. If you have not registered your targets yet, you can include them in the same command.

```
gcloud deploy apply \
  --file=pipeline.yaml \
  --region=YOUR_REGION \
  --project=YOUR_PROJECT_ID
```

### 3. verify the pipeline

Confirm that your pipeline and targets are successfully registered in your project:

```
# List your pipelines
gcloud deploy delivery-pipelines list --region=YOUR_REGION

# Describe your pipeline structure
gcloud deploy delivery-pipelines describe my-cloud-run-pipeline --region=YOUR_REGION
```


















