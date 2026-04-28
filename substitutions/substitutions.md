
## substitution 

Cloud Build substitutions allow you to use variables in your build configuration that are resolved at build time. 

## pre defined substitutions

Cloud Build provides several built-in substitutions that are automatically resolved during your build execution. These variables are populated regardless of how the build was started (CLI, API, or Trigger): 

`$PROJECT_ID:` The ID of your Google Cloud project. \
`$PROJECT_NUMBER:` The numerical ID of your project. \
`$BUILD_ID:` The unique identifier for the current build. \
`$LOCATION:` The region where your build is being executed.
