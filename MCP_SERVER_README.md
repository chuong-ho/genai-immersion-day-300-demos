# PTO MCP Server Setup Guide (HTTP/SSE)

This guide shows you how to use the PTO agent as a FastMCP server served over HTTP with Claude Desktop or other MCP clients.

The server runs at: **http://127.0.0.1:8000**

## 📁 Files

- **`mcp-agent-example.ipynb`** - Jupyter notebook with interactive examples
- **`pto_mcp_server.py`** - Standalone Python script for MCP server

## 🚀 Quick Start

### Option 1: Run Standalone Server

```bash
# Install dependencies first
pip install fastmcp python-dotenv

# Run the server
python pto_mcp_server.py
```

The server will start at: **http://127.0.0.1:8000**

You can test it by visiting the URL in your browser or using curl:
```bash
curl http://127.0.0.1:8000
```

### Option 2: Use Jupyter Notebook

Open `mcp-agent-example.ipynb` and run the cells to:
1. See how the tools work
2. Test them locally
3. Run as a server

## 🔧 Connect to Claude Desktop

### Step 1: Find Your Config File

**Mac:**
```bash
~/Library/Application Support/Claude/claude_desktop_config.json
```

**Windows:**
```
%APPDATA%\Claude\claude_desktop_config.json
```

**Linux:**
```bash
~/.config/Claude/claude_desktop_config.json
```

### Step 2: Edit Config

Add this to your config file:

```json
{
  "mcpServers": {
    "pto-server": {
      "command": "python",
      "args": ["/home/chuongho/working files/cag-example/pto_mcp_server.py"]
    }
  }
}
```

**Important:** Update the path to match your actual file location!

### Step 3: Restart Claude Desktop

Close and reopen Claude Desktop. Your PTO tools will now be available!

## 🛠️ Available Tools

The MCP server exposes 4 tools:

| Tool | Description | If-Else Logic |
|------|-------------|---------------|
| `get_pto_hours` | Returns total PTO hours | None |
| `get_pto_days` | Converts hours to days | None |
| `can_take_full_day` | Checks if ≥8 hours available | `if PTO_HOURS_AVAILABLE >= 8` |
| `can_take_half_day` | Checks if ≥4 hours available | `if PTO_HOURS_AVAILABLE >= 4` |

## 📝 Example Usage

### With Claude Desktop

Once configured, you can ask Claude:
- "How many PTO hours do I have?"
- "Can I take a full day off?"
- "What's my PTO balance in days?"

Claude will automatically use the appropriate tool!

### Direct HTTP Access

You can also test the server directly via HTTP:

```bash
# Check if server is running
curl http://127.0.0.1:8000

# Or visit in your browser
# http://127.0.0.1:8000
```

The server uses **SSE (Server-Sent Events)** transport, which allows MCP clients to connect over HTTP.

## 🔄 How It Compares

### OpenAI Agent (agent-example.ipynb)
- ✅ Direct function calls
- ✅ Integrated AI + tools
- ❌ Tied to OpenAI
- ❌ Less reusable

### FastMCP Server (this file) 
- ✅ Works with any MCP client
- ✅ **HTTP/SSE transport** at 127.0.0.1:8000
- ✅ Separated tools from AI
- ✅ Reusable across apps
- ✅ Standard protocol
- ✅ Network accessible
- ❌ Requires server to be running

## 🎯 When to Use Each

**Use OpenAI Agent when:**
- You want a self-contained solution
- You're only using OpenAI
- You need simple, direct integration

**Use FastMCP Server when:**
- You want to share tools across different AI apps
- You're using Claude Desktop or other MCP clients
- You need HTTP/network access to your tools
- You want to separate tool logic from AI logic
- You need a standardized approach
- You want to test tools via HTTP/curl/browser

## 🐛 Troubleshooting

### Server won't start
- Check Python version (3.8+)
- Install dependencies: `pip install fastmcp python-dotenv`
- Check for syntax errors in `pto_mcp_server.py`

### Claude Desktop doesn't see the tools
- Verify config file path is correct
- Ensure Python path in config is absolute
- Restart Claude Desktop completely
- Check Claude Desktop logs for errors

### Tools return errors
- Verify the server is running at http://127.0.0.1:8000
- Check server logs for exceptions
- Ensure environment variables are loaded correctly

### Can't connect to HTTP server
- Verify server is running: `curl http://127.0.0.1:8000`
- Check if port 8000 is already in use
- Try a different port by modifying the code
- Check firewall settings if accessing from another machine

## 📚 Learn More

- [FastMCP Documentation](https://github.com/jlowin/fastmcp)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Claude Desktop MCP Guide](https://docs.anthropic.com/claude/docs/mcp)

