# Setting Up Notion MCP with Cursor IDE

This guide provides step-by-step instructions for configuring a Notion Model Context Protocol (MCP) server to work with Cursor IDE, enabling AI assistants to interact with your Notion workspace.

## What is Model Context Protocol (MCP)?

Model Context Protocol (MCP) is a standardized interface that allows AI assistants to interact with external systems and APIs. When configured with Notion, it enables AI models to:

- Create and manage pages and databases
- Search for content
- Add content blocks and comments
- Query databases
- Retrieve and update information
- And more!

## Prerequisites

- [Cursor IDE](https://cursor.sh/) installed on your computer
- A [Notion](https://www.notion.so/) account
- Basic familiarity with Node.js and command line tools

## Step 1: Create a Notion Integration

First, you need to create a Notion integration to get an API key:

1. Go to [https://www.notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Click **"+ New integration"**
3. Name your integration (e.g., "Cursor AI Assistant")
4. Select the workspace you want to connect to
5. Set the appropriate capabilities:
   - ✅ Read content
   - ✅ Update content
   - ✅ Insert content
   - ✅ Read comments
   - ✅ Create comments
6. Click **"Submit"** to create your integration
7. Copy your **Internal Integration Token** (it starts with `secret_...`)

## Step 2: Configure the MCP Configuration File

1. Create or edit the MCP configuration file in your user directory:
   - Windows: `C:\Users\YourUsername\.cursor\mcp.json`
   - macOS/Linux: `~/.cursor/mcp.json`

2. Add the Notion MCP server configuration:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer secret_your_notion_token_here\", \"Notion-Version\": \"2022-06-28\" }"
      }
    }
  }
}
```

3. Replace `secret_your_notion_token_here` with your actual Notion integration token from Step 1.

## Step 3: Share Pages with Your Integration

For your integration to access specific pages in Notion:

1. Open a page in your Notion workspace
2. Click the **"•••"** (three dots) menu in the top right
3. Select **"Add connections"**
4. Find and select your integration name
5. The page (and its subpages) will now be accessible to your integration

**Note:** You must explicitly share each top-level page you want the AI to access.

## Step 4: Test Your Notion MCP Setup

1. Open Cursor IDE
2. Start a conversation with the AI assistant
3. Ask it to perform a simple Notion operation like:
   - "List the pages I have access to in Notion"
   - "Create a new page called 'Test Page' in my Notion workspace"
   - "Search for pages with the keyword 'project'"

If the configuration is correct, the AI should be able to perform these operations through the Notion API.

## Troubleshooting

### Common Issues and Solutions

#### "Could not find page with ID" Error
- **Cause**: The page hasn't been shared with your integration
- **Solution**: Share the page with your integration as described in Step 3

#### "Invalid token" Error
- **Cause**: Incorrect or expired Notion token
- **Solution**: Verify your token in the Notion integrations page and update it in the MCP config

#### "Permission denied" Error
- **Cause**: The integration doesn't have the required capabilities
- **Solution**: Check the capabilities you've granted to your integration in the Notion integrations page

#### No Notion Server Found
- **Cause**: MCP server for Notion not properly configured
- **Solution**: Verify your mcp.json file has the correct configuration and is in the right location

## Advanced Configuration

### Using Environment Variables

For better security, you can use environment variables instead of hardcoding the token:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "${NOTION_API_KEY}",
        "NOTION_VERSION": "2022-06-28"
      }
    }
  }
}
```

### Custom Server Options

You can customize the Notion MCP server with additional options:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server", "--options", "{\"debug\": true}"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer secret_your_token_here\", \"Notion-Version\": \"2022-06-28\" }"
      }
    }
  }
}
```

## Example Usage

Here are some examples of what you can ask the AI assistant to do with your Notion workspace:

### Creating Content
- "Create a new page titled 'Project Ideas' in my Notion workspace"
- "Add a to-do list to my 'Tasks' page"
- "Create a table with columns for Name, Status, and Due Date"

### Managing Content
- "Find all pages related to 'marketing'"
- "Update the status of 'Website Redesign' to 'In Progress'"
- "Add a comment to the 'Budget Review' page saying 'Please review by Friday'"

### Retrieving Information
- "Show me all the items in my 'Reading List' database"
- "Get the details of my 'Team Meeting' page"
- "Find all tasks with a due date this week"

## Resources

- [Notion API Documentation](https://developers.notion.com/)
- [Notion MCP Server Package](https://www.npmjs.com/package/@notionhq/notion-mcp-server)
- [Model Context Protocol Specification](https://github.com/modelcontextprotocol/protocol)
- [Cursor IDE Documentation](https://cursor.sh/docs)

---

*Note: Keep your Notion integration token secure and never commit it to public repositories.*