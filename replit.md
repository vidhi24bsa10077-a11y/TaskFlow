# TaskFlow - Project & Task Management Platform

## Overview

TaskFlow is a full-stack web application for managing projects, tasks, and team collaboration. It provides real-time analytics, activity tracking, and role-based access control in a modern, responsive interface. The platform is built with TypeScript across the entire stack, emphasizing type safety and developer experience.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Core Framework**: React 18 with TypeScript, using functional components and hooks throughout. The application uses Vite as the build tool for fast development and optimized production builds.

**Routing**: Wouter is used as a lightweight client-side routing solution instead of heavier alternatives like React Router. Routes are defined in `client/src/App.tsx` with separate pages for dashboard, projects, tasks, and activity feeds.

**State Management**: 
- **Server State**: React Query (@tanstack/react-query) handles all server state, caching, and data synchronization. Custom query client configured in `client/src/lib/queryClient.ts` with disabled auto-refetching to reduce server load.
- **Local State**: React hooks (useState, useContext) for component-level state.
- **Form State**: React Hook Form with Zod validation for type-safe form handling.

**UI Component System**: Shadcn UI component library provides the base components, all customizable through Tailwind CSS. The design follows a "Linear + Asana hybrid" approach as documented in `design_guidelines.md`, emphasizing typography-driven hierarchy and information density.

**Styling**: Tailwind CSS with extensive theme customization defined in `tailwind.config.ts` and `client/src/index.css`. Custom CSS variables support light/dark themes with smooth transitions.

### Backend Architecture

**Server Framework**: Express.js running on Node.js, with separate entry points for development (`server/index-dev.ts`) and production (`server/index-prod.ts`). Development mode integrates Vite's middleware for hot module replacement.

**API Design**: RESTful API with resource-based endpoints:
- Authentication: `/api/auth/*`
- Projects: `/api/projects/*`
- Tasks: `/api/tasks/*`
- Activities: `/api/activities/*`
- Dashboard: `/api/dashboard/stats`

All routes defined in `server/routes.ts` with consistent error handling and activity logging.

**Authentication & Authorization**: 
- Passport.js with OpenID Connect strategy for Replit Auth integration
- Session-based authentication using express-session with PostgreSQL session store (connect-pg-simple)
- Sessions stored in database table for persistence across server restarts
- Middleware (`isAuthenticated`) protects all API routes requiring authentication

**Data Layer**: 
- **ORM**: Drizzle ORM provides type-safe database queries with full TypeScript support
- **Schema Definition**: Centralized in `shared/schema.ts` using Drizzle's schema builder
- **Storage Abstraction**: `server/storage.ts` implements an `IStorage` interface providing a clean separation between business logic and database operations

### Database Architecture

**Database**: PostgreSQL (Neon serverless) configured through environment variable `DATABASE_URL`.

**Connection Management**: Connection pooling via `@neondatabase/serverless` with WebSocket support for serverless environments.

**Schema Structure**:
- **users**: User profiles with role-based permissions (admin, manager, member)
- **projects**: Project entities with status tracking and ownership
- **tasks**: Task entities with priorities, due dates, assignees, and status
- **activities**: Audit trail of all system actions for transparency
- **projectMembers**: Many-to-many relationship between users and projects
- **sessions**: Session storage for authentication persistence

**Data Relationships**:
- Users own projects (one-to-many)
- Projects contain tasks (one-to-many)
- Users can be assigned to tasks (many-to-one)
- Users can be members of projects (many-to-many through projectMembers)
- All activities link to users (many-to-one)

**Type Safety**: Drizzle-Zod integration generates Zod schemas from database schema for runtime validation, ensuring end-to-end type safety from database to API to frontend.

### Build & Deployment

**Development**: 
- `npm run dev` starts development server with Vite HMR
- Backend and frontend run together with Vite middleware integration
- TypeScript compilation checked separately with `npm run check`

**Production**:
- `npm run build` compiles both frontend (Vite) and backend (esbuild)
- Frontend builds to `dist/public`
- Backend bundles to `dist/index.js` as ESM module
- `npm start` serves production build with static file serving

**Database Migrations**: Drizzle Kit manages schema migrations with `npm run db:push` for pushing schema changes directly to database.

## External Dependencies

### Third-Party Services

**Replit Auth (OpenID Connect)**: Primary authentication provider supporting Google, GitHub, and email login. Configuration through environment variables `ISSUER_URL` and `REPL_ID`.

**Neon Database**: Serverless PostgreSQL database accessed via `DATABASE_URL` environment variable. Uses WebSocket connections for serverless compatibility.

### Key NPM Packages

**UI & Styling**:
- `@radix-ui/*`: Unstyled, accessible component primitives (20+ packages for dialogs, dropdowns, menus, etc.)
- `tailwindcss`: Utility-first CSS framework
- `class-variance-authority`: Type-safe component variant management
- `lucide-react`: Icon library

**Data Visualization**:
- `recharts`: Charting library for analytics dashboard

**Forms & Validation**:
- `react-hook-form`: Performant form state management
- `@hookform/resolvers`: Integration with Zod validation
- `zod`: Runtime type validation and schema definition

**Database**:
- `drizzle-orm`: TypeScript ORM
- `drizzle-zod`: Schema to Zod conversion
- `@neondatabase/serverless`: Neon database client with WebSocket support

**Authentication**:
- `passport`: Authentication middleware
- `openid-client`: OpenID Connect implementation
- `express-session`: Session management
- `connect-pg-simple`: PostgreSQL session store

**Utilities**:
- `date-fns`: Date manipulation and formatting
- `memoizee`: Function result caching
- `wouter`: Lightweight routing

### Environment Variables Required

- `DATABASE_URL`: PostgreSQL connection string (Neon)
- `SESSION_SECRET`: Secret key for session encryption
- `REPL_ID`: Replit application identifier for auth
- `ISSUER_URL`: OpenID Connect issuer URL (defaults to Replit)
- `NODE_ENV`: Environment indicator (development/production)