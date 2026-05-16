
## lint testing in cloud build


To run Flake8 lint testing in Google Cloud Build, define a build step in your cloudbuild.yaml file that installs Flake8 via pip and executes it against your Python codebase.

```
steps:
- name: 'python:3.11-slim'
  id: 'Lint Code with Flake8'
  entrypoint: 'bash'
  args: 
  - '-c'
  - |
    pip install flake8
    flake8 .

```
