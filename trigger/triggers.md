
## trigger

Cloud Build triggers automate CI/CD pipelines by initiating builds in response to events like code pushes, pull requests, or scheduled times. They support repository events (GitHub, Bitbucket, GitLab, Cloud Source Repositories), Pub/Sub messages, and webhook events, allowing for automated testing, container building, and deployment. 

### Key Types of Cloud Build Triggers

- **Repository Event Triggers:** Automate builds upon pushing code, creating tags, or opening/updating pull requests on GitHub, Bitbucket, GitLab, or Cloud Source Repositories.

- **Manual Triggers:** Allow users to manually run a trigger from the Cloud Build Triggers page to start a build on demand.

- **Pub/Sub Triggers:** Initiate builds in response to messages published to a Google Cloud Pub/Sub topic.

- **Webhook Triggers:** Trigger builds using a POST request to a specialized URL, allowing integration with external systems.

- **Scheduled Triggers (via Pub/Sub):** Enable cron-like, time-based builds (e.g., nightly builds) by combining Cloud Scheduler with Pub/Sub.
