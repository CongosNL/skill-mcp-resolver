# MCP Server Starter Template

## package.json

```json
{
  "name": "mcp-server-[name]",
  "version": "0.1.0",
  "type": "module",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.0.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

## tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"]
}
```

## src/index.ts

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({ name: "mcp-server-[name]", version: "0.1.0" }, {
  capabilities: { tools: {} }
});

server.setRequestHandler("tools/list", async () => ({
  tools: [{
    name: "[tool-name]",
    description: "[What the tool does]",
    inputSchema: { type: "object", properties: {} }
  }]
}));

server.setRequestHandler("tools/call", async (request) => {
  if (request.params.name === "[tool-name]") {
    return { content: [{ type: "text", text: "Result" }] };
  }
  throw new Error("Unknown tool");
});

new StdioServerTransport().connect(server);
```

## Project Structure

```
[project-name]/
├── package.json
├── tsconfig.json
├── src/
│   └── index.ts
└── .mcp.json
```

## .mcp.json (for local testing)

```json
{
  "mcpServers": {
    "[name]": {
      "command": "node",
      "args": ["dist/index.js"]
    }
  }
}
```

## Next Steps

1. `npm install`
2. Implement tool logic in `src/index.ts`
3. `npm run build`
4. Test locally: add to `.mcp.json`
5. (Optional) Publish to npm
6. (Optional) Submit to MCP Registry
