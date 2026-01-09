# Claude 101


## What is AI Fluency?


### 4D Framework for AI Fluency

- Delegation: Deciding on what work should be done by humans, what work should be done by AI, and how to distribute tasks between them. Includes understanding your goals, AI capabilities, and making strategic choices about collaboration.
- Description: Effectively communicating with AI systems. Includes clearly defining outputs, guiding AI processes, and specifying desired AI behaviors and interactions.
- Discernment: Thoughtfully and critically evaluating AI outputs, processes, behaviors and interactions. Includes assessing quality, accuracy, appropriateness, and determining areas for improvement.
- Diligence: Using AI responsibly and ethically. Includes making thoughtful choices about AI systems and interactions, maintaining transparency, and taking accountability for AI-assisted work.

## Organize Work and Knowledge

### Introduction to projects

Projects are self-contained workspaces with their own memory, chat histories, knowledge bases, and customized instructions. Think of them as dedicated environments for specific work streams.

- Project Knowledge
- Project instructions

Project Knowledge scale :

When your project knowledge approaches the context window limit, Claude seamlessly enables RAG mode. Instead of loading all project content into memory at once, Claude intelligently searches and retrieves only the most relevant information needed to answer your questions. This expands your project's capacity by up to 10x while maintaining response quality.


### Artifact


Common artifact types  
Claude can create different types of artifacts, each suited to different needs:

- Documents (like markdown, plain text): Great for anything text-heavy that you'll want to export or continue editing—like meeting notes, reports, project plans, blog posts, and other written content.
- Code snippets: Working code in any programming language—Python, JavaScript, C++, and more. You can view the code, copy it, or download it to use in your own projects.
- HTML pages: Complete web pages with HTML, CSS, and JavaScript in a single file. Perfect for landing pages, forms, interactive demos, or quick prototypes.
- SVG images: Scalable vector graphics for logos, icons, illustrations, and other visual elements. These render directly in the artifact window so you can see exactly what you're getting.
- Mermaid diagrams: Flowcharts, sequence diagrams, Gantt charts, org charts, and more. Describe the relationships you want to visualize, and Claude will create a diagram you can refine.
- React components: Interactive UI elements with real functionality—calculators, dashboards, games, data visualizations. These aren't just mockups; they include actual logic and respond to user input.



For example, you might say:

- "Create a flowchart showing our customer onboarding process"
- "Build an interactive dashboard that lets me input monthly expenses and see a breakdown"
- "Design a landing page for a productivity app with a hero section and feature list"
- "Write a project brief template I can reuse for new initiatives"

If Claude doesn't automatically create an artifact when you expect one, you can explicitly ask: "Create this as an artifact" or "Show me this in an artifact."


### Skills

Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Think of them as expertise packages—they teach Claude how to complete specific tasks in a repeatable way.

Types of Skills  
There are two categories of Skills you'll encounter:

- Anthropic Skills are created and maintained by Anthropic.
- Custom Skills are ones you or your organization create for specialized workflows and domain-specific tasks.

**Skills vs. Projects**

Projects store knowledge, skills perform tasks.

