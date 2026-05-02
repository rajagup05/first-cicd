
## additional configuration options


## waitFor

In Google Cloud Build, the waitFor field is the primary tool used to customize the execution order of your build steps. By default, steps run sequentially in the order they appear in your cloudbuild.yaml file. Using waitFor allows you to run steps in parallel or create complex dependency chains.

## Core Mechanics

- `id`: You must first assign a unique ID to a step so other steps can refer to it.
- `waitFor`: This field takes a list of step IDs. The current step will not start until all specified steps have completed successfully.
