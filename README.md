# powershell-devops/install-module

[![PowerShellGallery](https://img.shields.io/powershellgallery/dt/powershell-devops.svg)](https://www.powershellgallery.com/packages/powershell-devops)

A PowerShell module for dealing with commands in Azure DevOps Pipelines and GitHub Workflows.

## GitHub Action

See [action.yml](action.yml) for a detailed list of inputs.

Basic:

```yml
steps:
- uses: powershell-devops/install-module@v1
```

Specific version:

```yml
steps:
- uses: powershell-devops/install-module@v1
  with:
    required-version: 1.0.0
```

Minimum version:

```yml
steps:
- uses: powershell-devops/install-module@v1
  with:
    minimum-version: 1.0.0
```

Maximum version:

```yml
steps:
- uses: powershell-devops/install-module@v1
  with:
    maximum-version: 1.0.0
```

## Commands

### Set-EnvironmentVariable

Sets the environment variable for the current process and optionally marks it as a secret.

```powershell
set-env MY_VALUE 'Hello World!'
```

*Note: `set-env` is an alias for `Set-EnvironmentVariable`.*

### Get-EnvironmentVariable

Gets the environment variable for the current process and optionally throws an error if it is not defined.

```powershell
get-env MY_ENV_VALUE -Require
```

*Note: `get-env` is an alias for `Get-EnvironmentVariable`.*

### Add-Path

Prepends the value to the PATH environment.

```powershell
Add-Path $PSScriptRoot
```

### Enter-Group / Exit-Group

Creates an expandable group in the log. Anything you print to the log between the `Enter-Group` and `Exit-Group` commands is nested inside an expandable entry in the log.

```powershell
Enter-Group 'My group'
try {
    # .. some other commands ...
} finally {
    Exit-Group
}
```

### Utility functions

These functions are helper functions that are used by the module but could also be useful within your script.

#### Test-AdoPipeline

Returns true if running in an Azure DevOps Pipeline, determined by the environment variable `TF_BUILD` having a value.

```powershell
Test-AdoPipeline
```

#### Test-GitHubWorkflow

Returns true if running in a GitHub Workflow, determined by the environment variable `GITHUB_ACTIONS` having a value.

```powershell
Test-GitHubWorkflow
```
