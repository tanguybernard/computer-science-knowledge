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

### Code Tools

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


### The server inspector


Node 20 nécessaire

Run :

    uv run -- mcp dev mcp_server.py

On Graphical Interface :

Connect > Tools > List Tools

## Connection with MCP clients

### Execute code

uv run main.py

Try asking: "What is the contents of the report.pdf document?"

Here's what happens behind the scenes:

- Your application uses the client to get available tools
- These tools are sent to Claude along with your question
- Claude decides to use the read_doc_contents tool
- Your application uses the client to execute that tool
- The result is returned to Claude, who then responds to you

The client acts as the bridge between your application logic and the MCP server's functionality, making it easy to integrate powerful tools into your AI workflows.

### Resources

Resources in MCP servers __allow you to expose data to clients__, similar to GET request handlers in a typical HTTP server. They're perfect for scenarios where you need to fetch information rather than perform actions.

There are two types of resources:

#### Direct Resources

Direct resources have static URIs that never change. They're perfect for operations that don't need parameters.

#### Templated Resources

Templated resources include parameters in their URIs. The Python SDK automatically parses these parameters and passes them as keyword arguments to your function.


Resources provide a clean way to expose read-only data from your MCP server, making it easy for clients to fetch information without the complexity of tool calls.


### Defining prompts


#### Why Use Prompts?

Here's the key insight: users can already ask Claude to do most tasks directly. For example, a user could type "reformat the report.pdf in markdown" and get decent results. But they'll get much better results if you provide a thoroughly tested, specialized prompt that handles edge cases and follows best practices.

As the MCP server author, you can spend time crafting, testing, and evaluating prompts that work consistently across different scenarios. Users benefit from this expertise without having to become prompt engineering experts themselves.

#### Key Benefits

- Consistency - Users get reliable results every time
- Expertise - You can encode domain knowledge into prompts
- Reusability - Multiple client applications can use the same prompts
- Maintenance - Update prompts in one place to improve all clients

Prompts work best when they're specialized for your MCP server's domain. A document management server might have prompts for formatting, summarizing, or analyzing documents. A data analysis server might have prompts for generating reports or visualizations.

The goal is to provide prompts that are so well-crafted and tested that users prefer them over writing their own instructions from scratch.


## Questions

You're building an MCP client to connect your application to an MCP server. What are the two main components you need?

An MCP Client class and a Client Session


Your MCP client needs to find out what tools are available from an MCP server. What message type should it send?

ListToolsRequest


You've built an MCP server and want to test if your tools work correctly before connecting to a full application. What's the easiest way to do this?

- Write separate test scripts for each tool
- Test everything manually in the terminal
- Use the built-in MCP Inspector with `mcp dev mcp_server.py`  (yep)
- Connect directly to Claude first


You're building a chat app where users ask Claude about their GitHub data. Without MCP, what's the main problem you'd face?

- GitHub doesn't allow API access
- You'd have to write and maintain all the GitHub tool code yourself (yep)
- Claude can't understand GitHub data
- Users can't ask questions about repositories


You're deciding how to implement a new feature in your MCP server. Users should be able to click a button to trigger a "summarize document" workflow. Which MCP primitive should you use?

- Resources - because you need to fetch document data
- Functions - because it involves processing
- Prompts - because users control when to start the workflow (yep)
- Tools - because the AI needs new capabilities


You're using the Python MCP SDK to create a tool that reads files. What's the easiest way to define this tool?

- Use the @mcp.tool() decorator on a Python function (yep)
- Create a separate configuration file
- Write JSON schemas manually
- Send HTTP requests to register the tool

You want to create a resource that fetches different documents based on their ID, like docs://documents/report.pdf. What type of resource should you use?

- A templated resource with parameters in the URI (yep)
- A tool instead of a resource
- A direct resource with a static URI
- A database query resource

## MCP Review


### Tools: Model-Controlled
Tools are controlled entirely by Claude. The AI model decides when to call these functions, and the results are used directly by Claude to accomplish tasks.

Tools are perfect for giving Claude additional capabilities it can use autonomously. When you ask Claude to "calculate the square root of 3 using JavaScript," it's Claude that decides to use a JavaScript execution tool to run the calculation.

### Resources: App-Controlled
Resources are controlled by your application code. Your app decides when to fetch resource data and how to use it - typically for UI elements or to add context to conversations.

In our project, we used resources in two ways:

Fetching data to populate autocomplete options in the UI
Retrieving content to augment prompts with additional context
Think of the "Add from Google Drive" feature in Claude's interface - the application code determines which documents to show and handles injecting their content into the chat context.

### Prompts: User-Controlled
Prompts are triggered by user actions. Users decide when to run these predefined workflows through UI interactions like button clicks, menu selections, or slash commands.

Prompts are ideal for implementing workflows that users can trigger on demand. In Claude's interface, those workflow buttons below the chat input are examples of prompts - predefined, optimized workflows that users can start with a single click.

### Choosing the Right Primitive
Here's a quick decision guide:

- Need to give Claude new capabilities? Use tools
- Need to get data into your app for UI or context? Use resources
- Want to create predefined workflows for users? Use prompts

You can see all three primitives in action in Claude's official interface. The workflow buttons demonstrate prompts, the Google Drive integration shows resources in action, and when Claude executes code or performs calculations, it's using tools behind the scenes.

These are high-level guidelines to help you choose the right primitive for your specific use case. Each serves a different part of your application stack - tools serve the model, resources serve your app, and prompts serve your users.
