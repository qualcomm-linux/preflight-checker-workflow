# Preflight Checkers Workflow

This workflow utilizes a reusable workflow to run a series of preflight checks on your code. The checks include:

* **[Repolinter](https://github.com/qualcomm-linux/qli-actions)**: Checks the repository for consistency and adherence to coding standards.
* **[Semgrep](https://github.com/qualcomm-linux/qli-actions)**: Runs a static analysis tool to detect potential security vulnerabilities and coding errors.
* **[Copyright-License-Detector](https://github.com/qualcomm/copyright-license-checker-action)**: Checks for proper copyright and licensing information in the code.
* **[PR-Check-Emails](https://github.com/qualcomm/commit-emails-check-action)**: Verifies that the commit emails are properly formatted.

Reusable workflow is available at: [multi-checker-pipeline](https://github.com/qualcomm-linux/multi-checker-pipeline/blob/main/.github/workflows/checker.yml)

## Usage
```
name: preflight-checkers 
on:
  pull_request:
    branches: ["main", "master"]
  push:
    branches: ["main", "master"]
  workflow_dispatch:

jobs:
  checker:
    uses: qualcomm-linux/multi-checker-pipeline/.github/workflows/checker.yml@main
    with:
        repolinter: true # default: false
        semgrep: true # default: false
        copyright-license-detector: true # default: false
        pr-check-emails: true # default: false

    secrets:
      SEMGREP_APP_TOKEN: ${{ secrets.SEMGREP_APP_TOKEN }}
```

## Configuration
The workflow can be configured by passing the following inputs:

* **repolinter**: Enables or disables the Repolinter check. **__Default: false__**
* **semgrep**: Enables or disables the Semgrep check. **__Default: false__**
* **copyright-license-detector**: Enables or disables the Copyright-License-Detector check. **__Default: false__**
* **pr-check-emails**: Enables or disables the PR-Check-Emails check. **__Default: false__**

## Secrets
The workflow requires the following secret to be set:

**SEMGREP_APP_TOKEN**: The Semgrep app token.

## EVENTS
The workflow is triggered on the following events:

* **pull_request**: Triggered when a pull request is opened or updated.
* **push**: Triggered when code is pushed to the repository.
* **workflow_dispatch**: Triggered when the workflow is manually dispatched.