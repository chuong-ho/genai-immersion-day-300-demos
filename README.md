## How to run the demos

Prerequisite:
- Recommended to run these demos in VS Code or Cursor
- Create a virtual environment for python by executing:    `python3 -m venv ./.venv`
- Activate virtual environment:  `source ./.venv/bin.activate`
- Install requirements:      `pip install -r requirements.tx`
- Install jupyter kernal:  `pip install jupyter ipykernel`
- Credentials must be set in .env file or in set in terminal. If you set it in terminal, do not run the load_dotenv() command
- To run the full demo, you will need credentials for AWS, OpenAI, Gemini, and weather.com API keys.

To see demos, run the 

### 00_workflow-example.ipynb
- This is a an example of a verifyer/optimizer workflow. Reponses from OpenAI will be graded by Gemini
- Run cells in order

### 01_agent-example.ipynb
- Example of an agent running in python only
- run cells in order

### 02_strands-sdk-example.ipynb
- Example of an agent that was created using Strands sdk. running on AWS Bedrock
- run cells in order

### 03_strands-sdk-mcp-example.ipynb
- Example of a Strands agent running on bedrock, connecting to two MCP servers. MCP servers are created using FastMCP
- In separate terminal instances, run "python 04_pto_mcp_server.py" and "python 05_weather_mcp.py" to launch the MCP servers. If you don't, calls to the MCP servers will error out
- Run cells in order
