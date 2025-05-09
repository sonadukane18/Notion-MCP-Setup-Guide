# Detailed Notion Integration Setup

This document provides additional details on setting up your Notion integration for use with MCP.

## Creating a Notion Integration

1. Go to [https://www.notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Click on the **"+ New integration"** button
3. Fill in the integration details:
   - **Name**: Choose a descriptive name (e.g., "Cursor AI Assistant")
   - **Associated workspace**: Select the workspace you want to use
   - **Logo**: Optional - you can upload a custom logo
   - **Capabilities**: Select the capabilities your integration needs:
     - Read content
     - Update content
     - Insert content
     - Read comments
     - Create comments

4. Once created, you'll receive an **"Internal Integration Token"** that starts with `secret_`
5. Save this token securely - you'll need it for your MCP configuration

## Sharing Pages with Your Integration

For your integration to access specific pages in Notion:

1. Open a page in your Notion workspace
2. Click the **"•••"** (three dots) menu in the top right corner
3. Select **"Add connections"**
4. Find and select your integration name from the list
5. The page and all of its subpages will now be accessible to your integration

**Important Notes:**
- You must explicitly share each top-level page you want the AI to access
- Sharing a page also shares all of its subpages
- Database pages must be shared separately
- You cannot share individual pages within a database - you must share the entire database

## Permission Model

Notion's integration permission model works hierarchically:

- Integrations only have access to pages explicitly shared with them
- When you share a page, all of its subpages are automatically shared
- Permissions do not propagate upward (sharing a subpage does not grant access to its parent)
- You cannot restrict access to specific subpages once the parent is shared

## Best Practices

1. **Create a dedicated section for AI**: Consider creating a specific section in your workspace dedicated to AI interactions
2. **Use clear naming**: Name your pages and databases clearly so the AI can understand their purpose
3. **Regular token rotation**: For security, rotate your integration token periodically
4. **Limit scope**: Only share the pages that you need the AI to access
5. **Test incrementally**: Start by sharing one page, test the functionality, then expand access as needed

## Troubleshooting Access Issues

If your AI cannot access a specific page:

1. Verify the page has been explicitly shared with your integration
2. Check that your integration token is correctly configured in your MCP setup
3. Ensure your integration has the necessary capabilities enabled
4. Try sharing a parent page if the page is nested within another structure
5. For database items, make sure the parent database has been shared

## Advanced: Customizing Your Integration

For more advanced users, you can:

1. Add a custom icon and description for your integration
2. Set up public integrations (requires Notion approval)
3. Use OAuth for multi-user applications
4. Implement rate limiting strategies for high-volume usage