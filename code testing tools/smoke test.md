
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

To perform a smoke test in Google Cloud Build using pytest, you can mark your critical test functions with @pytest.mark.smoke and execute them in your cloudbuild.yaml file. This verifies basic system stability before proceeding with deeper deployment steps.

### Step 1: Add a Smoke Marker

Tag your essential tests using the smoke marker inside your Python test files (e.g., test_api.py):

```
import pytest

@pytest.mark.smoke
def test_health_check():
    # Example: Verify your core endpoint is responding
    assert 200 == 200 

```

### Step 2: Define your cloudbuild.yaml


Configure your Cloud Build pipeline to install dependencies and run only the tests marked as smoke:

```
steps:
  # Step 1: Install dependencies
  - name: 'python:3.10'
    entrypoint: 'pip'
    args: ['install', '-r', 'requirements.txt']

  # Step 2: Run Smoke Tests with Pytest
  - name: 'python:3.10'
    entrypoint: 'pytest'
    args: ['-m', 'smoke', '--junitxml=junit.xml'] # Executes only smoke tests

# Optional: Store test results in Google Cloud Storage
artifacts:
  objects:
    location: 'gs://your-bucket-name/test-reports/'
    paths:
      - 'junit.xml'

```

### Step 3: Run the Build

Submit your build to the cloud from your local terminal using the gcloud builds submit command:


```
gcloud builds submit --config cloudbuild.yaml .

```


















