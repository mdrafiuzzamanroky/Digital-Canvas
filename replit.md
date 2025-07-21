# Footcap E-commerce Platform

## Overview

Footcap is a modern e-commerce platform specializing in premium sneakers. It's built as a full-stack web application with a React frontend, Express backend, and PostgreSQL database. The platform features user authentication, product catalog, shopping cart, wishlist functionality, order management, and payment processing through Stripe.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a monorepo structure with clear separation between client, server, and shared components:

- **Frontend**: React with TypeScript, using Vite as the build tool
- **Backend**: Express.js with TypeScript running on Node.js
- **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
- **Authentication**: Replit's OpenID Connect (OIDC) authentication system
- **UI Framework**: Radix UI components with Tailwind CSS for styling
- **Payment Processing**: Stripe integration for secure transactions
- **State Management**: TanStack Query for server state, React Context for cart state

## Key Components

### Frontend Architecture
- **Component Library**: Built on Radix UI primitives with shadcn/ui design system
- **Styling**: Tailwind CSS with custom theme variables and responsive design
- **Routing**: Wouter for lightweight client-side routing
- **Forms**: React Hook Form with Zod validation
- **State Management**: 
  - TanStack Query for API data fetching and caching
  - React Context for cart and UI state
- **Build Tool**: Vite with HMR support and Replit-specific plugins

### Backend Architecture
- **API Framework**: Express.js with TypeScript
- **Database Layer**: Drizzle ORM with PostgreSQL connection via Neon
- **Authentication**: Passport.js with OpenID Connect strategy
- **Session Management**: Express sessions with PostgreSQL store
- **Payment Integration**: Stripe SDK for payment processing
- **Middleware**: Custom logging, error handling, and authentication middleware

### Database Schema
The application uses a comprehensive relational schema including:
- **Users**: Authentication and profile data
- **Products**: Core product information with variants (size, color)
- **Cart Items**: User shopping cart persistence
- **Orders**: Complete order lifecycle management
- **Addresses**: User shipping and billing addresses
- **Wishlist**: User favorite products

## Data Flow

### Authentication Flow
1. Users authenticate via Replit's OIDC system
2. Session data stored in PostgreSQL with connect-pg-simple
3. Protected routes check authentication status
4. User profile data synchronized with local database

### Product Catalog Flow
1. Products stored with categories, brands, and variants
2. Frontend queries products with filtering and pagination
3. TanStack Query handles caching and background updates
4. Product images served via external URLs

### Shopping Cart Flow
1. Cart items stored both in React Context and database
2. Anonymous users get local storage persistence
3. Authenticated users get database persistence
4. Cart state synchronizes on authentication

### Order Processing Flow
1. Checkout form validates shipping and payment information
2. Stripe handles secure payment processing
3. Order confirmation creates database records
4. Cart cleared upon successful order completion

## External Dependencies

### Payment Processing
- **Stripe**: Handles all payment processing and PCI compliance
- **Stripe React Components**: Frontend integration for payment forms

### Database
- **Neon**: PostgreSQL hosting with serverless capabilities
- **Drizzle ORM**: Type-safe database operations with migrations

### Authentication
- **Replit Auth**: OIDC-based authentication system
- **Passport.js**: Authentication middleware for Express

### UI Components
- **Radix UI**: Accessible component primitives
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide Icons**: Icon library for consistent iconography

## Deployment Strategy

### Development Environment
- **Local Development**: `npm run dev` starts both client and server
- **Hot Module Replacement**: Vite provides instant updates during development
- **TypeScript Checking**: `npm run check` validates types across the monorepo

### Production Build
- **Client Build**: Vite bundles React application for production
- **Server Build**: esbuild compiles Express server to single file
- **Database Migrations**: Drizzle Kit handles schema changes
- **Environment Variables**: Database URL and session secrets required

### Architecture Decisions

**Monorepo Structure**: Chosen to share TypeScript types between client and server, reducing duplication and ensuring type safety across the full stack.

**Drizzle ORM**: Selected over Prisma for better TypeScript integration and more flexible query building, with automatic type inference from schema definitions.

**TanStack Query**: Implemented for sophisticated client-side caching, background updates, and optimistic updates, reducing server load and improving user experience.

**Wouter**: Lightweight routing library chosen over React Router for smaller bundle size and simpler API, suitable for the application's routing needs.

**Radix UI + Tailwind**: Combination provides accessible components with flexible styling, allowing for consistent design system while maintaining customization flexibility.

**Replit Auth**: Leverages platform-native authentication to reduce complexity and provide seamless integration with the Replit ecosystem.