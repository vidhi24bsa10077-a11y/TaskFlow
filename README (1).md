# TaskFlow - Project & Task Management Platform

A comprehensive, full-stack web application for managing projects, tasks, and team collaboration with real-time analytics and activity tracking.

## 🌟 Features

### Core Functionality
- **User Authentication** - Secure login/logout with Replit Auth (supports Google, GitHub, email)
- **Project Management** - Create, update, and organize projects with status tracking
- **Task Management** - Comprehensive task system with priorities, due dates, and status updates
- **Analytics Dashboard** - Real-time charts and metrics showing productivity insights
- **Activity Feed** - Complete audit trail of all user actions and system events
- **Role-Based Access** - User roles (Admin, Manager, Member) with appropriate permissions

### User Experience
- **Responsive Design** - Fully optimized for desktop, tablet, and mobile devices
- **Dark Mode Support** - Toggle between light and dark themes
- **Real-time Updates** - Instant UI updates using React Query
- **Professional UI** - Clean, modern interface inspired by Linear and Asana
- **Comprehensive Error Handling** - User-friendly error messages and validation

## 🛠️ Technologies Used

### Frontend
- **React 18** - Modern UI library with hooks and functional components
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **Shadcn UI** - High-quality React component library
- **Wouter** - Lightweight routing solution
- **React Query** - Server state management and caching
- **React Hook Form** - Performant form handling with validation
- **Recharts** - Data visualization library for analytics
- **Lucide React** - Beautiful icon system

### Backend
- **Express.js** - Fast, minimalist web framework
- **PostgreSQL** - Robust relational database (Neon-backed)
- **Drizzle ORM** - TypeScript ORM for database operations
- **Passport.js** - Authentication middleware
- **Zod** - Runtime type validation

### Development Tools
- **Vite** - Next-generation frontend build tool
- **TypeScript** - Static type checking
- **ESBuild** - Fast JavaScript bundler

## 📋 Installation & Setup

### Prerequisites
- Node.js 20+ installed
- PostgreSQL database (provided by Replit)

### Steps

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd taskflow
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   The following environment variables are automatically configured:
   - `DATABASE_URL` - PostgreSQL connection string
   - `SESSION_SECRET` - Session encryption key
   - `REPL_ID` - Replit authentication ID
   - `ISSUER_URL` - OAuth issuer URL

4. **Push database schema**
   ```bash
   npm run db:push
   ```

5. **Start the development server**
   ```bash
   npm run dev
   ```

6. **Access the application**
   Open your browser and navigate to `http://localhost:5000`

## 🧪 Testing

### Manual Testing
1. **Login Flow**
   - Click "Log In" button on landing page
   - Complete authentication via Replit Auth
   - Verify redirect to dashboard

2. **Create Project**
   - Navigate to Projects page
   - Click "New Project"
   - Fill in project details and submit
   - Verify project appears in project list

3. **Create Task**
   - Navigate to Tasks page
   - Click "New Task"
   - Fill in task details and submit
   - Verify task appears in task list

4. **View Analytics**
   - Navigate to Dashboard
   - Verify charts display correct data
   - Check metric cards show accurate counts

5. **Activity Tracking**
   - Perform various actions (create project, update task)
   - Navigate to Activity page
   - Verify all actions are logged

## 📁 Project Structure

```
├── client/                 # Frontend application
│   ├── public/            # Static assets
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   │   ├── ui/       # Shadcn UI components
│   │   │   ├── app-sidebar.tsx
│   │   │   ├── theme-provider.tsx
│   │   │   └── theme-toggle.tsx
│   │   ├── hooks/        # Custom React hooks
│   │   │   ├── useAuth.ts
│   │   │   └── use-toast.ts
│   │   ├── lib/          # Utility functions
│   │   │   ├── authUtils.ts
│   │   │   ├── queryClient.ts
│   │   │   └── utils.ts
│   │   ├── pages/        # Application pages
│   │   │   ├── dashboard.tsx
│   │   │   ├── projects.tsx
│   │   │   ├── project-detail.tsx
│   │   │   ├── tasks.tsx
│   │   │   ├── activity.tsx
│   │   │   ├── landing.tsx
│   │   │   └── not-found.tsx
│   │   ├── App.tsx       # Root component with routing
│   │   ├── main.tsx      # Application entry point
│   │   └── index.css     # Global styles
│   └── index.html        # HTML template
├── server/                # Backend application
│   ├── db.ts             # Database connection
│   ├── storage.ts        # Data access layer
│   ├── routes.ts         # API route handlers
│   ├── replitAuth.ts     # Authentication setup
│   ├── app.ts            # Express app configuration
│   ├── index-dev.ts      # Development server
│   └── index-prod.ts     # Production server
├── shared/               # Shared code between client and server
│   └── schema.ts         # Database schema and types
├── package.json          # Project dependencies
├── tsconfig.json         # TypeScript configuration
├── tailwind.config.ts    # Tailwind CSS configuration
├── vite.config.ts        # Vite configuration
└── drizzle.config.ts     # Drizzle ORM configuration
```

## 🎯 Non-Functional Requirements

### 1. Security
- Secure authentication using OAuth 2.0
- Password-less login via trusted providers
- Session-based authentication with encrypted cookies
- SQL injection prevention via parameterized queries
- XSS protection through React's built-in escaping

### 2. Performance
- Optimistic UI updates for instant feedback
- Efficient database queries with proper indexing
- Client-side caching with React Query
- Code splitting for faster initial load
- Lazy loading of components

### 3. Usability
- Intuitive navigation with sidebar
- Clear visual hierarchy
- Responsive design for all devices
- Helpful error messages
- Loading states for async operations

### 4. Reliability
- Comprehensive error handling
- Database transaction support
- Graceful degradation
- Form validation (client and server-side)

### 5. Maintainability
- TypeScript for type safety
- Modular code organization
- Clear separation of concerns
- Consistent coding standards
- Comprehensive comments

### 6. Scalability
- Database-backed persistence
- Stateless API design
- Horizontal scaling capability
- Connection pooling

## 🚀 Deployment

The application can be deployed to any platform supporting Node.js:

1. **Replit** (Recommended)
   - Click "Publish" in the Replit interface
   - Application automatically deploys with database and secrets

2. **Other Platforms**
   - Set environment variables
   - Run `npm run build`
   - Start production server with `npm run prod`

## 📊 Database Schema

### Tables
- **users** - User profiles and authentication
- **projects** - Project information and status
- **tasks** - Task details with priorities and deadlines
- **project_members** - Many-to-many relationship for team members
- **activities** - Audit log of all user actions
- **sessions** - User session storage

### Key Relationships
- Users own Projects (one-to-many)
- Projects have Tasks (one-to-many)
- Tasks are assigned to Users (many-to-one)
- Projects have Members (many-to-many)
- Users create Activities (one-to-many)

## 🤝 Contributing

This is an academic project for VITyarthi coursework.

## 📄 License

This project is created for educational purposes as part of the VITyarthi Build Your Own Project assignment.

## 👥 Author

Created by [Your Name] for [Course Name] - [Academic Year]

## 🙏 Acknowledgments

- Built with Replit's full-stack template
- UI inspired by Linear and Asana
- Shadcn UI for component library
- Replit team for authentication and database services
