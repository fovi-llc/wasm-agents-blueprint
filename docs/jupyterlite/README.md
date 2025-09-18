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

2. Build the static site into `docs/jupyterlite/dist`:

   ```bash
   jupyter lite build --config docs/jupyterlite/jupyter_lite_config.json
   ```

   The first build downloads the Pyodide runtime and kernel extensions, so it may take a minute.

3. Serve the site locally (optional):

   ```bash
   jupyter lite serve --config docs/jupyterlite/jupyter_lite_config.json
   ```

   Then open the reported URL and launch the **Lab** application. The WebLLM notebooks live under
   `content/notebooks/`.

Once the site is built you can also host the `docs/jupyterlite/dist` folder on any static file server (including GitHub Pages).
