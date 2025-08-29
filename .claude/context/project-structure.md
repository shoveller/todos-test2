---
created: 2025-08-29T02:52:17Z
last_updated: 2025-08-29T02:52:17Z
version: 1.0
author: Claude Code PM System
---

# Project Structure

## Root Directory Layout

```
todos-test2/
├── .claude/                    # Claude Code PM system files
│   ├── context/               # Project context documentation
│   ├── rules/                 # PM system rules
│   └── scripts/               # PM automation scripts
├── .git/                      # Git repository data
├── .idea/                     # IntelliJ IDEA configuration
├── app/                       # React Router application source
│   ├── routes/               # Route components
│   ├── welcome/              # Welcome page components
│   ├── root.tsx              # Root application component
│   └── routes.ts             # Route configuration
├── build/                     # Production build output (generated)
│   ├── client/               # Client-side static assets
│   └── server/               # Server-side rendered code
├── node_modules/              # npm/pnpm dependencies
├── public/                    # Static public assets
└── [config files]            # Various configuration files
```

## Application Source Structure

### `/app` Directory
- **Purpose:** Main application source code
- **Pattern:** React Router v7 application structure
- **Key Files:**
  - `root.tsx` - Root application component and layout
  - `routes.ts` - Central route configuration
  - `routes/` - Individual route components
  - `welcome/` - Feature-specific component grouping

### Route Organization
```
app/routes/
├── home.tsx                   # Home page route
└── [future routes]           # Additional routes as needed
```

### Component Organization
```
app/welcome/
└── welcome.tsx               # Welcome page component
```

## Configuration Files

### Package Management
- `package.json` - Project dependencies and scripts
- `pnpm-lock.yaml` - Lock file for pnpm package manager
- `node_modules/` - Installed dependencies

### Build & Development
- `vite.config.ts` - Vite bundler configuration
- `react-router.config.ts` - React Router build configuration
- `tsconfig.json` - TypeScript compiler configuration

### Deployment
- `Dockerfile` - Container deployment configuration
- `.dockerignore` - Docker build exclusions

### Development Tools
- `.gitignore` - Git exclusions
- `.idea/` - IDE configuration (IntelliJ IDEA)

## File Naming Patterns

### React Components
- **Format:** `kebab-case.tsx` for pages, `PascalCase.tsx` for reusable components
- **Location:** Feature-grouped in relevant directories
- **Example:** `app/welcome/welcome.tsx`

### Route Files
- **Format:** `kebab-case.tsx` in `app/routes/` directory
- **Pattern:** URL path matches file name
- **Example:** `app/routes/home.tsx` → `/home` route

### Configuration Files
- **Format:** `kebab-case.ts` or standard names
- **Location:** Project root for global configs
- **Examples:** `vite.config.ts`, `tsconfig.json`

## Build Output Structure

### Production Build
```
build/
├── client/                   # Static assets served by CDN
│   ├── assets/              # Bundled CSS, JS, images
│   └── [generated files]    # Vite build output
└── server/                   # Server-side application
    └── index.js            # Main server entry point
```

## Module Organization

### Import Patterns
- **Relative imports** for local components and utilities
- **Absolute imports** from `app/` root (configured via tsconfig)
- **External dependencies** from node_modules

### Component Grouping
- **By feature:** Components grouped by functionality (e.g., `welcome/`)
- **By route:** Route-specific components in `routes/`
- **Shared components:** Would go in `app/components/` (not yet created)

## Development Workflow Structure

### Local Development
- Source files in `app/`
- Development server serves from memory
- Hot Module Replacement (HMR) enabled

### Production Build
- Build output in `build/`
- Static assets optimized and bundled
- Server-side rendering prepared

## Asset Management

### Static Assets
- **Location:** `public/` directory
- **Serving:** Available at root URL path
- **Processing:** Served as-is without bundling

### Bundled Assets
- **Processing:** Handled by Vite bundler
- **Location:** `build/client/assets/` after build
- **Optimization:** Minification, tree-shaking, code-splitting enabled