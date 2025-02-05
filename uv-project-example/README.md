# UV Project Example

This repo serves as a walkthrough to setting up a new UV project (it is also possible to convert an existing Python project to a UV project, with some command modifications).

## Initialization

To create a new UV project, you can either run `uv init` inside of an existing dir, or `uv init <new_dir>` to create a new dir and initialize a new project inside of it. Additionally, there are a few important flags you can pass to specify certain things about the project you're creating.

The command used for this repo was:

```sh
uv init --app --python 3.12
```

Passing the `--app` flag tells `uv` that we want to create an application with a proper entrypoint.

This creates the basic starting layout of a `uv` project. The next step is to run any `uv` command so that it auto-generates the `uv.lock` file as well as the `.venv` subdir.

```sh
uv run hello.py
```

## Adding Dependencies

`uv` is able to handle very fine-grained dependency management and version-pinning. This means that the optimal way to add new dependencies is with the `uv add` command.

```sh
uv add requests
```

Running this command updates the `pyproject.toml` file as well as updating the `uv.lock` file with extremely fine-grained dependency metadata. This is a cross-platform file used to create completely reproducible environments.
