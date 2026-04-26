
## artifacts with python application

we will set up a build trigger in Google Cloud Build to automate the CI/CD pipeline for a Python application

### Prerequisites: 

You need to have your application code in a file named `hello.py` and a configured pipeline in a `cloudbuild.yaml` file. It's important to note that changes to the application code alone will not trigger the pipeline; you must set up a build trigger.

## Triggers: 

Build Triggers allows Cloud Build to automatically initiate the build process when specific events happen, such as code changes (e.g., a push to a branch, pull request).

