# Feature-Based Next.js Starter Template

A modular, clean-slate starter template for modern [Next.js](https://nextjs.org/) applications. Built with **Next.js 16 (App Router)**, **React 19**, and **Tailwind CSS 4**, this template organizes code around a **Feature-Based Design Architecture** and provides a curated collection of pre-installed, popular libraries to jumpstart development without boilerplate clutter.

---

## Table of Contents

- [Overview & Purpose](#overview--purpose)
- [Key Highlights](#key-highlights)
- [Architecture: Feature-Based Design](#architecture-feature-based-design)
- [Pre-Installed Libraries](#pre-installed-libraries)
- [Flexible & Removable Dependencies](#flexible--removable-dependencies)
- [Built-In Configurations](#built-in-configurations)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)

---

## Overview & Purpose

Setting up a new Next.js project often involves repetitive tasks: deciding on a folder structure, configuring path aliases, whitelisting image sources for rapid prototyping, installing common utilities (HTTP clients, state managers, notification tools), and stripping away demo boilerplate.

This template solves that friction by providing:
1. **A clear architectural convention** centered on domain features rather than scattered technical layers.
2. **A battle-tested set of pre-installed dependencies** for state management, data fetching, and user interface components.
3. **A clean, unpolluted foundation** (`src/app/page.js` is minimal and ready for your code) with zero lock-in.

---

## Key Highlights

- **Feature-Based Architecture**: Code is grouped by business domain inside `src/features/`, keeping components, hooks, services, and state co-located and maintainable as the project scales.
- **Curated Dependency Suite**: Pre-installed support for global client state, server state management, HTTP requests, UI selects, icons, and notifications.
- **100% Modular & Removable**: Pre-installed packages are completely decoupled. Remove any library you do not need with a single `npm uninstall` command without breaking template integrity.
- **Developer-Friendly Image Whitelisting**: `next.config.mjs` allows images from any remote source during local development (`NODE_ENV === "development"`), while keeping production builds secure.
- **Next.js 16 & React 19 Ready**: Built with the latest App Router foundation, optimized Geist fonts, and Tailwind CSS 4 via Turbopack.
- **Docker Ready**: Includes `Dockerfile`, `Dockerfile.dev`, `docker-compose.yml`, and `docker-compose.dev.yml` out of the box.

---

## Architecture: Feature-Based Design

Rather than separating an application purely by technical layers (e.g., placing all components in one global folder, all hooks in another, and all API calls in a third), this template adopts a **Feature-Based Design Architecture**.

### Why Feature-Based?

In traditional layer-based structures, working on a single feature requires jumping across multiple directories spread across the repository. As applications grow, maintaining and refactoring domain logic becomes error-prone.

In a Feature-Based architecture:
- Related code for a single domain capability lives together inside `src/features/<feature-name>/`.
- Features maintain their own components, state slices, hooks, and services.
- The `src/app/` directory focuses strictly on routing, layouts, and page orchestration, delegating business logic to corresponding features.

### Recommended Feature Structure

When creating a new feature under `src/features/<feature-name>/`, follow this modular convention:

```text
src/features/<feature-name>/
├── components/          # UI components specific to this feature
├── hooks/               # Custom hooks used within this feature
├── services/            # API queries, mutations, and HTTP calls
├── slices/              # Feature state (e.g., Redux Toolkit slices)
└── index.js             # Public API / barrel export for the feature
```

---

## Pre-Installed Libraries

The template comes with essential libraries pre-installed to cover standard requirements for modern web applications:

### 1. State Management
- **[@reduxjs/toolkit](https://redux-toolkit.js.org/) (`^2.13.0`)**: The official, opinionated standard for Redux logic. Simplifies store setup, reducer definitions, and immutable updates.
- **[react-redux](https://react-redux.js.org/) (`^9.3.1`)**: Official React bindings to connect your components to the Redux store.

### 2. Server State & Data Fetching
- **[@tanstack/react-query](https://tanstack.com/query/latest)** (`^5.105.1`): Declarative, asynchronous server-state management for fetching, caching, synchronizing, and updating server data in React.
- **[axios](https://axios-http.com/) (`^1.21.0`)**: Promise-based HTTP client for the browser and Node.js with built-in request/response interceptors, JSON serialization, and cancellation.

### 3. UI Components & Presentation
- **[react-icons](https://react-icons.github.io/react-icons/) (`^5.7.0`)**: Extensive collection of popular SVG icon sets (FontAwesome, Material Design, Feather, etc.) importable as lightweight React components.
- **[react-select](https://react-select.com/) (`^5.10.2`)**: Flexible, accessible select/dropdown control supporting multi-select, search filtering, and asynchronous data loading.
- **[react-toastify](https://fkhadra.github.io/react-toastify/) (`^11.2.0`)**: Toast notification system providing customizable, non-blocking alert banners.

### 4. Styling & Build Engine
- **[tailwindcss](https://tailwindcss.com/) (`^4.0.0`)**: Utility-first CSS framework configured via modern `@import "tailwindcss";` in `globals.css`.
- **[@tailwindcss/turbopack](https://www.npmjs.com/package/@tailwindcss/turbopack)**: Turbopack CSS loaders configured for fast development builds.

---

## Flexible & Removable Dependencies

All included libraries are **optional**. No tightly coupled runtime wrappers or mandatory boilerplate code have been injected into `src/app/layout.js` or `src/app/page.js`.

If a library is not needed for your project, simply uninstall it:

```bash
# Example: Remove Redux if using a different state manager
npm uninstall @reduxjs/toolkit react-redux

# Example: Remove React Select or React Toastify if using custom UI components
npm uninstall react-select react-toastify
```

The template leaves you with full architectural freedom without needing to untangle unwanted integrations.

---

## Built-In Configurations

### 1. Development-Only Image Wildcard (`next.config.mjs`)
Next.js requires explicit domain whitelisting to serve external images via `next/image`. To simplify prototyping and working with dynamic external sources during development, `next.config.mjs` allows all HTTP and HTTPS image sources when `process.env.NODE_ENV === "development"`:

```javascript
const isDev = process.env.NODE_ENV === "development";

const nextConfig = {
  images: {
    remotePatterns: isDev
      ? [
          { protocol: "https", hostname: "**" },
          { protocol: "http", hostname: "**" },
        ]
      : [],
  },
  turbopack: {
    rules: {
      "*.css": {
        loaders: ["@tailwindcss/turbopack"],
        as: "*.css",
      },
    },
  },
};
```

In production builds, `remotePatterns` defaults to an empty array so you can define strictly authorized production hostnames.

### 2. Path Aliases (`jsconfig.json`)
The project provides root path aliasing configured via `jsconfig.json`:
- `@/*` points directly to `./src/*`

This allows clean imports from any subfolder:
```javascript
import { MyFeatureComponent } from "@/features/my-feature";
```

### 3. Containerization
The template includes standard Docker configurations for both development and production workflows:
- `Dockerfile.dev` & `docker-compose.dev.yml`: Volume-mounted development environment with hot-reloading.
- `Dockerfile` & `docker-compose.yml`: Production multi-stage build container.

---

## Project Structure

```text
.
├── docker-compose.dev.yml     # Docker Compose configuration for development
├── docker-compose.yml         # Docker Compose configuration for production
├── Dockerfile                 # Production Docker build definition
├── Dockerfile.dev             # Development Docker build definition
├── eslint.config.mjs          # Flat ESLint configuration with Next.js Core Web Vitals
├── jsconfig.json              # Path alias mapping (@/* -> ./src/*)
├── next.config.mjs            # Next.js configuration (Dev image wildcard & Turbopack)
├── package.json               # Dependencies and build scripts
├── public/                    # Static public assets (SVG icons, etc.)
└── src/
    ├── app/                   # Next.js App Router (Routes & Layouts)
    │   ├── favicon.ico
    │   ├── globals.css        # Global Tailwind CSS imports
    │   ├── layout.js          # Root layout with Geist font optimization
    │   └── page.js            # Minimal starter page (blank canvas)
    └── features/              # Feature-Based modules root
```

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (version 20 or higher recommended)
- [npm](https://www.npmjs.com/) (or `pnpm` / `yarn` / `bun`)

### 1. Clone & Install Dependencies

```bash
git clone <repository-url> my-next-app
cd my-next-app
npm install
```

### 2. Run the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

### 3. Build for Production

```bash
npm run build
npm run start
```

### 4. Running with Docker (Optional)

To start the local development environment inside Docker:

```bash
docker compose -f docker-compose.dev.yml up
```

---

## Available Scripts

| Command | Description |
| :--- | :--- |
| `npm run dev` | Starts the Next.js development server with Turbopack. |
| `npm run build` | Compiles the production build. |
| `npm run start` | Runs the compiled production server. |
| `npm run lint` | Runs ESLint to verify code quality and rule conformance. |

---

## License

This starter template is open source and free to use for personal and commercial projects.
