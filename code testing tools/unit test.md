
## why we use unit test using pytest in cloud build

We use unit testing with pytest in Cloud Build to automatically verify that small, individual parts of code—like functions or methods—behave correctly before they are deployed. This process is a core part of a Continuous Integration (CI) pipeline, ensuring that every code change is validated for logic errors and edge cases early in the development cycle.

## unit test using pytest cloud build

To run unit tests using pytest in Google Cloud Build, you must define specific steps in a cloudbuild.yaml file to install dependencies and execute the test runner.

A standard configuration involves using the official Python image to run these tasks. Each step typically runs in a separate container, so you must ensure dependencies are available to the test runner.

```
steps:
  # 1. Install dependencies
  - name: 'python:3.12'
    id: 'install'
    entrypoint: 'pip'
    args: ['install', '-r', 'requirements.txt', 'pytest', '--user']

  # 2. Run unit tests
  - name: 'python:3.12'
    id: 'test'
    entrypoint: 'python'
    args: ['-m', 'pytest', 'tests/', '--junitxml=results.xml']
```

### Key Implementation Details

- **Dependency Management**: Use the --user flag during pip install to ensure that modules installed in one build step are accessible to subsequent steps.
- **Test Discovery**: Pytest automatically finds files starting with test_ or ending with _test.py.
- **Reporting**: Use the --junitxml flag (e.g., --junitxml=${SHORT_SHA}_test_log.xml) to generate reports that can be saved to Cloud Storage for later analysis.
- **Pipeline Control**: If a pytest step fails (returns a non-zero exit code), Cloud Build will stop the process, preventing faulty code from reaching deployment.












