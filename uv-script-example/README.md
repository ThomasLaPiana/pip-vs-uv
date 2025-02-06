# `uv` Script Example

This directory provides an example of what creating and running scripts with `uv` looks like.

## Creating a Script

When creating a script using `uv`, `uv` will help you automatically generate a valid script file.

```sh
uv init --script example.py --python 3.12
```

This generates a barebones script that you can start building on top of. You will most likely need some dependencies, so we'll use the following command to update the dependencies required for that script.

```sh
uv add --script example.py 'httpx==0.28.1'
```

Now we can run the script:

```sh
uv run example.py
```

This will automatically create a new virtual env for this script and install the required dependencies (including Python version) and then run the script within that environment.
