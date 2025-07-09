# replit.md

## Overview

This is a full-stack TypeScript chat application built with React, Express, and PostgreSQL. The application features a modern chat interface powered by OpenAI's GPT-4o model, with FaithJayBot as the AI assistant. The architecture follows a monorepo structure with shared schemas and clean separation between frontend and backend concerns.

## Recent Changes

### July 2025 - Enhanced FaithJayBot Features
- **OpenAI Model Upgrade**: Upgraded from GPT-3.5-turbo to GPT-4o for better responses
- **Error Handling**: Added fallback message "I'm temporarily offline. Please try again shortly 🙏🏽" for API quota/billing issues
- **Dark Mode**: Implemented complete dark/light theme switching with smooth transitions
- **Custom Logo**: Added FaithJayBot branded logo with circular styling and web3 glow effects
- **Enhanced UI**: Improved mobile responsiveness and smooth scroll animations
- **Welcome Message**: Added persistent welcome message on page load
- **Creator Attribution**: Added special handling for questions about creator/developer
- **Footer Enhancement**: Added attribution footer with Revelation 14 Family branding and website link
- **Watery-Dark Theme**: Enhanced header/footer with elegant dark blue glass effect and blur backdrop
- **Auto-Typed Intro**: Added 3-message intro sequence that auto-types on page load with delays
- **Web3 Aesthetics**: Improved visual design with modern glass-morphism effects
- **Database Integration**: Added LowDB-based chat history storage with session management
- **Export Functionality**: Users can export last 10 messages as downloadable .txt or .json files
- **Session Management**: Automatic session ID generation and persistence via localStorage
- **Authentication System**: Added complete login system with email/password authentication
- **Sign-Up Flow**: Created comprehensive user registration with full name, email, password validation
- **Session Persistence**: User authentication state maintained via localStorage with "Remember Me" option
- **Personalized Greetings**: Welcome messages include user's first name after login/signup
- **Logout Functionality**: Clean logout with session clearing and toast notifications
- **User Management**: LocalStorage-based user database for demo purposes with duplicate email prevention

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Styling**: Tailwind CSS with shadcn/ui component library
- **Build Tool**: Vite with hot module replacement
- **State Management**: TanStack Query for server state management
- **Routing**: Wouter for lightweight client-side routing
- **UI Components**: Radix UI primitives with custom styling

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **API Design**: RESTful endpoints with JSON communication
- **Session Management**: Built-in session handling with connect-pg-simple
- **Development**: Development server with automatic restarts using tsx

### Database Strategy
- **Primary Database**: PostgreSQL (configured via Drizzle)
- **ORM**: Drizzle ORM for type-safe database operations
- **Migration Strategy**: Drizzle Kit for schema migrations
- **Development Fallback**: In-memory storage implementation for development
- **Chat History Storage**: LowDB JSON file-based database for persistent chat history
- **Database Location**: `chat_history.json` in project root directory

## Key Components

### Database Schema
- **Users Table**: Basic user authentication with username/password
- **Messages Table**: Chat message storage with role-based classification (user/assistant)
- **Shared Schema**: Type-safe schema definitions using Drizzle and Zod validation

### API Endpoints
- `POST /api/chat`: Send user messages and receive AI responses (with optional sessionId)
- `GET /api/messages`: Retrieve chat history from memory storage
- `GET /api/export/:sessionId`: Export chat history as downloadable .txt or .json file
- `GET /api/stats`: Get database statistics (total messages and sessions)
- Error handling with structured JSON responses

### Frontend Pages
- **Chat Interface**: Main chat page with real-time messaging
- **404 Page**: Standard not found page
- **UI Components**: Comprehensive component library built on Radix UI

### External Service Integration
- **OpenAI Integration**: GPT-4o for chat completions with fallback error handling
- **Neon Database**: PostgreSQL hosting service
- **Environment Configuration**: API keys and database URLs via environment variables

## Data Flow

1. **User Input**: User types message in chat interface
2. **Client Processing**: React Query manages API calls and state
3. **Server Processing**: Express server validates input and stores user message
4. **AI Integration**: OpenAI API generates response using GPT-3.5-turbo
5. **Database Storage**: Both user and AI messages stored in PostgreSQL
6. **Real-time Updates**: Client refetches messages to display conversation

## External Dependencies

### Production Dependencies
- **Database**: @neondatabase/serverless, drizzle-orm, connect-pg-simple
- **AI Service**: OpenAI API integration
- **UI Framework**: React ecosystem with Radix UI components
- **Validation**: Zod for schema validation
- **HTTP Client**: Built-in fetch with TanStack Query

### Development Dependencies
- **Build System**: Vite with React plugin
- **TypeScript**: Full type checking and compilation
- **Development Tools**: tsx for server development, esbuild for production builds

## Deployment Strategy

### Build Process
1. **Frontend Build**: Vite builds React app to `dist/public`
2. **Backend Build**: esbuild bundles server code to `dist/index.js`
3. **Database Setup**: Drizzle migrations applied via `db:push` command

### Environment Configuration
- **Development**: Local development with in-memory storage fallback
- **Production**: PostgreSQL database with OpenAI API integration
- **Required Variables**: DATABASE_URL, OPENAI_API_KEY

### Server Architecture
- **Static Assets**: Express serves built React app
- **API Routes**: RESTful endpoints under `/api` prefix
- **Error Handling**: Centralized error middleware with structured responses
- **Logging**: Request/response logging for API endpoints

The application is designed to be easily deployable on platforms like Replit, with automatic environment detection and graceful fallbacks for development scenarios.