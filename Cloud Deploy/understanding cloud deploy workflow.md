

## understanding cloud deploy workflow

A cloud deployment workflow is the automated, repeatable pipeline used to promote application code from source control into live cloud infrastructure. It typically follows a structured CI/CD model (Continuous Integration/Continuous Deployment) that builds, tests, and safely deploys containerized applications or serverless functions to production.


### 1. The Continous Integration phase (CI):

- **Source Control:** Developers commit application code and deployment configurations (like Dockerfiles) to repositories.
- **Build & Package:** Tools like Google Cloud Build automatically trigger, compile the code, and package it into a container image.
- **Registry:** The built container image is pushed and secured in an image repository, such as the Google Cloud Artifact Registry.
- **Testing & Scanning:** Automated unit tests and security vulnerability scans run on the container to ensure it is safe for release.

### 2. The Continous Delivery phase (CD): 

- **Release Creation:** A "release" is created (often using services like Google Cloud Deploy), which fetches the specific container image from the registry.
- **Pipeline Promotion:** The release is promoted through a sequence of pre-defined environments in a specific order (e.g., \(Dev\rightarrow Staging\rightarrow Production\)).
- **Strategies:** Deployment tools often utilize different release strategies to prevent downtime:
  - **Rolling Deployments:** Gradually update instances to minimize impact.
  - **Canary Deployments:** Send a small percentage of user traffic to the new version first.
- **Verification & Approval:** Before moving to production, automated verification tests run, and manual approvals can be programmed into the pipeline.

### Execution and Infrastructure platform: 

- The final stage of the workflow applies the release to your chosen compute platform:
  - **Serverless Execution:** Deploying to platforms like Google Cloud Run automatically provisions and scales serverless containers.
  - **Container Orchestration:** Deploying to platforms like Google Kubernetes Engine (GKE) using manifest tools like Skaffold or Helm.










