# SCOR Level 1 Make - Simulation Game (SSG-Make)

## Overview

This is an educational simulation game focused on SCOR (Supply Chain Operations Reference) Level 1 Manufacturing processes. The application provides a serious game environment where teams of students collaborate in different roles to manage a virtual production line, making decisions about production planning, capacity engineering, lean/quality initiatives, and automation.

The game operates in rounds with different phases (design, simulating, reviewing) where players configure production parameters and observe the resulting KPIs (Key Performance Indicators) including OEE (Overall Equipment Effectiveness), throughput, and quality metrics.

## Current Status (December 2025)

**Working Features:**
- Landing page with team setup and role selection
- Game dashboard with production line visualization (4 workstations)
- OEE Dashboard showing Availability, Performance, Quality breakdown
- Simulation engine with deterministic KPI calculations
- Round progression through 5 round types
- Role-specific configuration modules (Production Planner, Capacity Engineer, Lean & Quality, Automation)

**Known Behaviors:**
- Session creation uses 3-second timeout for API calls, falls back to local session if API unavailable
- KPI calculations are deterministic (no random jitter) for reproducible results

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: 
  - React Query (@tanstack/react-query) for server state
  - React Context (GameContext) for game session state
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming (light/dark mode support)
- **Build Tool**: Vite with React plugin

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript (ESM modules)
- **API Pattern**: RESTful JSON API under `/api/*` routes
- **Development Server**: Vite middleware integration for HMR

### Data Layer
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Location**: `shared/schema.ts` (Zod schemas with type exports)
- **Current Storage**: In-memory storage implementation (`MemStorage` class)
- **Database Ready**: Drizzle configuration present for PostgreSQL migration

### Key Design Patterns
1. **Shared Types**: Schema definitions in `shared/` directory accessible by both client and server
2. **Role-Based Modules**: Separate React components for each team role (Production Planner, Capacity Engineer, Lean/Quality Engineer, Automation Engineer)
3. **Round-Based Gameplay**: Game sessions contain multiple rounds with distinct types (practice, baseline, lean_quality, automation, challenge)
4. **KPI Visualization**: Dedicated components for OEE dashboards, production line visualization, and round progress tracking

### Project Structure
```
├── client/src/          # React frontend
│   ├── components/      # UI components including role modules
│   ├── pages/           # Route pages (landing, game-dashboard)
│   ├── lib/             # Utilities, context providers, query client
│   └── hooks/           # Custom React hooks
├── server/              # Express backend
│   ├── routes.ts        # API endpoint definitions
│   ├── storage.ts       # Data storage abstraction
│   └── vite.ts          # Dev server integration
├── shared/              # Shared types and schemas
└── migrations/          # Drizzle database migrations
```

## External Dependencies

### Database
- **PostgreSQL**: Primary database (Drizzle ORM configured)
- **Connection**: Via `DATABASE_URL` environment variable
- **Session Store**: connect-pg-simple for Express sessions

### Frontend Libraries
- **Radix UI**: Accessible component primitives (dialogs, dropdowns, forms, etc.)
- **Recharts**: Data visualization for KPI charts
- **React Hook Form**: Form state management with Zod validation
- **Embla Carousel**: Carousel component
- **date-fns**: Date formatting utilities

### Backend Libraries
- **Express**: Web server framework
- **Drizzle ORM**: Database queries and migrations
- **Zod**: Schema validation (shared between client/server)
- **express-session**: Session management

### Development Tools
- **Vite**: Frontend build and dev server
- **esbuild**: Server bundling for production
- **TypeScript**: Type checking across the stack
- **Tailwind CSS**: Utility-first styling

### Replit-Specific
- **@replit/vite-plugin-runtime-error-modal**: Error overlay in development
- **@replit/vite-plugin-cartographer**: Development tooling
- **@replit/vite-plugin-dev-banner**: Development environment indicator