
## artifacts with python application

we will set up a build trigger in Google Cloud Build to automate the CI/CD pipeline for a Python application

### Prerequisites: 

You need to have your application code in a file named `hello.py` and a configured pipeline in a `cloudbuild.yaml` file. It's important to note that changes to the application code alone will not trigger the pipeline; you must set up a build trigger.

## Triggers: 

Build Triggers allows Cloud Build to automatically initiate the build process when specific events happen, such as code changes (e.g., a push to a branch, pull request).

## cloud build trigger creation

Cloud Build triggers automate your CI/CD pipeline by starting builds whenever changes are made to your source code. You can create them using the Google Cloud Console, the gcloud CLI, or Infrastructure-as-Code tools like Terraform.

