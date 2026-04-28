
## secret manager

Google Cloud Secret Manager is a secure, managed storage system for sensitive data like API keys, passwords, and certificates. It provides a central "source of truth" to help you avoid hardcoding credentials in your application code.


## Cloud build file

To use Secret Manager in a Google Cloud Build file (cloudbuild.yaml), you must define the secrets in an availableSecrets block and reference them using secretEnv in the specific build steps that need them 

### 📋 Basic cloudbuild.yaml Template

This example shows how to pull an API key from Secret Manager and use it in a script.

yaml
```
steps:
  # 1. Use the secret in a build step
  - name: 'gcr.io/cloud-builders/gcloud'
    entrypoint: 'bash'
    args:
      - '-c'
      - |
        echo "Using my secret: $$MY_API_KEY"
        # Perform actions with the secret here
    secretEnv: ['MY_API_KEY']

# 2. Define the secrets mapping at the end of the file
availableSecrets:
  secretManager:
  - versionName: projects/$PROJECT_ID/secrets/my-secret-name/versions/latest
    env: 'MY_API_KEY'
```

### 🚀 Common Use Cases

**Passing Secrets to Docker Build**

To pass a secret as a build argument during a Docker build, use this pattern:

yaml
```
steps:
  - name: 'gcr.io/cloud-builders/docker'
    entrypoint: 'bash'
    args:
      - '-c'
      - |
        docker build \
          --build-arg="API_KEY=$$MY_API_KEY" \
          -t gcr.io/$PROJECT_ID/my-image .
    secretEnv: ['MY_API_KEY']

availableSecrets:
  secretManager:
  - versionName: projects/$PROJECT_ID/secrets/my-api-key/versions/latest
    env: 'MY_API_KEY'
```

**Writing a Secret to a File**

If your tool requires a credential file (like .npmrc or a service account key), you can write it to a temporary file: 

yaml
```
steps:
  - name: 'ubuntu'
    entrypoint: 'bash'
    args:
      - '-c'
      - 'echo "$$CONFIG_JSON" > /workspace/config.json'
    secretEnv: ['CONFIG_JSON']
```










