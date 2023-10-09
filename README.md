# Python & Poetry Setup Action

A Github Action that will:

- Setup Python and Poetry
- Optionally set up the AWS CDK
- Load the `.venv` directory from cache
- Install the project dependencies

> [!NOTE]  
> - This action will **not** perform a fetch of your project. This must be performed before this action is run
> - When a Python version is not specified in the inputs, it will use the value in the `pyproject.toml` file. By default, Poetry will use `^3.X.X` for dependency versioning. This will often be too broad for most use-cases and you will likely need to set spesific version bracketing, for example `>=3.11 <3.12`


## Cache

This action will cache the `.venv` directory for use with later workflow runs. You can disable this by setting the `cache_venv` input to `false`. The cache key is assembled using the python version and a hash of the poetry lock file.

## Inputs

| Input            | Description                                                | Required | Default                           |
| ---------------- | ---------------------------------------------------------- | -------- | --------------------------------- |
| `python_version` | The Python version to install                              | No       | Version defined in pyproject.toml |
| `project_root`   | The location of the python project root                    | No       | The root of the project           |
| `install_cdk`    | Install the AWS CDK                                        | No       | False                             |
| `cache_venv`     | Cache the .venv directory for use with later workflow runs | No       | True                              |

## Example

```yaml
jobs:
  test:
    name: tests
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v3

      - uses: citizensadvice/python-poetry-setup-action@v0

      - name: Pytest
        run: poetry run pytest
```
