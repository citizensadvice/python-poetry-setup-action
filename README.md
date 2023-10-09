# Python & Poetry Setup Action

A Github Action that will:

- Setup Python and Poetry
- Optionally set up the AWS CDK
- Load the `.venv` directory from cache
- Install the project dependencies

> [!NOTE]  
> This action will **not** perform a fetch of your project. This must be performed before this action is run

## Cache

This action will cache the `.venv` directory for use with later workflow runs. You can disable this by setting the `cache_venv` input to `false`. The cache key is assembled using the python version and a hash of the poetry lock file.

## Inputs

| Input            | Description                                                | Required | Default                           |
| ---------------- | ---------------------------------------------------------- | -------- | --------------------------------- |
| `python_version` | The Python version to install                              | No       | Version defined in pyproject.toml |
| `project_root`   | The location of the python project root                    | No       | The root of the project           |
| `install_cdk`    | Install the AWS CDK                                        | No       | False                             |
| `cache_venv`     | Cache the .venv directory for use with later workflow runs | No       | True                              |
