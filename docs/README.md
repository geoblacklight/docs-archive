## This repository is for documentation of the [GeoBlacklight](https://geoblacklight.org) application.

### Local Build

1. Clone this repo (or your own fork of it)

    ```
    git clone https://github.com/geoblacklight/docs && cd docs
    ```

2. Create and activate a Python virtual environment with the tool of your choice ([venv](https://docs.python.org/3/library/venv.html), [conda](https://docs.conda.io/projects/conda), etc.). The following example uses `venv`.

    ```
    python3 -m venv env && source env/bin/activate
    ```

    On Windows this will look something like

    ```
    python -m venv env && env\Scripts\activate
    ```

3. Install Python requirements

    ```
    pip install mkdocs==1.4.3
    ```

4. Build and serve the docs for autoreloading while you edit:

    ```
    mkdocs serve
    ```

You can now access the documentation in a browser at `http://localhost:8000`, and the page will be refreshed whenever you change the Markdown content in the `docs` directory. Use `Ctrl+C` to stop the server in the terminal.
