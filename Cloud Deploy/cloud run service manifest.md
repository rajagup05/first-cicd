

## cloud run service manifests


When using Google Cloud Deploy with Skaffold, Cloud Run services are defined using the Kubernetes-style Knative Service syntax.

### service manifests: 

```
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: my-cloud-run-app
  labels:
    ://amazonaws.com: YOUR_REGION
spec:
  template:
    spec:
      containers:
        - image: gcr.io/YOUR_PROJECT_ID/your-app-image # Skaffold replaces this automatically
          resources:
            limits:
              cpu: "1"
              memory: 512Mi
          ports:
            - containerPort: 8080
```
