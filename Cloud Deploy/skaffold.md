
## skaffold 

Here is how to configure a single skaffold.yaml file that handles both your staging and prod deployments using Skaffold profiles.

### skaffold configuration files

Save this content as skaffold.yaml in your root directory. It defines how your application builds and maps specific manifests to your targets.

```
apiVersion: skaffold/v4beta11
kind: Config
metadata:
  name: cloud-deploy-app
build:
  artifacts:
    - image: gcr.io/YOUR_PROJECT_ID/your-app-image
      context: .
      docker:
        dockerfile: Dockerfile
manifests:
  rawYaml:
    - k8s-base/*.yaml
profiles:
  - name: staging
    manifests:
      rawYaml:
        - k8s-base/*.yaml
        - k8s-staging/*.yaml
  - name: prod
    manifests:
      rawYaml:
        - k8s-base/*.yaml
        - k8s-prod/*.yaml
```


### Key configurations

- **build artifacts**: Defines your container image name and the location of your Dockerfile.
- **profiles**: Creates environment-specific flags matching your Cloud Deploy targets.
- **manifests**.rawYaml: Points to your Kubernetes resource files (Deployments, Services).
- **Layering**: Profiles can combine core manifests (k8s-base) with environment overrides (k8s-staging or k8s-prod).










