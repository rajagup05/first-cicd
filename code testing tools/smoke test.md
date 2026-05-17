
## smoke test using pytest

Running smoke tests using pytest in Cloud Build provides immediate, automated validation that your latest application build and cloud deployment have successfully initialized. It acts as a rapid "health check" to catch fatal configuration or startup errors, ensuring that only stable builds move forward in the CI/CD pipeline.

### How it looks in a Cloud Build Pipeline:

```
steps:
  # ... Your build and deployment steps ...

  # Run Smoke Tests
  - name: 'python:3.11'
    entrypoint: 'bash'
    args: 
      - '-c'
      - |
        pip install -r requirements-test.txt
        pytest -m smoke --url=https://run.app

```
