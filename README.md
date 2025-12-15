# IBM Tutorials MCP Server

A Model Context Protocol (MCP) server that provides access to IBM's tutorial collection through a searchable interface. This server enables AI assistants and other MCP clients to discover and recommend IBM tutorials on various topics including AI, cloud, containers, databases, and more.

## Features

- **Search IBM Tutorials**: Search through IBM's comprehensive tutorial library
- **Detailed Results**: Get tutorial titles, URLs, publication dates, and authors
- **Real-time Data**: Fetches the latest tutorials from IBM's GitHub repository
- **Easy Integration**: Works with any MCP-compatible client (Claude Desktop, VS Code Copilot, etc.)

## Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Setup

1. Clone or download this repository:
```bash
git clone <your-repo-url>
cd ibmtutorialmcpserver
```

2. Install dependencies:
```bash
pip install fastmcp requests
```

Or using a virtual environment (recommended):
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install fastmcp requests
```

## Configuration

### For Claude Desktop

Add the following to your Claude Desktop MCP configuration file:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "ibm-tutorials": {
      "command": "fastmcp",
      "args": ["run", "/absolute/path/to/ibmtutorialmcpserver/server.py"]
    }
  }
}
```

### For VS Code Copilot

Create or update `.vscode/mcp.json` in your workspace:

```json
{
  "servers": {
    "ibm-tutorials": {
      "type": "stdio",
      "command": "fastmcp",
      "args": [
        "run",
        "/absolute/path/to/ibmtutorialmcpserver/server.py"
      ],
      "env": {}
    }
  }
}
```

**Important**: Replace `/absolute/path/to/ibmtutorialmcpserver/server.py` with the actual absolute path to your server.py file.

## Usage

### Available Tools

#### `search_ibmtutorials`

Searches IBM's tutorial collection for relevant content.

**Parameters:**
- `query` (string): The search term to look for in tutorial titles and URLs

**Returns:**
- Formatted list of matching tutorials with title, URL, date, and author information

### Example Queries

When using with an MCP client, you can ask questions like:

- "What IBM tutorials are available about Kubernetes?"
- "Find IBM tutorials on machine learning"
- "Search for IBM cloud deployment tutorials"
- "Show me IBM tutorials about time series"
- "What are the latest IBM AI tutorials?"

### Example Response

```
Found 2 tutorial(s) matching 'time series':

1. **In this tutorial, we'll use the Lag-Llama model...**
   URL: https://ibm.github.io/ibmdotcom-tutorials/tutorials/generative-ai/time-series-forecasting-lag-llama
   Date: 2025-06-09

2. **Using the watsonx.ai Time Series Forecasting API to predict energy demand**
   URL: https://ibm.github.io/ibmdotcom-tutorials/tutorials/generative-ai/time-series-forecasting-api
   Date: 2025-05-22
   Author: Aleksandra Kłeczek and Meredith Syed
```

## Testing

You can test the server directly using the fastmcp command:

```bash
fastmcp run server.py
```

Or run it as a Python script:

```bash
python3 server.py
```

## How It Works

The server:
1. Fetches the latest tutorial index from IBM's GitHub repository
2. Searches through tutorial titles and URLs for your query term
3. Returns formatted results with all relevant details

**Data Source**: [IBM Tutorials Repository](https://github.com/IBM/ibmdotcom-tutorials)

## Troubleshooting

### Server won't start
- Ensure all dependencies are installed: `pip install fastmcp requests`
- Check that the path to server.py in your MCP configuration is absolute and correct
- Verify Python 3.7+ is installed: `python3 --version`

### No results found
- Try broader search terms (e.g., "AI" instead of "artificial intelligence")
- The search is case-insensitive and looks in both titles and URLs
- Check that you have internet connectivity (server fetches data from GitHub)

### MCP client doesn't recognize the tool
- Restart your MCP client after configuration changes
- Verify the JSON configuration syntax is valid
- Check MCP client logs for connection errors

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This MCP server is provided as-is for educational and development purposes.

## Related Links

- [IBM Tutorials on GitHub](https://github.com/IBM/ibmdotcom-tutorials)
- [Model Context Protocol Documentation](https://modelcontextprotocol.io)
- [FastMCP Framework](https://github.com/jlowin/fastmcp)

---

**Note**: This is an unofficial tool that queries public IBM tutorial data. It is not affiliated with or endorsed by IBM Corporation.