# 🚀 OpenAPI Spec Master

[![npm version](https://badge.fury.io/js/openapi-spec-master.svg)](https://badge.fury.io/js/openapi-spec-master)
[![Downloads](https://img.shields.io/npm/dm/openapi-spec-master.svg)](https://www.npmjs.com/package/openapi-spec-master)
[![NPM](https://img.shields.io/npm/l/openapi-spec-master.svg)](https://www.npmjs.com/package/openapi-spec-master)
[![VS Code Extension](https://img.shields.io/visual-studio-marketplace/v/RyanCardin.openapi-spec-explorer)](https://marketplace.visualstudio.com/items?itemName=RyanCardin.openapi-spec-explorer)

> **The ultimate OpenAPI specification toolkit for professional developers**

A powerful, professional-grade OpenAPI specification analyzer with advanced AI integration via Model Context Protocol (MCP). Features comprehensive API analysis, code generation, and seamless integration with VS Code extension.

**📦 [Available on NPM](https://www.npmjs.com/package/openapi-spec-master)** - Install with `npx openapi-spec-master@latest`  
**🔌 [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=RyanCardin.openapi-spec-explorer)** - Professional IDE integration

---

## ✨ **Why Choose OpenAPI Spec Master?**

- 🎯 **Professional Grade**: Enterprise-ready with advanced performance optimizations
- 🤖 **AI Integration**: Native MCP server for Claude, Cursor, and other AI tools
- ⚡ **Lightning Fast**: Optimized for large specifications with intelligent caching
- 🔍 **Deep Analysis**: 16 powerful tools for comprehensive API insights
- 🛠️ **Multi-Language**: Generate code in TypeScript, JavaScript, Python, cURL, and more
- 📊 **Rich Analytics**: Advanced filtering, grouping, and visualization capabilities
- 🔌 **VS Code Integration**: Professional extension for seamless development workflow

---

## Features

### 🔍 Advanced Analysis
- **Smart Filtering**: Multi-dimensional filtering by methods, tags, complexity, security, and more
- **Intelligent Grouping**: Organize endpoints by tags, methods, complexity, or path patterns
- **Analytics Dashboard**: Comprehensive API analytics with distribution charts and insights
- **AI Suggestions**: Context-aware recommendations for API improvements

### 🤖 MCP Server Integration
- **One-Click Cursor Installation**: Native deeplink support for instant Cursor IDE setup
- **Dual Transport Support**: Both stdio and HTTP transport options
- **AI Client Connectivity**: Connect to Claude Desktop, Cursor, and other MCP-compatible clients
- **16 Powerful Tools**: Comprehensive suite for API analysis, development, validation, and optimization
- **Advanced Schema Analysis**: Deep property searching, dependency tracking, and evolution analysis
- **Code Generation**: TypeScript types, mock data, and multi-language examples
- **Security & Validation**: Authentication analysis, example validation, and design recommendations
- **Real-time Analysis**: Get instant API insights through your AI conversations
- **Streaming Support**: Server-sent events for real-time updates (HTTP transport)

### 📊 Visualization & Export
- **Multiple View Modes**: List, grid, compact, and table layouts
- **Export Options**: JSON, PDF, CSV, and Markdown formats
- **Dark/Light Theme**: Beautiful UI with theme switching
- **Responsive Design**: Works perfectly on desktop and mobile

## Quick Start

### 🚀 NPX Usage (Recommended)

**Get started instantly without installation:**

```bash
# Show setup instructions
npx openapi-spec-master@latest setup

# Start MCP server (stdio transport)
npx openapi-spec-master@latest mcp

# Start MCP server (HTTP transport)
npx openapi-spec-master@latest mcp --http

# Start web interface (development mode)
npx openapi-spec-master@latest web
```

### 📦 Installation

If you prefer to install globally:

```bash
npm install -g openapi-spec-master
```

### 🤖 MCP Server Setup

#### Option A: Cursor Deeplink (Easiest!) 🆕
**One-click installation for Cursor users:**

**For stdio transport (recommended):**
[**🚀 Add OpenAPI Spec Master to Cursor**](cursor://anysphere.cursor-deeplink/mcp/install?name=openapi-spec-master&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyJvcGVuYXBpLXNwZWMtbWFzdGVyQGxhdGVzdCIsICJtY3AiXX0=)

> **Note:** Deeplinks require Cursor IDE. For other AI tools, use the manual configuration below.  
> Learn more about [Cursor Deeplinks](https://docs.cursor.com/deeplinks)

#### Option B: NPX (Manual Configuration)
Easy setup for Claude Desktop and other MCP-compatible clients:

**Configure Claude Desktop** (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):
```json
{
  "mcpServers": {
    "openapi-spec-master": {
      "command": "npx",
      "args": ["openapi-spec-master@latest", "mcp"]
    }
  }
}
```

**For HTTP transport:**
```json
{
  "mcpServers": {
    "openapi-spec-master-http": {
      "command": "npx",
      "args": ["openapi-spec-master@latest", "mcp", "--http", "--port", "3001"]
    }
  }
}
```

#### Option C: Local Development
For development or customization:

1. Clone the repository
2. Install dependencies: `npm install`
3. Build the servers: `npm run build:all`

**Configure with local build:**
```json
{
  "mcpServers": {
    "openapi-spec-master": {
      "command": "node",
      "args": ["path/to/openapi-spec-master/dist/mcp/server.js"]
    }
  }
}
```

### Web Application (Development)
1. Clone the repository
2. Install dependencies: `npm install`
3. Start the development server: `npm run dev`
4. Open your browser and load an OpenAPI specification

#### Test the Connection

**Test with NPX:**
```bash
npx openapi-spec-master@latest mcp
```

**Test HTTP server:**
```bash
npx openapi-spec-master@latest mcp --http
# Check health: curl http://localhost:3001/health
```

## HTTP Transport Features

The HTTP transport provides additional capabilities beyond the standard MCP protocol:

### RESTful API Endpoints
- `GET /health` - Server health check
- `POST /mcp/tools/list` - List available MCP tools
- `POST /mcp/tools/call` - Execute an MCP tool
- `GET /mcp/stream` - Server-sent events stream
- `POST /mcp/execute` - Execute tool with optional streaming
- `GET /api/info` - Get loaded API information
- `GET /api/endpoints` - Search endpoints directly
- `GET /docs` - API documentation

### Streaming Support
```bash
# Real-time updates via Server-Sent Events
curl -N http://localhost:3001/mcp/stream

# Streaming tool execution
curl -X POST http://localhost:3001/mcp/execute \
  -H "Content-Type: application/json" \
  -d '{"tool": "get_api_overview", "args": {}, "stream": true}'
```

### Direct API Access
```bash
# Load OpenAPI spec
curl -X POST http://localhost:3001/mcp/tools/call \
  -H "Content-Type: application/json" \
  -d '{
    "name": "load_openapi_spec",
    "arguments": {
      "source": "https://petstore.swagger.io/v2/swagger.json",
      "sourceType": "url"
    }
  }'

# Search endpoints
curl "http://localhost:3001/api/endpoints?query=user&method=GET&limit=10"
```

## MCP Tools Available

### Core Functions (4 tools)
- `load_openapi_spec` - Load and parse OpenAPI specifications from multiple sources
- `get_api_overview` - Get comprehensive API overview and statistics
- `search_endpoints` - Search and filter endpoints with advanced criteria
- `get_endpoint_details` - Get detailed information about specific endpoints

### Development Tools (3 tools)
- `generate_code_examples` - Generate code examples in multiple programming languages
- `generate_typescript_types` - Convert OpenAPI schemas to TypeScript interfaces and types
- `generate_mock_data` - Generate realistic mock data based on OpenAPI schemas

### Analysis & Validation (5 tools)
- `search_request_body_properties` - Deep search through request body schemas for properties
- `find_schema_dependencies` - Trace schema references and dependencies throughout the API
- `validate_request_examples` - Validate that request/response examples match their schemas
- `get_api_analytics` - Comprehensive API analytics and insights
- `validate_api_design` - API design validation with recommendations

### Security & Optimization (3 tools)
- `extract_auth_patterns` - Analyze authentication and authorization patterns across the API
- `find_unused_schemas` - Identify schemas that are defined but never referenced
- `analyze_schema_evolution` - Analyze how schemas might evolve and suggest versioning strategies

### Documentation (1 tool)
- `export_documentation` - Export API documentation in various formats

## 🔥 New Advanced Capabilities

The latest version introduces 8 powerful new tools that dramatically expand analysis capabilities:

### 🔍 Deep Schema Analysis
- **Property Search**: Find specific properties across all request/response schemas
- **Dependency Mapping**: Understand how schemas relate and depend on each other
- **Evolution Analysis**: Assess how schemas might change and plan versioning strategies

### 🛡️ Security & Quality Assurance
- **Auth Pattern Analysis**: Comprehensive security scheme analysis and recommendations
- **Example Validation**: Ensure all documented examples actually match their schemas
- **Unused Schema Detection**: Clean up APIs by finding orphaned schema definitions

### ⚡ Developer Productivity
- **TypeScript Generation**: Auto-generate type-safe interfaces from OpenAPI schemas
- **Smart Mock Data**: Context-aware mock data generation that understands field semantics
- **Advanced Code Examples**: Multi-language code generation with proper typing

These tools work seamlessly with AI clients to provide unprecedented insight into API design, helping developers build better, more maintainable APIs.

## Usage Examples with AI Clients

Once connected to Claude Desktop or Cursor, you can use prompts like:

### Core Operations
- "Load this OpenAPI spec and give me an overview: [paste spec]"
- "Search for all POST endpoints in the user management section"
- "Get detailed information about the GET /users/{id} endpoint"

### Development & Code Generation
- "Generate a Python example for the GET /users/{id} endpoint"
- "Generate TypeScript interfaces for all schemas in this API"
- "Create realistic mock data for the User schema"

### Advanced Analysis
- "Find all properties named 'email' in request bodies"
- "Show me the schema dependencies for the User model"
- "Validate all examples against their schemas"
- "Analyze the authentication patterns used in this API"
- "Find any unused schemas that could be cleaned up"

### Optimization & Planning
- "Analyze how the User schema might evolve over time"
- "Get comprehensive analytics about this API's design"
- "Validate the API design and suggest improvements"
- "Export the documentation in markdown format"

## Supported Formats

- **OpenAPI 3.0+** (JSON/YAML)
- **Swagger 2.0** (JSON/YAML) - automatically converted
- **URL Loading** - Direct import from API endpoints
- **File Upload** - Drag & drop or file picker
- **Text Paste** - Direct specification pasting

## Development

### Project Structure
```
src/
├── components/          # React components
├── utils/              # Utility functions
├── hooks/              # Custom React hooks
├── types/              # TypeScript type definitions
└── mcp/               # MCP server implementations
    ├── server.ts      # Stdio transport server
    └── http-server.ts # HTTP transport server
```

### Available Scripts
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run mcp:build` - Build stdio MCP server
- `npm run mcp:http:build` - Build HTTP MCP server
- `npm run mcp:dev` - Run stdio MCP server in development
- `npm run mcp:http` - Run HTTP MCP server in development

## Transport Comparison

| Feature | Stdio Transport | HTTP Transport |
|---------|----------------|----------------|
| **Latency** | Lower | Higher |
| **Setup** | Simple | Moderate |
| **Streaming** | No | Yes (SSE) |
| **Direct Access** | No | Yes (REST API) |
| **MCP Standard** | ✅ | ✅ |
| **Custom Integration** | Limited | Full |
| **Debugging** | Harder | Easier |

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

MIT License - see LICENSE file for details.

## Support

- 📖 Check the in-app MCP instructions for detailed setup
- 🐛 Report issues on GitHub
- 💡 Request features through GitHub issues
- 🌐 HTTP API documentation at `/docs` endpoint