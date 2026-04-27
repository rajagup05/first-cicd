
# artifacts with python application

we will set up a build trigger in Google Cloud Build to automate the CI/CD pipeline for a Python application

### Prerequisites: 

You need to have your application code in a file named `hello.py` and a configured pipeline in a `cloudbuild.yaml` file. It's important to note that changes to the application code alone will not trigger the pipeline; you must set up a build trigger.

## Triggers: 

Build Triggers allows Cloud Build to automatically initiate the build process when specific events happen, such as code changes (e.g., a push to a branch, pull request).

## cloud build trigger creation

Cloud Build triggers automate your CI/CD pipeline by starting builds whenever changes are made to your source code. You can create them using the Google Cloud Console, the gcloud CLI, or Infrastructure-as-Code tools like Terraform.

## 🏗️ How to Create a Trigger (Console)

**Open the Triggers page:** Go to the Cloud Build Triggers page in the Google Cloud console.

**Connect a Repository:** If you haven't already, click Connect Repository. Select your source (GitHub, Bitbucket, or Cloud Source Repositories) and authenticate.

**Click Create Trigger:** Provide a descriptive name and select the region.

**Choose the Event:** Select what action should fire the trigger:
- **Push to a branch:** Starts a build on any commit to a specific branch (e.g., main).
- **Push new tag:** Fires when a Git tag is created.
- **Pull request:** Runs tests when a PR is opened or updated.
- **Manual invocation:** Only runs when you manually click "Run".

**Set the Source:** Pick the repository and the branch/tag regex pattern (e.g., `^main$` for the main branch).

**Select Build Configuration:**
- **Autodetect**: Looks for cloudbuild.yaml or a Dockerfile at the root.
- **Cloud Build configuration file**: Path to your specific .yaml or .json file.
- **Dockerfile**: Builds a container image directly from a Dockerfile.

**Save:** Click Create. 
