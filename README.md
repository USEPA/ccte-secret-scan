# Trufflehog-Scan Action

This GitHub Action scans your codebase for secrets using [TruffleHog](https://github.com/trufflesecurity/trufflehog). It is designed to be used in your CI/CD pipelines to ensure that no sensitive information is committed to your repositories.

## Features

- Scans your repository for secrets using TruffleHog
- Supports additional TruffleHog arguments
- Configurable fetch depth for repository checkout

## Inputs

| Name         | Description                                 | Required | Default                           |
|--------------|---------------------------------------------|----------|-----------------------------------|
| `fetch_depth`| Depth to fetch repository history           | No       | `0`                               |
| `base_branch`| Base branch for TruffleHog scan             | Yes      |                                   |
| `extra_args` | Additional arguments for TruffleHog         | No       | `--debug --only-verified --json`  |
| `path`       | Path to scan                                | No       | `./`                              |

## Usage

To use this action in your workflow, add the following steps to your job:

```yaml
name: Trufflehog-Scan
on:
  push:
    branches: [ "dev" ]
  pull_request:

jobs:
  trufflehog:
    runs-on: ubuntu-latest
    steps:
    - name: Trufflehog Scan
      uses: your-username/your-action-repo@v1
      with:
        base_branch: ${{ github.event.repository.default_branch }}
