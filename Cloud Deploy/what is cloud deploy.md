
## what is Cloud Deploy 

Google Cloud Deploy is a fully managed continuous delivery (CD) service that automates the deployment of your applications. It is specifically designed to streamline the rollout process for containerized software across platforms like Google Kubernetes Engine (GKE), Cloud Run, and Anthos.


### Key Capabilities

- **Automated Delivery Pipelines**: It allows you to define a standardized sequence of environments (e.g., Development \(\rightarrow \) Staging \(\rightarrow \) Production) and automate the progression of releases between them.
- **Integrated with Skaffold**: Cloud Deploy uses the open-source CLI tool Skaffold to handle manifest rendering, verification, and custom deployment actions.
- **Safety & Control**: It supports automated rollbacks if a deployment fails, canary deployments, and manual approval gates before pushing to production.


### Cloud Build vs. Cloud Deploy

While both services handle parts of the DevOps lifecycle, they serve different primary functions:

- **Cloud Build**: A flexible, remote script/build runner that compiles your code, runs unit tests, and builds your Docker images. It's used for the Continuous Integration (CI) phase.

- **Cloud Deploy**: Strictly handles the Continuous Delivery (CD) phase. It takes the container images created by Cloud Build and manages how they are rolled out, promoted, and monitored in your target environments. 
