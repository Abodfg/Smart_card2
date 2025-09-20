# Overview

This is a Telegram bot application for digital charging services (شحن رقمي) built with Express.js backend and React frontend. The system consists of two separate Telegram bots - one for customers to browse and purchase digital products/services, and another for administrators to manage the system. The application supports Arabic language and uses Telegram Stars for payments.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture
- **React SPA**: Built with Vite as the build tool and development server
- **UI Framework**: shadcn/ui components with Radix UI primitives for accessible, composable components
- **Styling**: Tailwind CSS with CSS custom properties for theming
- **State Management**: React Query (TanStack Query) for server state management
- **Routing**: Wouter for lightweight client-side routing
- **Form Handling**: React Hook Form with Zod validation via @hookform/resolvers

## Backend Architecture
- **Express.js Server**: RESTful API with middleware for logging, error handling, and request parsing
- **Database Layer**: Drizzle ORM with PostgreSQL as the primary database
- **Bot Framework**: Telegraf for Telegram bot development with separate bot instances for users and admins
- **Session Management**: In-memory session storage for bot interactions using Map data structures
- **Service Layer**: Modular services for database operations, payments, and notifications

## Database Design
The schema includes hierarchical product organization:
- **Product Categories**: Main categories (e.g., "Game Charging", "Gift Cards")
- **Products**: Specific items within categories with shipping types (code/id/phone/email)
- **Categories**: Price tiers/variants for each product
- **Users**: Telegram user data with balance and order history
- **Orders**: Transaction records with status tracking
- **Balance Management**: Top-up requests and transaction logging

## Bot Architecture
- **Dual Bot System**: Separate bots for user interactions and admin management
- **User Bot Features**: Product browsing, order placement, balance checking, order history
- **Admin Bot Features**: Order management, user management, statistics dashboard, product management
- **Payment Integration**: Telegram Stars payment system with invoice generation and verification
- **Notification System**: Real-time notifications to admins for new orders and system events

## Configuration Management
- **Environment-based Config**: Centralized configuration with validation
- **Startup Checks**: Comprehensive validation of environment variables, bot tokens, and database connectivity
- **Error Handling**: Graceful error handling with user-friendly messages in Arabic

# External Dependencies

- **Database**: PostgreSQL with Neon Database serverless driver (@neondatabase/serverless)
- **ORM**: Drizzle ORM for type-safe database operations
- **Bot Platform**: Telegram Bot API via Telegraf framework
- **Payment Gateway**: Telegram Stars payment system
- **UI Components**: Radix UI primitives for accessible component foundation
- **Styling**: Tailwind CSS for utility-first styling
- **Build Tools**: Vite for fast development and optimized production builds
- **Development**: Replit-specific plugins for development environment integration