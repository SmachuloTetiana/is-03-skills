# AGENTS.md

## Project Overview

Excalidraw is an open-source, collaborative virtual whiteboard for sketching hand-drawn-like diagrams. Built with React and TypeScript, it uses a custom Canvas 2D rendering engine and custom state management via `actionManager`.

## Tech Stack

- **Language**: TypeScript (strict mode)
- **UI**: React 19 (functional components, hooks only)
- **Build**: Vite
- **Testing**: Vitest + React Testing Library
- **Package Manager**: Yarn 1.x with workspaces
- **Linting**: ESLint + Prettier

## Project Structure

```
excalidraw-monorepo/
├── excalidraw-app/        # Vite-based web application
├── packages/
│   ├── excalidraw/        # Core library (@excalidraw/excalidraw)
│   │   ├── components/    # React UI components
│   │   ├── actions/       # State actions (actionManager)
│   │   ├── renderer/      # Canvas rendering pipeline
│   │   ├── scene/         # Scene management
│   │   └── types.ts       # Core type definitions (AppState)
│   ├── math/              # Math utilities (points, angles, vectors)
│   ├── element/           # Element types and operations
│   ├── common/            # Shared utilities
│   └── utils/             # General utilities
├── examples/              # Usage examples (Next.js, browser script)
└── dev-docs/              # Developer documentation
```

## Key Commands

- `yarn` — install dependencies
- `yarn start` — start dev server (excalidraw-app)
- `yarn build` — build the app
- `yarn test:app` — run Vitest tests
- `yarn test:typecheck` — TypeScript type checking
- `yarn test:code` — ESLint
- `yarn test:other` — Prettier check
- `yarn test:all` — run all checks
- `yarn fix` — auto-fix linting and formatting

## Architecture

- **State Management**: custom `actionManager` (NOT Redux/Zustand/MobX). State updates via `actionManager.dispatch()` only. State type: `AppState` in `packages/excalidraw/types.ts`.
- **Rendering**: Canvas 2D rendering via custom engine (NOT React DOM for drawing). Pipeline: Scene -> `renderScene()` -> canvas 2D context.
- **Monorepo**: Yarn workspaces with `@excalidraw/*` package aliases defined in `tsconfig.json`.

## Conventions

- Functional components with hooks only (no class components)
- Named exports only (no default exports)
- Props type: `{ComponentName}Props`
- Colocated tests: `ComponentName.test.tsx`
- TypeScript strict mode — no `any`, no `@ts-ignore`
- SCSS modules or CSS custom properties for styling
- kebab-case for utility files, PascalCase for components

## Skills

Agent skills provide specialized domain knowledge and refined workflows for high-quality outputs. Use the relevant skill when working on specific aspects of the project.

### Available Skills

#### 1. Creating Excalidraw Components
**Location**: `.agents/skills/creating-excalidraw-components/`

Creates React components following Excalidraw's established patterns and architecture. Use when adding new UI components, panels, dialogs, or toolbar items.

**Key points**:
- Functional components with hooks only (no class components)
- State updates via `actionManager` only
- Props interface pattern: `{ComponentName}Props`
- Colocated tests: `{ComponentName}.test.tsx`
- Use SCSS modules or CSS custom properties for styling
- Import types from `packages/excalidraw/types`

#### 2. Analyzing Bundle Size
**Location**: `.github/skills/analyzing-bundle-size/`

Analyzes bundle size, validates imports, and identifies large dependencies. Use when optimizing bundle size, reviewing PRs with new dependencies, or checking for unauthorized packages.

**Key points**:
- Run `scripts/check-imports.sh` to verify imports
- Run `scripts/analyze-deps.sh` for dependency analysis
- Forbidden dependencies: Redux, Zustand, MobX, Recoil, Jotai, react-konva, fabric.js, pixi.js, @mui/material, antd, chakra-ui
- Core library must use custom state management only

#### 3. Excalidraw Architecture
**Location**: `.github/skills/excalidraw-architecture/`

Explains Excalidraw's internal architecture, state flow, rendering pipeline, and monorepo structure. Use when understanding how the system works, making architectural decisions, or debugging state-related issues.

**Key points**:
- Monorepo with Yarn workspaces
- Custom `actionManager` for state (NOT Redux/Zustand/MobX)
- Canvas 2D rendering pipeline (NOT React DOM)
- Package structure: excalidraw, math, element, common, utils
- References: State Management, Rendering Pipeline guides

#### 4. Testing
**Location**: `.github/skills/test/`

Best practices and patterns for testing in the Excalidraw project using Vitest and React Testing Library.
