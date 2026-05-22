
## GitHub Actions

GitHub Actions integrates with Google Cloud Platform (GCP) to automate building, testing, and deploying your applications. . The integration primarily relies on official GitHub Actions provided by Google to handle authentication and resource management.


### key integration methods

- **Authentication (Highly Recommended**): Use Workload Identity Federation (WIF) instead of static service account keys. It uses short-lived tokens, which is more secure than storing long-lived JSON keys as GitHub secrets.
- **Official Google Actions:** Use the Google GitHub Actions suite for specific tasks:
  - `auth`: Authenticates to Google Cloud via WIF or service account keys.
  - `setup-gcloud`: Installs and configures the Google Cloud SDK (gcloud).
  - `deploy-cloudrun`: Automates deployments to Cloud Run.
  - `deploy-cloud-functions`: Deploys Google Cloud Functions.
  - `upload-cloud-storage`: Uploads files or build artifacts to Google Cloud Storage.
  - `get-secretmanager-secrets`: Retrieves sensitive data from Secret Manager.
 


### common CI CD workflows:

1. **Deploying to Cloud Run:** The workflow typically checks out code, authenticates, builds a Docker image, pushes it to Artifact Registry, and then deploys the image to Cloud Run.
2. **Infrastructure as Code (Terraform):** You can use GitHub Actions to run terraform plan on a pull request and terraform apply when merging to main to provision GCP resources like VMs or buckets.
3. **Self-Hosted Runners**: If you need specific hardware or a private network, you can run GitHub Actions runners on Google Compute Engine

<!--
**sample code**

```
name: Deploy to Google Cloud Run

on:
  push:
    branches:
      - main

env:
  PROJECT_ID: 'my-gcp-project-id' # 👈 Replace with your GCP Project ID
  GAR_LOCATION: 'us-central1'       # 👈 Replace with your Artifact Registry region
  REPOSITORY: 'my-docker-repo'      # 👈 Replace with your Artifact Registry name
  SERVICE: 'my-cloud-run-service'   # 👈 Replace with your Cloud Run service name
  REGION: 'us-central1'             # 👈 Replace with your Cloud Run region

jobs:
  deploy:
    name: Build and Deploy
    runs-on: ubuntu-latest

    # Required permissions for Workload Identity Federation
    permissions:
      contents: 'read'
      id-token: 'write'

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    # 1. Authenticate with Google Cloud using WIF
    - name: Google Auth
      id: auth
      uses: google-github-actions/auth@v2
      with:
        token_format: 'access_token'
        workload_identity_provider: '${{ secrets.WIF_PROVIDER }}' # 👈 Saved in GitHub Secrets
        service_account: '${{ secrets.WIF_SERVICE_ACCOUNT }}'     # 👈 Saved in GitHub Secrets

    # 2. Login to Artifact Registry
    - name: Docker Auth
      uses: docker/login-action@v3
      with:
        registry: ${{ env.GAR_LOCATION }}-docker.pkg.dev
        username: 'oauth2accesstoken'
        password: ${{ steps.auth.outputs.access_token }}

    # 3. Build and Push Container Image
    - name: Build and Push Container
      run: |-
        IMAGE_TAG="${{ env.GAR_LOCATION }}-docker.pkg.dev/${{ env.PROJECT_ID }}/${{ env.REPOSITORY }}/${{ env.SERVICE }}:${{ github.sha }}"
        docker build -t $IMAGE_TAG .
        docker push $IMAGE_TAG
        echo "IMAGE_TAG=$IMAGE_TAG" >> $GITHUB_ENV

    # 4. Deploy to Google Cloud Run
    - name: Deploy to Cloud Run
      id: deploy
      uses: google-github-actions/deploy-cloudrun@v2
      with:
        service: ${{ env.SERVICE }}
        region: ${{ env.REGION }}
        image: ${{ env.IMAGE_TAG }}

    # 5. Output the URL
    - name: Show URL
      run: echo "Deployed successfully! Service URL is ${{ steps.deploy.outputs.url }}"
```

-->













