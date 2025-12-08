# Baasix MCP Server

A Model Context Protocol (MCP) server that provides Claude Desktop and other MCP clients with direct access to Baasix headless CMS operations.

## Quick Start

1. **Install dependencies:**
   ```bash
   cd mcp
   npm install
   ```

2. **Configure environment:**
   ```bash
   cp .env.example .env
   # Edit .env with your Baasix server details
   ```

3. **Start the MCP server:**
   ```bash
   npm start
   ```

## Package Usage

When this package is published, users can install and use it like this:

### Installation
```bash
npm install @tspvivek/baasix-mcp-server
```

### Usage in your own server.js
```javascript
import { startMCPServer } from '@tspvivek/baasix-mcp-server';

// Start the MCP server
startMCPServer().catch((error) => {
  console.error('Failed to start MCP server:', error);
  process.exit(1);
});
```

### Custom Usage with BaasixMCPServer class
```javascript
import { BaasixMCPServer } from '@tspvivek/baasix-mcp-server';

// Create and customize your own server instance
const server = new BaasixMCPServer();
server.run().catch((error) => {
  console.error('Failed to start MCP server:', error);
  process.exit(1);
});
```

## Configuration

The MCP server uses environment-specific configuration files, similar to the API server:

### Environment Files
- `.env` - Development environment (default)
- `.env.production` - Production environment

### Available Scripts
- `npm run development` - Start with development environment (`.env`)
- `npm start` - Start with production environment (`.env.production`)
- `npm run dev` - Development mode with auto-restart (`.env`)
- `npm test` - Run tests with development environment
- `npm run debug` - Start with MCP inspector for debugging

### Environment Variables
- `BAASIX_URL` - Your Baasix server URL (required)
- `BAASIX_AUTH_TOKEN` - Pre-obtained JWT token (recommended for production)
- `BAASIX_EMAIL` - Email for auto-authentication (alternative to token)
- `BAASIX_PASSWORD` - Password for auto-authentication (alternative to token)

### Authentication Methods

1. **Manual Token** (Recommended for production):
   - Set `BAASIX_AUTH_TOKEN` with a pre-obtained JWT token
   - Token management is handled externally

2. **Auto-login** (Convenient for development):
   - Set `BAASIX_EMAIL` and `BAASIX_PASSWORD`
   - Server automatically authenticates and manages tokens

## Available Tools

The MCP server provides comprehensive tools for Baasix operations:

### Schema Management
- `baasix_list_schemas` - List all collections/schemas
- `baasix_get_schema` - Get schema details for a collection
- `baasix_create_schema` - Create new collection schema
- `baasix_update_schema` - Update existing schema
- `baasix_delete_schema` - Delete schema

### Item Management
- `baasix_list_items` - Query items with filtering, sorting, pagination
- `baasix_get_item` - Get specific item by ID
- `baasix_create_item` - Create new item
- `baasix_update_item` - Update existing item
- `baasix_delete_item` - Delete item

### File Management
- `baasix_list_files` - List files with metadata
- `baasix_get_file_info` - Get file information
- `baasix_delete_file` - Delete file

### Authentication
- `baasix_auth_status` - Check authentication status
- `baasix_refresh_auth` - Refresh authentication token

### Reports & Analytics
- `baasix_generate_report` - Generate reports with grouping
- `baasix_get_stats` - Get collection statistics

### Notifications
- `baasix_list_notifications` - List user notifications
- `baasix_send_notification` - Send notifications
- `baasix_mark_notification_seen` - Mark notifications as seen

### Settings
- `baasix_get_settings` - Get application settings
- `baasix_update_settings` - Update settings

### Permissions
- `baasix_list_roles` - List available roles
- `baasix_get_permissions` - Get role permissions
- `baasix_update_permissions` - Update role permissions

### Utilities
- `baasix_server_info` - Get server information and health status

## Development

### Running in Development Mode
```bash
npm run dev
```

### Testing
```bash
npm test
```

### Debugging
```bash
npm run debug
```

## Integration with Claude Desktop

To use this MCP server with Claude Desktop, add it to your Claude configuration file (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "baasix": {
      "command": "node",
      "args": ["/path/to/baasix/mcp/server.js"],
      "env": {
        "BAASIX_URL": "http://localhost:8056",
        "BAASIX_EMAIL": "admin@baasix.com",
        "BAASIX_PASSWORD": "admin@123"
      }
    }
  }
}
```

## File Structure

```
mcp/
├── server.js              # Entry point (similar to api/server.js)
├── package.json           # Dependencies and scripts
├── .env                   # Environment configuration
├── .env.example          # Environment template
├── README.md             # This file
└── baasix/               # Core MCP server implementation
    ├── index.js          # Main server class and logic
    └── config.js         # Configuration management
```

This structure follows the same pattern as the `api/` folder, with `baasix/` containing the core implementation and `server.js` as the simple entry point.

## Claude Code - Adding and Removing using command
```claude mcp add servicecrm-mcp npm run start
```

```claude mcp remove servicecrm-mcp
```
