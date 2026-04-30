
## cloud build push image to dockerhub

To push a Docker image to Docker Hub using Google Cloud Build, you must first store your Docker Hub credentials in Secret Manager and then reference them in your cloudbuild.yaml file. 

### 1. Store Credentials in Secret Manager

Store your Docker Hub username and Access Token (recommended over a password) in Secret Manager: 

- Secret 1: docker-username (Value: your Docker Hub username)
- Secret 2: docker-password (Value: your Docker Hub token) 

Ensure the Cloud Build Service Account has the Secret Manager Secret Accessor role (roles/secretmanager.secretAccessor) for these secrets. 
