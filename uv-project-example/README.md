# UV Project Example

This repo serves as a walkthrough to setting up a new UV project (it is also possible to convert an existing Python project to a UV project, with some command modifications).

## Initialization

To create a new UV project, you can either run `uv init` inside of an existing dir, or `uv init <new_dir>` to create a new dir and initialize a new project inside of it. Additionally, there are a few important flags you can pass to specify certain things about the project you're creating.

The command used for this repo was:

```sh
uv init --lib --python 3.12
```

Passing the `--lib` flag tells `uv` that we want to create an application with a proper entrypoint. Alternatively you can use `--script` if you will only be working on scripts.

## Adding Dependencies

`uv` is able to handle very fine-grained dependency management and version-pinning. This means that the optimal way to add new dependencies is with the `uv add` command.

```sh
uv add httpx
```

Running this command updates the `pyproject.toml` file as well as creating & updating the `uv.lock` file with extremely fine-grained dependency metadata. This is a cross-platform file used to create completely reproducible environments.

This command also creates the virtual environment in `.venv`.

## Installing Dev Tools

Naturally, we'll want to run dev tools on our code, such as linters and formatters. We also install these using `uv`.

```sh
uv add --dev mypy black
```

The `--dev` flag tells `uv` to include these dev tools only locally, and remove then when building the final package.

We can then run the tools like so:

```sh
uv run mypy src
uv run black src    
```

### REPL-driven Development

To enable REPL-driven development, we can install `IPython` as a dev dependency and import our project directly since they live in the same `uv` project.

```sh
uv add --dev ipython
```

Now we can import and run as usual

```sh
uv run ipython
...
In [1]: from uv_project_example import main

In [2]: main.main()
Hello, World!
```

Using the `autoreload` plugin, you can also test changes to your code in real-time without needing to reload the REPL.
