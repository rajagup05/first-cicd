
## additional configuration options


## waitFor

In Google Cloud Build, the waitFor field is the primary tool used to customize the execution order of your build steps. By default, steps run sequentially in the order they appear in your cloudbuild.yaml file. Using waitFor allows you to run steps in parallel or create complex dependency chains.

## Core Mechanics

- `id`: You must first assign a unique ID to a step so other steps can refer to it.
- `waitFor`: This field takes a list of step IDs. The current step will not start until all specified steps have completed successfully.

## Common Patterns
### 1. Running Steps in Parallel

To make a step start immediately when the build begins (instead of waiting for the previous step), use the special character "-".

```
steps:
- name: 'gcr.io/cloud-builders/npm'
  args: ['install']
  id: 'install'

- name: 'gcr.io/cloud-builders/npm'
  args: ['run', 'lint']
  id: 'lint'
  waitFor: ['-'] # Starts immediately, doesn't wait for 'install'

- name: 'gcr.io/cloud-builders/npm'
  args: ['run', 'test']
  id: 'test'
  waitFor: ['-'] # Also starts immediately
```

### 2. Creating a "Fan-In" (Dependency Junction)

If you have a step that depends on multiple parallel steps finishing first, list all their IDs in the waitFor array.

```
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/my-project/image', '.']
  waitFor: ['lint', 'test'] # Only runs once both lint and test succeed
```



















