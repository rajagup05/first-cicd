

## create secrets in gcp for Cloud build

To use secrets in Google Cloud Build, you typically follow a three-step process: creating the secret in Secret Manager, authorizing Cloud Build to see it, and referencing it in your configuration file. 

### 1. Create the Secret

You can create a secret via the Google Cloud Console or the command line. 

Google Cloud Console:

- Go to the Secret Manager page.
- Click Create Secret.
- Enter a Name (e.g., MY_API_KEY).
- Enter the Secret value and click Create.
