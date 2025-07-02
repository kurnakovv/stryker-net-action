<div align="center">

# [![S](https://raw.githubusercontent.com/stryker-mutator/stryker-mutator.github.io/6026230eaa82a130950a859e523a703d7f30f291/static/images/stryker-80x80.png)](https://github.com/stryker-mutator/stryker-net)tryker.NET GitHub action <a href="https://github.com/kurnakovv/stryker-net-action"><img src="https://raw.githubusercontent.com/jpb06/jpb06/master/icons/GithubActions-Dark.svg" width="80" /></a>

![Visitors](https://api.visitorbadge.io/api/VisitorHit?user=kurnakovv&repo=stryker-net-action&countColor=%237B1E7A&style=flat)
[![Test with all params](https://github.com/kurnakovv/stryker-net-action/actions/workflows/all-params-test.yml/badge.svg)](https://github.com/kurnakovv/stryker-net-action/actions/workflows/all-params-test.yml)
[![Test with all params disabled](https://github.com/kurnakovv/stryker-net-action/actions/workflows/disable-all-params-test.yml/badge.svg)](https://github.com/kurnakovv/stryker-net-action/actions/workflows/disable-all-params-test.yml)
[![Test without params](https://github.com/kurnakovv/stryker-net-action/actions/workflows/without-params-test.yml/badge.svg)](https://github.com/kurnakovv/stryker-net-action/actions/workflows/without-params-test.yml)

</div>

This is a GitHub action that runs the [Stryker.NET](https://stryker-mutator.io/docs/stryker-net/introduction/) tool

# 🚀 Quick start

Install dotnet-stryker (not required) | [how?](https://stryker-mutator.io/docs/stryker-net/getting-started/#install-in-project)

Add config file via terminal
```
dotnet stryker init --config-file ".config/stryker-config.json"
```

Open `.config/stryker-config.json` file and set minimum parameters
```json
{
    "stryker-config": {
        "reporters": [
            "html",
            "dashboard",
            "progress",
        ],
        "project-info": {
            "name": "github.com/OWNER/YOUR_REPOSITORY_NAME"
        }
    }
}
```

Where `OWNER` is your GitHub name (e.g. `kurnakovv`), and `YOUR_REPOSITORY_NAME` your repository name (e.g. `stryker-net-action`)

Add `.github/workflows/stryker-net.yml` action
```yml
name: Stryker.NET mutation testing

on: [push, pull_request]

jobs:
  stryker_net:
    runs-on: ubuntu-latest
    # permissions.pull-request:write is required to send a report message to a pull request (when send-report-message: "true")
    permissions:
      pull-requests: write
    name: Stryker.NET GitHub action
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: 9.0.x

      - name: Stryker.NET
        uses: ./
        with:
          config-path: ".config/stryker-config.json"
          dashboard-api-key: ${{ secrets.STRYKER_DASHBOARD_API_KEY }}
```
