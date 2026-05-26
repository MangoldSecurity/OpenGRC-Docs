# MCP Server

!!! enterprise "Enterprise Feature"
    The enhanced MCP Server is available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

The OpenGRC MCP (Model Context Protocol) Server lets AI assistants like **Claude** and **ChatGPT** interact directly with your OpenGRC data. Once connected, you can ask the assistant to read, create, and update programs, controls, audits, risks, policies, incidents, and more -- all through natural language and all governed by your existing user permissions.

## Overview

- **OAuth 2.1** authentication with Dynamic Client Registration -- no API keys to manage
- **Per-user access** -- the AI acts on behalf of the authenticated user and inherits their permissions
- Supports any MCP-compatible client (Claude.ai, Claude Desktop, ChatGPT, Cursor, etc.)
- Manages the full OpenGRC object model: Programs, Standards, Controls, Implementations, Audits, Risks, Policies, Vendors, Assets, Incidents, Evidence, and more

## Enable the MCP Server

Before clients can connect, an administrator must enable MCP in the application:

1. Navigate to **Settings > AI Settings**
2. Scroll to the **MCP Server** section
3. Toggle **Enable MCP Server** on and save

## Find Your MCP Endpoint

Each OpenGRC instance has its own MCP endpoint URL based on its hostname.

1. Go to **Settings > AI Settings**
2. Expand the **OAuth 2.1 Endpoints** section
3. Copy the value next to **MCP Endpoint**

The MCP endpoint follows this pattern:

```
https://<your-opengrc-host>/mcp/opengrc
```

You will use this URL when configuring any MCP client.

## Connect Claude

OpenGRC works with both Claude.ai (web) and Claude Desktop. Both use the same OAuth 2.1 flow -- there are no client secrets or API keys to copy.

### Claude.ai (Web)

1. Sign in to [claude.ai](https://claude.ai) on a plan that supports custom connectors (Pro, Team, or Enterprise)
2. Open **Settings > Connectors** (or **Settings > Integrations**)
3. Click **Add custom connector**
4. Fill in:
    - **Name**: `OpenGRC` (or any label you prefer)
    - **Remote MCP server URL**: your MCP endpoint, e.g. `https://{your OpenGRC URL}/mcp/opengrc`
5. Click **Add** / **Connect**
6. A browser tab opens to your OpenGRC sign-in page. Log in if prompted, then click **Authorize** on the consent screen
7. You will be returned to Claude with the connector marked as connected

### Claude Desktop

1. Open Claude Desktop and go to **Settings > Connectors**
2. Click **Add custom connector**
3. Enter your MCP endpoint URL (e.g. `https://{your OpenGRC URL}/mcp/opengrc`)
4. Complete the OAuth login and authorization in the browser window that opens
5. Restart Claude Desktop if the tools do not appear immediately

Once connected, start a new chat and ask Claude something like *"List my open audits in OpenGRC"* to confirm the tools are available.

## Connect ChatGPT

ChatGPT supports remote MCP servers via **Custom Connectors** for Business, Enterprise, Edu, and Pro accounts.

1. Sign in to [chatgpt.com](https://chatgpt.com)
2. Open **Settings > Connectors** and choose **Create** (or **Add custom connector**)
3. Fill in:
    - **Name**: `OpenGRC`
    - **MCP Server URL**: your MCP endpoint, e.g. `https://grc.example.com/mcp/opengrc`
    - **Authentication**: select **OAuth**
4. Save -- ChatGPT will redirect you to OpenGRC to sign in and authorize the connection
5. After approving, return to ChatGPT. The connector will appear in your tool list

To use the connector in a conversation, enable it from the tools/connectors menu in the composer, then ask questions like *"Show me the controls in my NIST 800-53 program."*

!!! note "Plan availability"
    Custom MCP connectors require a paid ChatGPT plan that supports them. Free accounts cannot add remote MCP servers.

## How Authorization Works

OpenGRC implements OAuth 2.1 with Dynamic Client Registration ([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591)). 

When you add the connector, your capabilities are tied to **your user account**. Any action the AI takes is performed as you and respects all role and permission checks.

## Revoking Access

To disconnect an AI client:

- **From OpenGRC**: an administrator can disable MCP entirely under **Settings > AI Settings > MCP Server**. Individual tokens can be revoked from Laravel Passport storage if needed.
- **From the client**: remove the connector from Claude or ChatGPT's settings. The next request will fail until you re-authorize.

## Permissions

- Enabling or disabling the MCP server requires an **Super Admin** role
- Connecting a client requires any user account that can sign in to OpenGRC
- All MCP tool calls run as the authenticated user and inherit their existing permissions
