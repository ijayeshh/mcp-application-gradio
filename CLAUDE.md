# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the app

```powershell
# Activate the virtual environment first
.\venv\Scripts\Activate.ps1

# Run the app (starts both Gradio UI and MCP server)
python app.py
```

The app launches at `http://localhost:7860` by default. Passing `mcp_server=True` to `demo.launch()` also exposes an MCP-compatible endpoint alongside the Gradio UI.

## Architecture

This is a single-file Gradio app (`app.py`) that doubles as an MCP server:

- **`sentiment_analysis(text)`** — the core tool function; wraps TextBlob and returns a JSON string with `polarity` (−1 to 1), `subjectivity` (0 to 1), and `assessment` (`positive` / `negative` / `neutral`).
- **`gr.Interface`** — wires the function to a Gradio UI with a textbox in and a textbox out.
- **`demo.launch(mcp_server=True)`** — enables Gradio's built-in MCP server so Claude (or any MCP client) can call `sentiment_analysis` as a tool.

When adding new tools, define them as plain Python functions and register them with `gr.Interface` or `gr.Blocks`; Gradio's MCP integration automatically exposes them.

## Dependencies

Managed in `venv/`. Key packages: `gradio`, `textblob`.

To install from scratch:
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install gradio textblob
```
