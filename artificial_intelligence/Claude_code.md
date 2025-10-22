
# Claude Code - Anthropic Course, October 2025

## Coding Assistant


<img width="1280" height="720" alt="instructor_a46l9irobhg0f5webscixp0bs_public_1750967940_002_-_What_is_a_Coding_Assistant__02 1750967940100" src="https://github.com/user-attachments/assets/c526f10e-9696-4f14-b5af-a170bbbeda70" />


- Gather Context : For example Read an external File
- Formulate a plan: Deciding how to solve the issue
- Take action: Run command, edit a file

LLM is simple : You send Text, you receive text. 

The coding assistant adds instructions to your message that teach the language model how to request actions. 

## Tools with Claude Code (Integration)

- Playwright MCP Server : Set of tools that allow Claude to control a browser (Open browser, take screenshot)
- Github MCP Server: Set of tools that allow Claude to interact with Github (Write summary report, read the changes in the pull request)


## Hands On

## Init

> claude

We can scan project with command **/init**

This tells Claude to analyze your entire codebase and understand:

- The project's purpose and architecture
- Important commands and critical files
- Coding patterns and structure

### The CLAUDE.md File
The CLAUDE.md file serves two main purposes:

- Guides Claude through your codebase, pointing out important commands, architecture, and coding style
- Allows you to give Claude specific or custom directions
  
This file gets included in every request you make to Claude, so it's like having a persistent system prompt for your project.

### Adding Custom Instructions


Use the # command to enter "memory mode" - this lets you edit your CLAUDE.md files intelligently.

For example:

    # Use comments sparingly. Only comment complex code.


### File Mentions with '@'

> How does the auth system work ? @src/components/auth/AuthDialog.tsx  


### Use Planning vs Thinking Mode

These two features handle different types of complexity:

Planning Mode is best for:

- Tasks requiring broad understanding of your codebase
- Multi-step implementations
- Changes that affect multiple files or components

Thinking Mode is best for:

- Complex logic problems
- Debugging difficult issues
- Algorithmic challenges
  
You can combine both modes for tasks that require both breadth and depth. Just keep in mind that both features consume additional tokens, so there's a cost consideration for using them.

## Controlling context

//TO CONTINUE


