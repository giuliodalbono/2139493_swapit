#### MICROSERVICE: swapit-frontend

- TYPE: frontend

- DESCRIPTION: Manages all frontend functionalities including user authentication and profile management, skill catalog management UI (skills, skills desired, skills offered), swap proposal lifecycle management UI, feedback and rating system UI, real-time chat messaging, notifications, and Google Calendar integration UI for scheduling.

- PORTS: 3000 (default Next.js development port)

- TECHNOLOGICAL SPECIFICATION:

  The microservice is developed in TypeScript 5 and uses Next.js 14.2.16 framework with React 18.

  It uses the following libraries and technologies:

    - Next.js 14.2.16: For building the React-based web application with App Router architecture

    - React 18: For building user interfaces and component-based architecture

    - TypeScript 5: For type-safe development

    - Tailwind CSS 4.1.9: For utility-first CSS styling

    - Firebase 12.3.0: For user authentication (Firebase Auth)

    - Socket.io-client 4.8.1: For real-time bidirectional communication and chat functionality

    - Radix UI: Comprehensive set of accessible UI primitives (Accordion, Alert Dialog, Avatar, Checkbox, Dialog, Dropdown Menu, Popover, Select, Tabs, Toast, Tooltip, etc.)

    - React Hook Form 7.60.0: For form state management and validation

    - Zod 3.25.67: For schema validation

    - @hookform/resolvers 3.10.0: For integrating Zod with React Hook Form

    - Lucide React: For icon components

    - date-fns: For date manipulation and formatting

    - next-themes 0.4.6: For theme management (light/dark mode)

    - Sonner 1.7.4: For toast notifications

    - Recharts 2.15.4: For data visualization and charts

    - Vercel Analytics: For application analytics

    - Geist Font: For typography (Geist Sans and Geist Mono)

- SERVICE ARCHITECTURE:

  The service follows a modern Next.js App Router architecture pattern:

    - App Directory: Contains route pages and layouts (app/page.tsx, app/dashboard/page.tsx, app/layout.tsx)

    - Components: Reusable UI components organized by feature
      - UI Components: Radix UI-based components in components/ui/ (Button, Card, Dialog, Input, Select, etc.)
      - Feature Components: Business logic components (auth-modal.tsx, dashboard.tsx, skill-matcher.tsx, swap-proposals.tsx, chat-section.tsx, notifications.tsx, profile-setup.tsx, rating-modal.tsx, create-swap-modal.tsx, skill-catalog.tsx)

    - Hooks: Custom React hooks for state management and side effects
      - use-auth.tsx: Authentication context and user management
      - use-toast.ts: Toast notification management
      - use-mobile.ts: Responsive design utilities

    - Lib: Core business logic and API integrations
      - api.ts: REST API client for backend communication (user management, skills, swap proposals, feedback, Google Calendar)
      - firebase.ts: Firebase configuration and authentication setup
      - chatClient.ts: Socket.io client for real-time chat functionality
      - utils.ts: Utility functions

    - Styles: Global CSS and styling configuration
      - globals.css: Global styles and Tailwind CSS configuration

    - Public: Static assets (images, logos, placeholders)



