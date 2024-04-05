# Python & Poetry Setup Action

A Github Action that will:

- Setup Python and Poetry
- Optionally set up the AWS CDK
- Load the `.venv` directory from cache
- Install the project dependencies (i.e. `poetry install`)
- Print the installed packages version tree

> [!NOTE]  
> - This action will **not** perform a fetch of your project. This must be performed before this action is run
> - When a Python version is not specified in the inputs, it will use the value in the `pyproject.toml` file. By default, Poetry will use `^3.X.X` for dependency versioning. This will often be too broad for most use-cases and you will likely need to set specific version bracketing, for example `>=3.11 <3.12`


## Cache

This action will cache the `.venv` directory for use with later workflow runs. You can disable this by setting the `cache_venv` input to `false`. The cache key is assembled using the python version and a hash of the poetry lock file.

## Inputs

| Input                 | Description                                                                         | Required | Default                           |
| --------------------- | ----------------------------------------------------------------------------------- | -------- | --------------------------------- |
| `python_version`      | The Python version to install                                                       | No       | Version defined in pyproject.toml |
| `project_root`        | The location of the python project root                                             | No       | The root of the project           |
| `install_cdk`         | Install the AWS CDK                                                                 | No       | False                             |
| `cache_venv`          | Load and cache the .venv directory                                                  | No       | True                              |
| `codeartifact_login`  | Log in to CodeArtifact. Defaults to false                                           | No       | False                             |
| `codeartifact_source` | The name of the source in pyproject.toml to log into. Only supports a single source | No       | `code-artifact`                   |

## Example

```yaml
jobs:
  test:
    name: tests
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v3

      - uses: citizensadvice/python-poetry-setup-action@v1

      - name: Pytest
        run: poetry run pytest
```

## Versioning

The `v1` tag will be maintained and updated until there is an interface change.
