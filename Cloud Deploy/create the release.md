
## create the release

Creating a release in Google Cloud Deploy takes your manifest and Skaffold configuration, builds an immutable release object, and starts an automatic rollout to your first target. You can create this from your terminal using the gcloud CLI or directly through the Google Cloud Console.

### Option 1: Using gcloud CLI

Run the following command in your terminal, replacing the placeholders with your specific configurations:

```
gcloud deploy releases create RELEASE_NAME \
  --delivery-pipeline=PIPELINE_NAME \
  --region=REGION \
  --source=. \
  --images=IMAGE_NAME=IMAGE_URI
```


**FLAGS:** 

- **RELEASE_NAME:** A unique identifier for the release (e.g., rel-v1-0-0). Usually tied to a build number or Git SHA.
- **--delivery-pipeline:** The exact name of your pre-configured Cloud Deploy pipeline.
- **--source:** Points to the directory containing your skaffold.yaml file (use . for your current directory).
- **--images:** Maps the placeholder image name in your manifest file to the actual container image URI hosted in your repository.

### Option 2: Using Google cloud console

1. Go to the Google Cloud Console and navigate to the Cloud Deploy section.
2. Under the Delivery pipelines tab, select the name of your specific delivery pipeline.
3. Click the Create release button at the top of the page.
4. In the Choose a container field, specify the path to your pre-built container image.
5. Fill in your release name and click Create.







































