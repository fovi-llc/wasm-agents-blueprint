# JupyterLite WebLLM Notebooks

This directory hosts the assets that build the in-browser JupyterLite experience for the WASM Agents Blueprint. The notebooks
show how to launch a WebLLM worker and call the OpenAI-compatible API asynchronously from Python and JavaScript kernels.

## Contents

- `jupyter_lite_config.json` — build configuration that tells `jupyter lite` where to find the notebooks and where to emit the
  static site.
- `content/notebooks/webllm-python.ipynb` — Pyodide notebook that awaits WebLLM chat completions from Python.
- `content/notebooks/webllm-javascript.ipynb` — JavaScript notebook demonstrating both standard and streaming chat calls.

## Building the JupyterLite Site

1. Install the optional dependencies:

   ```bash
   pip install .[lite]
   ```

   This will install JupyterLite along with the Pyodide and JavaScript kernels.

2. Build the static site into `docs/jupyterlite/dist`:

   ```bash
   cd docs/jupyterlite
   jupyter lite build
   ```

   The first build downloads the Pyodide runtime and kernel extensions, so it may take a minute.

   **Troubleshooting missing kernels:**
   
   If no kernels appear, try these steps:
   
   1. Check that kernel extensions are installed:
      ```bash
      jupyter lite list
      ```
   
   2. Build with verbose output to see what's happening:
      ```bash
      jupyter lite build --debug
      ```

   3. Try building without the config file to use defaults:
      ```bash
      cd docs/jupyterlite && jupyter lite build
      ```

   **Note:**  
   If you do not see both the Python (Pyodide) and JavaScript kernels in the JupyterLite interface, ensure the following:
   - The `jupyterlite-pyodide-kernel` and `jupyterlite-javascript-kernel` packages are installed (see `pyproject.toml`).
   - Your `jupyter_lite_config.json` does not explicitly disable these kernels.
   - Try running `pip install --force-reinstall .[lite]` to ensure all extensions are present.

3. Serve the site locally (optional):

   ```bash
   cd docs/jupyterlite
   jupyter lite serve
   ```

   Then open the reported URL and launch the **Lab** application. The WebLLM notebooks live under
   `content/notebooks/`.

Once the site is built you can also host the `docs/jupyterlite/dist` folder on any static file server (including GitHub Pages).
