# Cursor IDE MCP Configuration Guide

This guide details how to configure Cursor IDE to work with the Notion MCP server.

## Understanding the MCP Configuration File

The MCP configuration file is a JSON file that tells Cursor IDE which external services to connect to and how to communicate with them. For Notion integration, this file needs to be set up correctly.

## Location of the MCP Configuration File

The MCP configuration file is stored in your user directory:

- **Windows**: `C:\Users\YourUsername\.cursor\mcp.json`
- **macOS**: `/Users/YourUsername/.cursor/mcp.json`
- **Linux**: `/home/YourUsername/.cursor/mcp.json`

## Basic Configuration Structure

A basic MCP configuration file for Notion looks like this:

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

## Key Components Explained

1. **mcpServers**: The parent object containing all your MCP server configurations
2. **notionApi**: An identifier for the Notion MCP server (you can name this whatever you want)
3. **command**: The command to run the MCP server (typically `npx` for Node.js-based servers)
4. **args**: Array of arguments to pass to the command
   - `-y`: Automatically answer "yes" to any prompts
   - `@notionhq/notion-mcp-server`: The NPM package for the Notion MCP server
5. **env**: Environment variables to pass to the MCP server
   - `OPENAPI_MCP_HEADERS`: JSON string containing headers to send with each API request
     - `Authorization`: Bearer token containing your Notion integration token
     - `Notion-Version`: The version of the Notion API to use

## Multiple MCP Servers Configuration

You can configure multiple MCP servers in the same configuration file:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer secret_your_notion_token_here\", \"Notion-Version\": \"2022-06-28\" }"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_github_pat_here"
      }
    }
  }
}
```

## Troubleshooting Configuration Issues

### Configuration File Not Found

If Cursor can't find your MCP configuration file:

1. Verify the file exists at the correct location
2. Ensure the file is named `mcp.json` (case-sensitive)
3. Try creating the file manually if it doesn't exist

### JSON Parsing Errors

If your configuration file has invalid JSON:

1. Validate your JSON using a JSON validator
2. Check for missing commas, brackets, or quotes
3. Ensure all JSON strings are properly escaped

### Connection Issues

If Cursor can't connect to the Notion MCP server:

1. Check your internet connection
2. Verify that Node.js is installed on your system
3. Try running the command manually to see if it works:
   ```
   npx -y @notionhq/notion-mcp-server
   ```
4. Check for firewall or antivirus software blocking the connection

### Authentication Issues

If the MCP server can't authenticate with Notion:

1. Verify your Notion integration token is correct
2. Check that the token hasn't expired
3. Ensure the token has the necessary permissions
4. Verify the Notion API version is current

## Restarting Cursor after Configuration Changes

After making changes to your MCP configuration file:

1. Save the file
2. Completely close Cursor IDE
3. Restart Cursor IDE
4. Start a new conversation with the AI assistant

## Advanced: Using Configuration Variables

For more security, you can use environment variables in your configuration:

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer ${NOTION_TOKEN}\", \"Notion-Version\": \"2022-06-28\" }"
      }
    }
  }
}
```

Then set the environment variable `NOTION_TOKEN` before starting Cursor.