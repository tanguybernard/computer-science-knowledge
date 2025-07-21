# Model Context Protocol

## Course goals

- Overview of MCP (understand what problems MCP solves)
- MCP clients / servers
- Tools (implemented on server ans extends LLM's capabilities)
- REsources (Servers devliver info to clients)
- Prompt (Servers can provide clients with pre-optimized prompt)

https://modelcontextprotocol.io/introduction

## Introducing MCP

MCP is **communication Layer**

MCP Server act as interface for outside service. MCP Servers provide access to data or functionality implemented by outside services.


### MCP server VS Api directly ?

Sure! Here's the summarized GitHub example in English:

---

### ✅ **GitHub Example – Summary (With vs Without MCP):**

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

---

👉 **Bottom line**: MCP saves you from coding and configuring the GitHub API access — everything is ready to use.
