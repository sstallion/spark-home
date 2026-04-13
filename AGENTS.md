# AGENTS Instructions

This file provides guidance to AI Agents when working with code in this repository.

## Development Commands

```bash
pnpm install      # Install dependencies (PNPM enforced via packageManager)
pnpm dev          # Start development server on http://localhost:3000
pnpm mock         # Start mock API server for testing service integrations
pnpm build        # Build for production
pnpm preview      # Preview production build
pnpm lint         # Run ESLint with auto-fix
```

## Architecture Overview

Spark Home is a static Vue.js 3 PWA dashboard that loads configuration from YAML files. The architecture is service-oriented with dynamic component loading.

### Core Application Structure

- **Entry Point**: `src/main.js` mounts the Vue app
- **Root Component**: `src/App.vue` handles layout, configuration loading, and routing
- **Configuration System**: YAML-based with runtime merging of defaults (`src/assets/defaults.yml`) and user config (`/assets/config.yml`)
- **Service Components**: Only `Generic.vue` (base layout) and `_error.vue` (async error fallback) remain in `src/components/services/`; upstream service integrations are not included in this build

### Service Integration Pattern

All service components follow this architecture:

- Extend `Generic.vue` using Vue slots (`<template #indicator>`, `<template #content>`, `<template #icon>`)
- Use the `service.js` mixin (`src/mixins/service.js`) for common API functionality
- Use a custom `fetch` method provided by the service mixin to seamlessly support proxy configuration, custom headers, and credentials.

### Configuration & Routing

- **Multi-page Support**: Hash-based routing without Vue Router
- **Dynamic Config Loading**: External URLs supported via `config.remote_config`
- **Theme System**: CSS layers architecture with three built-in themes in `src/assets/themes/`
- **Asset Management**: Static files served from `/assets/` with runtime configuration merging

### Build System Details

- **Vite 7**: Modern build tool with Vue plugin
- **PWA**: Auto-updating service worker via `vite-plugin-pwa`
- **SCSS**: Bulma framework with modular component styling
- **Docker**: Multi-stage build (Node.js → Alpine + Lighttpd)

### Development Notes

- Configuration changes require restart in development mode
- Themes use CSS custom properties for dynamic color switching
- The app has no backend dependencies and generates static files only
