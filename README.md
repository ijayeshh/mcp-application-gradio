# mcp-application-gradio

A text sentiment analysis tool built with Gradio and TextBlob, exposed both as an interactive web UI and as an MCP (Model Context Protocol) server — allowing Claude and other MCP clients to call it as a tool.

## Features

- Analyzes text sentiment and returns **polarity**, **subjectivity**, and an **assessment** (positive / negative / neutral)
- Interactive Gradio web interface at `http://localhost:7860`
- Built-in MCP server endpoint for AI assistant integration

## Output format

```json
{
  "polarity": 0.5,       // -1.0 (negative) to 1.0 (positive)
  "subjectivity": 0.6,   // 0.0 (objective) to 1.0 (subjective)
  "assessment": "positive"
}
```

## Setup

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install gradio textblob
```

## Usage

```powershell
python app.py
```

Opens the Gradio UI at `http://localhost:7860` and starts the MCP server on the same process.

## MCP Integration

To use this as an MCP tool in Claude Desktop, add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "sentiment-analysis": {
      "url": "http://localhost:7860/gradio_api/mcp/sse"
    }
  }
}
```
