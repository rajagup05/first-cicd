
## substitution 

Cloud Build substitutions allow you to use variables in your build configuration that are resolved at build time. 

## pre defined substitutions

Cloud Build provides several built-in substitutions that are automatically resolved during your build execution. These variables are populated regardless of how the build was started (CLI, API, or Trigger): 

`$PROJECT_ID:` The ID of your Google Cloud project. \
`$PROJECT_NUMBER:` The numerical ID of your project. \
`$BUILD_ID:` The unique identifier for the current build. \
`$LOCATION:` The region where your build is being executed.

## User-defined substitutions

User-defined substitutions allow you to create custom variables for your build. They make your cloudbuild.yaml files flexible and reusable across different environments or projects.

**📋 Basic Rules**

**Prefix:** Must start with an underscore (e.g., `$_SERVICE_NAME`).
**Characters:** Use only uppercase letters and numbers.
**Format:** Reference them in your YAML using $VARIABLE_NAME or `${VARIABLE_NAME}`.

### 🛠️ How to Define and Use Them

**Set Defaults in cloudbuild.yaml**

Add a substitutions block at the end of your configuration file. These values are used if nothing else is provided.

**yaml**
```
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', '$_REGION-docker.pkg.dev/$PROJECT_ID/$_REPO/$_IMAGE', '.']

substitutions:
    _REGION: 'us-central1'
    _REPO: 'my-apps'
    _IMAGE: 'web-service'
```

## Dynamic substitutions

Dynamic substitutions allow you to use bash-style string manipulation on your variables. This is perfect for things like converting a branch name to lowercase or grabbing a specific part of a version string.

### ⚙️ How to Enable

Add this block to your configuration file/yaml:
```
options:
  dynamicSubstitutions: true
```

