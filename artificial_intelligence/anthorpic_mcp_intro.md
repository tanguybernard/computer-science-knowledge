# Model Context Protocol

## Course goals

- Overview of MCP (understand what problems MCP solves)
- MCP clients / servers
- Tools (implemented on server ans extends LLM's capabilities)
- REsources (Servers devliver info to clients)
- Prompt (Servers can provide clients with pre-optimized prompt)

https://modelcontextprotocol.io/introduction

## Introducing MCP Server

MCP is **communication Layer**

MCP Server act as interface for outside service. MCP Servers provide access to data or functionality implemented by outside services.


### MCP server VS Api directly ?

✅ **GitHub Example – Summary (With vs Without MCP):**

#### 🔧 **Without MCP**:

You have to:

* Write a function like `get_pull_requests(owner, repo)`
* Manually define the JSON schema for the model
* Handle the GitHub API call using `requests` (or similar)
* Connect the function to the model via tool/function calling

#### ⚙️ **With MCP**:

* The `get_pull_requests` tool is **already available**
* The schema is **predefined**
* The MCP server **handles the API call automatically**
* The model can **use it directly** without extra setup

👉 **Bottom line**: MCP saves you from coding and configuring the GitHub API access — everything is ready to use.


## MCP Client

The MCP client serves as the communication bridge between your server and MCP servers. It's your access point to all the tools that an MCP server provides, handling the message exchange and protocol details so your application doesn't have to.

### How It Works


<img width="1920" height="1080" alt="instructor_a46l9irobhg0f5webscixp0bs_public_1749849232_09_-_002_-_MCP_Clients_19 1749849231568" src="https://github.com/user-attachments/assets/7e81837f-6760-4f3d-aa5b-a29e06486034" />


*source: https://anthropic.skilljar.com/introduction-to-model-context-protocol/296690*


## Hands-on with MCP servers

Execute code : uv run main.py

```python
@mcp.tool(
    name="read_doc_contents",
    description="Read the contents of a document and return it as a string.", # Clear parameter descriptions help Claude understand tool usage
)
    if doc_id not in docs:
        raise ValueError(f"Doc with id {doc_id} not found")

    return docs[doc_id]
```

Note : Tool registration happens automatically through decorators




