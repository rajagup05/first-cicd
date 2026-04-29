

## create secrets in gcp for Cloud build

To use secrets in Google Cloud Build, you typically follow a three-step process: creating the secret in Secret Manager, authorizing Cloud Build to see it, and referencing it in your configuration file. 

### 1. Create the Secret

You can create a secret via the Google Cloud Console or the command line. 

Google Cloud Console:

- Go to the Secret Manager page.
- Click Create Secret.
- Enter a Name (e.g., MY_API_KEY).
- Enter the Secret value and click Create.

### 2. Grant Permissions to Cloud Build 

Grant the Secret Manager Secret Accessor role to your project's Cloud Build service account ([PROJECT_NUMBER]@://gserviceaccount.com) in the Secret Manager IAM settings so it can read the secret. 

### 3. Reference Secrets in cloudbuild.yaml 

Define the secret in your build configuration file to make it accessible during the build process. 
As Environment Variables (Recommended): Use availableSecrets in cloudbuild.yaml to securely inject the secret into specific steps, referencing it with $$ in args.



To use secrets in a build, you need to define them in the availableSecrets section and then reference them in a specific step.

Here is a template using Secret Manager 

```
steps:
  - name: 'gcr.io/cloud-builders/docker'
    entrypoint: 'bash'
    args:
      - '-c'
      - |
        # Reference the secret using $$
        echo "Using my secret: $$MY_SECRET_DATA"
    secretEnv: ['MY_SECRET_DATA']

# Define which secrets to fetch from Secret Manager
availableSecrets:
  secretManager:
    - versionName: projects/$PROJECT_ID/secrets/MY_API_KEY/versions/latest
      env: 'MY_SECRET_DATA'
```





