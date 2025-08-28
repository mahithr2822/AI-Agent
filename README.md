# AI-Agent
Absolutely! Here's a more concise version under 250 characters:  An AI agent is a system that senses its environment, processes data, and acts to achieve goals. It uses AI methods like learning and decision-making, enabling applications like chatbots, robots, and virtual assistants.

GitHub stars Discord Cloud Documentation Twitter Follow Twitter Follow Weave Badge

🌤️ Want to skip the setup? Use our cloud for faster, scalable, stealth-enabled browser automation!

Quick start
With pip (Python>=3.11):

pip install browser-use
If you don't already have Chrome or Chromium installed, you can also download the latest Chromium using playwright's install shortcut:

uvx playwright install chromium --with-deps --no-shell
Spin up your agent:

import asyncio
from dotenv import load_dotenv
load_dotenv()
from browser_use import Agent, ChatOpenAI

async def main():
    agent = Agent(
        task="Find the number of stars of the browser-use repo",
        llm=ChatOpenAI(model="gpt-4.1-mini"),
    )
    await agent.run()

asyncio.run(main())
Add your API keys for the provider you want to use to your .env file.

OPENAI_API_KEY=
For other settings, models, and more, check out the documentation 📕.

Demos



Task: Add grocery items to cart, and checkout.

AI Did My Groceries




Prompt: Add my latest LinkedIn follower to my leads in Salesforce.

LinkedIn to Salesforce




Prompt: Read my CV & find ML jobs, save them to a file, and then start applying for them in new tabs, if you need help, ask me.'

 apply.to.jobs.8x.mp4 



Prompt: Write a letter in Google Docs to my Papa, thanking him for everything, and save the document as a PDF.

Letter to Papa




Prompt: Look up models with a license of cc-by-sa-4.0 and sort by most likes on Hugging face, save top 5 to file.

 hugging_face_high_quality.mp4 



More examples
For more examples see the examples folder or join the Discord and show off your project. You can also see our awesome-prompts repo for prompting inspiration.

MCP Integration
Browser-use supports the Model Context Protocol (MCP), enabling integration with Claude Desktop and other MCP-compatible clients.

Use as MCP Server with Claude Desktop
Add browser-use to your Claude Desktop configuration:

{
  "mcpServers": {
    "browser-use": {
      "command": "uvx",
      "args": ["browser-use[cli]", "--mcp"],
      "env": {
        "OPENAI_API_KEY": "sk-..."
      }
    }
  }
}
This gives Claude Desktop access to browser automation tools for web scraping, form filling, and more.

Connect External MCP Servers to Browser-Use Agent
Browser-use agents can connect to multiple external MCP servers to extend their capabilities:

import asyncio
from browser_use import Agent, Tools, ChatOpenAI
from browser_use.mcp.client import MCPClient

async def main():
    # Initialize tools
    tools = Tools()

    # Connect to multiple MCP servers
    filesystem_client = MCPClient(
        server_name="filesystem",
        command="npx",
        args=["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/documents"]
    )

    github_client = MCPClient(
        server_name="github",
        command="npx",
        args=["-y", "@modelcontextprotocol/server-github"],
        env={"GITHUB_TOKEN": "your-github-token"}
    )

    # Connect and register tools from both servers
    await filesystem_client.connect()
    await filesystem_client.register_to_tools(tools)

    await github_client.connect()
    await github_client.register_to_tools(tools)

    # Create agent with MCP-enabled tools
    agent = Agent(
        task="Find the latest pdf report in my documents and create a GitHub issue about it",
        llm=ChatOpenAI(model="gpt-4.1-mini"),
        tools=tools  # Tools has tools from both MCP servers
    )

    # Run the agent
    await agent.run()

    # Cleanup
    await filesystem_client.disconnect()
    await github_client.disconnect()

asyncio.run(main())
See the MCP documentation for more details.

Vision
Tell your computer what to do, and it gets it done.

Roadmap
Agent
 Make agent 3x faster
 Reduce token consumption (system prompt, DOM state)
DOM Extraction
 Enable interaction with all UI elements
 Improve state representation for UI elements so that any LLM can understand what's on the page
Workflows
 Let user record a workflow - which we can rerun with browser-use as a fallback
User Experience
 Create various templates for tutorial execution, job application, QA testing, social media, etc. which users can just copy & paste.
Parallelization
 Human work is sequential. The real power of a browser agent comes into reality if we can parallelize similar tasks. For example, if you want to find contact information for 100 companies, this can all be done in parallel and reported back to a main agent, which processes the results and kicks off parallel subtasks again.
Contributing
We love contributions! Feel free to open issues for bugs or feature requests. To contribute to the docs, check out the /docs folder.

🧪 How to make your agents robust?
We offer to run your tasks in our CI—automatically, on every update!

Add your task: Add a YAML file in tests/agent_tasks/ (see the README there for details).
Automatic validation: Every time we push updates, your task will be run by the agent and evaluated using your criteria.
Local Setup
To learn more about the library, check out the local setup 📕.

main is the primary development branch with frequent changes. For production use, install a stable versioned release instead.

Swag
Want to show off your Browser-use swag? Check out our Merch store. Good contributors will receive swag for free 👀.

Citation
If you use Browser Use in your research or project, please cite:

@software{browser_use2024,
  author = {Müller, Magnus and Žunič, Gregor},
  title = {Browser Use: Enable AI to control your browser},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/browser-use/browser-use}
}

Twitter Follow Twitter Follow

Made with ❤️ in Zurich and San Francisco
