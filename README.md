Enables slack notifications for completed builds.  

# Usage

<!-- start usage -->
```yaml
- uses: nrccua/github-action-build-slack-notification@v1.0.0
  with:
    # App name
    # Required: true
    app_name: ''

    # Git branch
    # Required: true
    git_branch: ''

    # Git sha
    # Required: true
    git_sha: ''

    # Deploy url (application url)
    # Required: true
    deploy_url: ''

    # Slack url (webhook url)
    # Required: true
    slack_url: ''
```
<!-- end usage -->

# Example

```yaml
name: Build my amazing app

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        persist-credentials: false
    - run: my_build.sh
    # add this action to the end of a successful build
    - name: call slack action
      uses: nrccua/github-action-build-slack-notification@v1.0.0
      with:
        app_name: ${{github.repository}}
        git_branch: ${{ github.ref }}
        git_sha: ${{ github.sha }} 
        slack_url: "URL TO SLACK WEBHOOK - SHOULD BE AN ORG SECRET"
        deploy_url: "URL TO APPLICATION ENV - SHOULD BE A REPO SECRET"
```