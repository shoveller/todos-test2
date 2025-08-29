---
created: 2025-08-29T02:52:17Z
last_updated: 2025-08-29T02:52:17Z
version: 1.0
author: Claude Code PM System
---

# Project Style Guide

## Code Style & Conventions

### TypeScript Standards

#### Type Safety Requirements
```typescript
// ✅ Strict TypeScript configuration enabled
"strict": true,
"noEmit": true,
"verbatimModuleSyntax": true

// ✅ Prefer explicit typing for exported functions
export function meta({}: Route.MetaArgs): MetaDescriptor[] {
  return [{ title: "Page Title" }];
}

// ✅ Use generated route types
import type { Route } from "./+types/home";
```

#### Import/Export Patterns
```typescript
// ✅ Default exports for main route components
export default function Home() {
  return <Welcome />;
}

// ✅ Named exports for utilities and secondary functions
export function meta({}: Route.MetaArgs) { ... }
export function ErrorBoundary({ error }: Route.ErrorBoundaryProps) { ... }

// ✅ Import order: React → React Router → Types → Local components
import { Links, Meta, Outlet } from "react-router";
import type { Route } from "./+types/root";
import { Welcome } from "../welcome/welcome";
```

#### Path Resolution
```typescript
// ✅ Use absolute imports from app root
import { Welcome } from "../welcome/welcome"; // Current pattern
// Configured alias available: import { Welcome } from "~/welcome/welcome";

// ✅ Relative imports for local utilities
import "./app.css";
import logoDark from "./logo-dark.svg";
```

### React Component Standards

#### Component Definition Pattern
```typescript
// ✅ Function components with explicit typing
export function Layout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <head>
        <meta charSet="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <Meta />
        <Links />
      </head>
      <body>
        {children}
        <ScrollRestoration />
        <Scripts />
      </body>
    </html>
  );
}

// ✅ Route components with meta and error boundary exports
export default function Home() {
  return <Welcome />;
}

export function meta({}: Route.MetaArgs) {
  return [
    { title: "New React Router App" },
    { name: "description", content: "Welcome to React Router!" }
  ];
}

export function ErrorBoundary({ error }: Route.ErrorBoundaryProps) {
  // Error handling logic
}
```

#### Component Structure
```typescript
// ✅ Component file organization
// 1. Imports (React Router, types, local components)
// 2. Component definition
// 3. Route-specific exports (meta, ErrorBoundary)
// 4. Constants and utilities (if needed)

const resources = [
  {
    href: "https://example.com",
    text: "Link Text",
    icon: <SVGIcon />
  }
];
```

### File Naming Conventions

#### Route Files
```
app/routes/
├── home.tsx                 # ✅ kebab-case for route files
├── about-us.tsx            # ✅ kebab-case with hyphens
└── user.$id.tsx            # ✅ dynamic routes with $ prefix
```

#### Component Files
```
app/components/
├── Welcome.tsx             # ✅ PascalCase for reusable components
├── ui/                     # ✅ Feature grouping
│   ├── Button.tsx
│   └── Modal.tsx
└── welcome/                # ✅ Feature-specific grouping
    ├── welcome.tsx         # ✅ kebab-case for feature files
    ├── logo-dark.svg       # ✅ kebab-case for assets
    └── logo-light.svg
```

#### Configuration Files
```
root/
├── vite.config.ts          # ✅ kebab-case.ts for configs
├── tsconfig.json           # ✅ Standard config names
├── react-router.config.ts  # ✅ Framework-specific configs
└── package.json            # ✅ Standard package files
```

### CSS & Styling Standards

#### TailwindCSS Usage
```typescript
// ✅ Semantic class grouping
<main className="flex items-center justify-center pt-16 pb-4">
  
// ✅ Responsive design first
<div className="w-[500px] max-w-[100vw] p-4">

// ✅ Dark mode support
<img
  className="block w-full dark:hidden"
  alt="React Router"
/>

// ✅ State-based styling
<a className="group flex items-center gap-3 self-stretch p-3 leading-normal text-blue-700 hover:underline dark:text-blue-500">
```

#### CSS Class Organization
```typescript
// ✅ Logical grouping order:
// 1. Layout (flex, grid, position)
// 2. Sizing (w-, h-, max-, min-)
// 3. Spacing (p-, m-, gap-)
// 4. Typography (text-, font-, leading-)
// 5. Colors (text-, bg-, border-)
// 6. Effects (hover:, dark:, group-hover:)

className="flex items-center gap-3 p-3 text-blue-700 hover:underline dark:text-blue-500"
```

### Project Structure Standards

#### Directory Organization
```
app/
├── routes/                 # ✅ File-based routing
│   ├── home.tsx           # Route components
│   └── _layout.tsx        # Layout routes (if needed)
├── components/            # ✅ Reusable components (future)
│   ├── ui/               # Base UI components
│   └── features/         # Feature-specific components
├── welcome/              # ✅ Current feature grouping
│   ├── welcome.tsx       # Feature component
│   └── *.svg            # Feature assets
├── utils/                # ✅ Utility functions (future)
├── hooks/                # ✅ Custom React hooks (future)
└── root.tsx              # ✅ Application root
```

## Code Quality Standards

### Error Handling Patterns

#### Route-Level Error Boundaries
```typescript
// ✅ Comprehensive error boundary with environment awareness
export function ErrorBoundary({ error }: Route.ErrorBoundaryProps) {
  let message = "Oops!";
  let details = "An unexpected error occurred.";
  let stack: string | undefined;

  if (isRouteErrorResponse(error)) {
    message = error.status === 404 ? "404" : "Error";
    details = error.status === 404
      ? "The requested page could not be found."
      : error.statusText || details;
  } else if (import.meta.env.DEV && error && error instanceof Error) {
    details = error.message;
    stack = error.stack;
  }

  return (
    <main className="pt-16 p-4 container mx-auto">
      <h1>{message}</h1>
      <p>{details}</p>
      {stack && (
        <pre className="w-full p-4 overflow-x-auto">
          <code>{stack}</code>
        </pre>
      )}
    </main>
  );
}
```

#### Type-Safe Error Handling
```typescript
// ✅ Use React Router error response types
if (isRouteErrorResponse(error)) {
  // Handle route-specific errors
}

// ✅ Environment-specific error display
if (import.meta.env.DEV && error instanceof Error) {
  // Development error details
}
```

### Performance Standards

#### Asset Loading
```typescript
// ✅ Preload critical resources
export const links: Route.LinksFunction = () => [
  { rel: "preconnect", href: "https://fonts.googleapis.com" },
  {
    rel: "preconnect",
    href: "https://fonts.gstatic.com",
    crossOrigin: "anonymous",
  },
  {
    rel: "stylesheet",
    href: "https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap",
  },
];
```

#### Code Splitting
```typescript
// ✅ Route-based code splitting (automatic with React Router)
// ✅ Component-level splitting when needed (future)
const LazyComponent = React.lazy(() => import('./HeavyComponent'));
```

### Accessibility Standards

#### Semantic HTML
```typescript
// ✅ Use appropriate semantic elements
<main className="flex items-center justify-center pt-16 pb-4">
<header className="flex flex-col items-center gap-9">
<nav className="rounded-3xl border border-gray-200 p-6">
```

#### Alt Text and Labels
```typescript
// ✅ Descriptive alt text for images
<img
  src={logoLight}
  alt="React Router"
  className="block w-full dark:hidden"
/>

// ✅ Accessible link attributes
<a
  href={href}
  target="_blank"
  rel="noreferrer"
>
```

### Development Workflow Standards

#### Script Commands
```json
// ✅ Consistent npm script naming
{
  "scripts": {
    "build": "react-router build",
    "dev": "react-router dev",
    "start": "react-router-serve ./build/server/index.js",
    "typecheck": "react-router typegen && tsc"
  }
}
```

#### Environment Configuration
```typescript
// ✅ Environment-aware code
if (import.meta.env.DEV) {
  // Development-only code
}

// ✅ Environment variables access
const apiUrl = import.meta.env.VITE_API_URL;
```

## Commit and Documentation Standards

### Git Commit Messages
```bash
# ✅ Conventional commit format
feat: add new todo component
fix: resolve SSR hydration issue
docs: update README with deployment guide
refactor: extract common utility functions
style: update TailwindCSS class organization
test: add unit tests for welcome component
```

### Code Comments
```typescript
// ✅ Minimal comments for complex logic only
// Development vs production error handling strategy
if (import.meta.env.DEV && error && error instanceof Error) {
  details = error.message;
  stack = error.stack;
}

// ✅ JSDoc for exported functions (when needed)
/**
 * Generates meta tags for the route
 */
export function meta({}: Route.MetaArgs): MetaDescriptor[] {
  // Implementation
}
```

### Documentation Standards
- **README.md** - Clear setup and deployment instructions
- **Component docs** - JSDoc for complex components
- **API documentation** - When backend APIs are added
- **Deployment guides** - Platform-specific deployment steps