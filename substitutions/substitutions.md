
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

## run bash scripts in build step

To run bash scripts in a Cloud Build step, you use the script field or the bash entrypoint. Using the script field is the modern, recommended way as it handles multi-line commands cleanly.

### 📝 Option 1: Using the script field (Recommended)

This is the easiest way to write multi-line bash scripts directly in your YAML.

yaml
```
steps:
- name: 'ubuntu' # Or any image with bash installed
  script: |
    #!/bin/bash
    echo "Current directory: $(pwd)"
    if [ "$_ENV" == "prod" ]; then
      echo "Deploying to production..."
    else
      echo "Deploying to staging..."
    fi
```

### 🛠️ Option 2: Using entrypoint and args

Use this if you are using an older version of Cloud Build or prefer the classic structure. You must specify bash as the entrypoint.

yaml
```
steps:
- name: 'gcr.io/cloud-builders/gcloud'
  entrypoint: 'bash'
  args:
  - '-c'
  - |
    echo "Starting cleanup"
    rm -rf ./temp_files
    echo "Done!"
```

### 📂 Option 3: Running an External Script File
If your script is complex, keep it in a .sh file in your repository. Use chmod to ensure it is executable.

yaml
```
steps:
- name: 'ubuntu'
  script: |
    chmod +x ./scripts/deploy.sh
    ./scripts/deploy.sh
```



**Accessing Substitutions**

You can use your variables directly inside the script. Use $$ to escape bash variables so Cloud Build doesn't confuse them with its own substitutions.

yaml
```
steps:
- name: 'ubuntu'
  script: |
    echo "Cloud Build Var: $_MY_VAR"
    export LOCAL_VAR="hello"
    echo "Bash Var: $$LOCAL_VAR" # Use double $$ for bash variables
```

## manual mapping and auto mapping

### 🤖 Automapping

Automapping is the "set it and forget it" method. When enabled, Cloud Build automatically converts all substitutions into environment variables for every step.

**How to enable:
**
yaml
```
options:
  automapSubstitutions: true
```

**How it works:**
- Built-in variables (like $PROJECT_ID) become $PROJECT_ID.
- User-defined variables (like $_SERVICE_NAME) get an additional underscore and become $__SERVICE_NAME.

**Example:**

yaml
```
steps:
- name: 'ubuntu'
  script: echo "Deploying $__SERVICE_NAME to $PROJECT_ID"

substitutions:
  _SERVICE_NAME: 'my-app'

options:
  automapSubstitutions: true
```

## ✍️ Manual Mapping

Manual mapping gives you total control. You explicitly define which variables are passed to which specific step using the env field.

**When to use:**

- You only want certain steps to see specific sensitive data.
- You want to rename the variable (e.g., mapping $_DB_URL to DATABASE_URL).
- You aren't using the automapSubstitutions option.

**Example:**

yaml
```
steps:
- name: 'gcr.io/cloud-builders/docker'
  entrypoint: 'bash'
  args: ['-c', 'echo "Target env is: $TARGET"']
  env:
  - 'TARGET=$_ENV' # Manually mapping _ENV to TARGET

substitutions:
  _ENV: 'staging'
```




