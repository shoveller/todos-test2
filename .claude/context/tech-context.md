---
created: 2025-08-29T02:52:17Z
last_updated: 2025-08-29T02:52:17Z
version: 1.0
author: Claude Code PM System
---

# Technology Context

## Core Technology Stack

### Frontend Framework
- **React** v19.1.0 - Latest React version with modern features
- **React DOM** v19.1.0 - React rendering engine
- **React Router** v7.7.1 - File-based routing and SSR framework

### Development Language
- **TypeScript** v5.8.3 - Type-safe JavaScript development
- **Node.js** v20+ - Runtime environment (inferred from @types/node)

### Package Management
- **pnpm** v10.12.4 - Fast, disk-efficient package manager
- **Package Manager:** Explicitly configured in package.json

## Build & Development Tools

### Build System
- **Vite** v6.3.3 - Modern build tool and dev server
- **@react-router/dev** v7.7.1 - React Router development tools
- **vite-tsconfig-paths** v5.1.4 - Path resolution for TypeScript

### Development Server
- **@react-router/node** v7.7.1 - Node.js server runtime
- **@react-router/serve** v7.7.1 - Production server

## Styling & UI

### CSS Framework
- **TailwindCSS** v4.1.4 - Utility-first CSS framework
- **@tailwindcss/vite** v4.1.4 - Vite integration for Tailwind

## Runtime Dependencies

### Core Libraries
```json
"dependencies": {
  "@react-router/node": "^7.7.1",
  "@react-router/serve": "^7.7.1", 
  "isbot": "^5.1.27",
  "react": "^19.1.0",
  "react-dom": "^19.1.0",
  "react-router": "^7.7.1"
}
```

### Utility Libraries
- **isbot** v5.1.27 - User agent bot detection

## Development Dependencies

### Type Definitions
- **@types/node** v20+ - Node.js type definitions
- **@types/react** v19.1.2 - React type definitions  
- **@types/react-dom** v19.1.2 - React DOM type definitions

### Development Tools
```json
"devDependencies": {
  "@react-router/dev": "^7.7.1",
  "@tailwindcss/vite": "^4.1.4",
  "tailwindcss": "^4.1.4",
  "typescript": "^5.8.3",
  "vite": "^6.3.3",
  "vite-tsconfig-paths": "^5.1.4"
}
```

## Scripts & Commands

### Development Workflow
- **`pnpm dev`** - Start development server with HMR
- **`pnpm build`** - Create production build
- **`pnpm start`** - Run production server
- **`pnpm typecheck`** - Run TypeScript type checking

### Build Process
1. `react-router build` - Creates optimized production build
2. `react-router-serve ./build/server/index.js` - Serves production build
3. `react-router typegen && tsc` - Type generation and checking

## Development Environment

### Package Manager Configuration
- **pnpm workspace** support ready
- **Lock file:** `pnpm-lock.yaml` for dependency consistency
- **Node version:** Compatible with Node 20+

### TypeScript Configuration
- **Target:** Modern ES modules
- **Type checking:** Strict mode enabled
- **Path mapping:** Configured for absolute imports from `app/`

## Architecture Patterns

### Server-Side Rendering (SSR)
- React Router v7 with built-in SSR capabilities
- Hydration on client-side for interactivity
- SEO-friendly with server-rendered HTML

### Modern React Patterns
- Function components with hooks
- React 19 features available (concurrent features, etc.)
- TypeScript for type safety throughout

### Build Optimization
- **Vite bundling** for fast development and optimized production
- **Code splitting** automatic with React Router
- **Tree shaking** for minimal bundle size
- **Hot Module Replacement** for development speed

## Deployment Stack

### Containerization
- **Docker** support with included Dockerfile
- **Multi-stage build** for optimized production image
- **Port 3000** default for production server

### Platform Compatibility
- **Node.js servers** (self-hosted)
- **Docker containers** (AWS ECS, Google Cloud Run, etc.)
- **Static hosting** (client-side build can be served statically)

## Version Management

### Dependency Versioning Strategy
- **Caret ranges (^)** for automatic minor/patch updates
- **Lock file** ensures consistent installs across environments
- **Latest stable versions** of all major dependencies

### Framework Versions
- React Router v7 (latest major version)
- React v19 (cutting-edge React features)
- TypeScript v5 (modern TS capabilities)
- Vite v6 (latest build tooling)