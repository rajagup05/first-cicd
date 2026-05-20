

## different types of environments


Google Cloud Deploy handles different types of environments by defining them as Targets. A target represents the specific runtime infrastructure where your application will be deployed.

Cloud Deploy natively supports three major types of environments:

1. Google Kubernetes Engine (GKE)
2. Anthos / GKE Enterprise
3. Cloud Run


### Environmental Progression (Stages)

Within your pipeline, you can label and sequence these targets to reflect your standard software development lifecycle (SDLC). Common environment stages include:

- **Development (Dev):** Automated, rapid deployments for immediate testing.
- **Staging / QA:** Used for integration testing, security scanning, and user acceptance testing (UAT).
- **Production (Prod):** The live environment, usually protected by manual approval gates and slower rollout strategies.
