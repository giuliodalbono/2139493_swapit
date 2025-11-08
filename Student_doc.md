# SYSTEM DESCRIPTION:

The SwapIt project aims to create a platform that allows people to exchange skills and knowledge in a simple and immediate way. The main objective is to promote mutual learning, break down the economic barriers associated with education, and build an active and inclusive community.
SwapIt users will be able to offer their skills in exchange for other abilities they are interested in, without the need to use money.

# USER STORIES:

1) As a new user, I want to create an account and complete a short onboarding to set my interests and skills I can offer, so that I can access the platform's services.

2) As a registered user, I want to log in using my credentials, so that I can access my personal area and platform features.

3) As a registered user, I want to see the home page after login, so that I can quickly access matches, skill discovery, active chats, reviews, and my personal area.

4) As a registered user, I want to update my personal information and manage my skills, so that my profile reflects the correct information.

5) As a registered user, I want to search for skills or compatible partners, so that I can find skills of my interest to learn.

6) As a registered user, I want to be able to match with a partner who offers the skills that I want to learn, so that I can set up a meeting for the first lesson.

7) As a registered user, I want to view the history of my past matches and reviews, so that I can keep track of my activities.

8) As a registered user, I want to interact with other users via chat, so that I can understand better what they are offering and set up future meetings.

9) As a registered user, I want to see the upcoming sessions together with the completed sessions, so that I can prepare for the lessons.

10) As a registered user, I want to write a review rating another user’s skill and leaving a comment, so that other users can visualize my reviews and base their match better.



# CONTAINERS:

## CONTAINER_NAME: swapit-be

### DESCRIPTION:
Manage backend functionalities for User, Skill and Swap Proposal management.

### USER STORIES:
1) As a new user, I want to create an account and complete a short onboarding to set my interests and skills I can offer, so that I can access the platform's services.

2) As a registered user, I want to log in using my credentials, so that I can access my personal area and platform features.

3) As a registered user, I want to see the home page after login, so that I can quickly access matches, skill discovery, active chats, reviews, and my personal area.

4) As a registered user, I want to update my personal information and manage my skills, so that my profile reflects the correct information.

5) As a registered user, I want to search for skills or compatible partners, so that I can find skills of my interest to learn.

6) As a registered user, I want to be able to match with a partner who offers the skills that I want to learn, so that I can set up a meeting for the first lesson.

7) As a registered user, I want to view the history of my past matches and reviews, so that I can keep track of my activities.

9) As a registered user, I want to see the upcoming sessions together with the completed sessions, so that I can prepare for the lessons.

10) As a registered user, I want to write a review rating another user’s skill and leaving a comment, so that other users can visualize my reviews and base their match better.



### PORTS:
8080:8080

### DESCRIPTION:
Manage backend functionalities for User, Skill and Swap Proposal management.

### PERSISTENCE EVALUATION
The swapit-be container requires persistent storage to maintain details about the users and skills and swaps. It needs to store user-specific information, such as personal data and any associated skills or swaps attributed to that user. This data includes profile contact details like email and username.

### EXTERNAL SERVICES CONNECTIONS
The swapit-be container requires Kafka broker connection, and connection with the frontend container.

### MICROSERVICES:

#### MICROSERVICE: swapit-be
- TYPE: backend
- DESCRIPTION: Manages all backend functionalities including user management, skill catalog management (skills, skills desired, skills offered), swap proposal lifecycle management, feedback system, and Google Calendar integration for scheduling.
- PORTS: 8080
- TECHNOLOGICAL SPECIFICATION:
  The microservice is developed in Kotlin 1.9.25 and uses Spring Boot 3.5.3 framework.
  It uses the following libraries and technologies:
    - Spring Boot Starter Web: For building RESTful APIs
    - Spring Boot Starter Data JPA: For database interactions using JPA/Hibernate
    - Spring Boot Starter Actuator: For application monitoring and health checks
    - Spring Cloud Stream Kafka: For Kafka integration and event streaming
    - MySQL Connector/J: For MySQL database connectivity
    - Liquibase: For database schema versioning and migrations
    - SpringDoc OpenAPI: For Swagger API documentation
    - Google API Services Calendar: For Google Calendar integration
    - Google Auth Library OAuth2: For OAuth2 authentication with Google services
    - Kotlin Logging JVM: For logging functionality
    - Java 21: The application runs on Java 21 JRE
- SERVICE ARCHITECTURE:
  The service follows a layered architecture pattern:
    - Controllers: Handle HTTP requests and responses (UserController, SkillController, SwapProposalController, FeedbackController, CalendarController)
    - Services: Contain business logic (UserService, SkillService, SwapProposalService, FeedbackService, CalendarService, CloudEventService)
    - Repositories: Handle database operations using Spring Data JPA
    - DTOs: Data Transfer Objects for request and response handling
    - Entities: JPA entities representing database tables

- ENDPOINTS:

  | HTTP METHOD | URL                                               | Description                    | User Stories |
    	|-------------|---------------------------------------------------|--------------------------------|--------------|
  | GET         | /api/users                                        | Retrieve all users             | 5            |
  | GET         | /api/users/{uid}                                  | Get user by UID                | 4, 7         |
  | GET         | /api/users/email/{email}                          | Get user by email              | 4            |
  | POST        | /api/users                                        | Create new user                | 1            |
  | PUT         | /api/users/{uid}                                  | Update user                    | 4            |
  | DELETE      | /api/users/{uid}                                  | Delete user                    | 1            |
  | GET         | /api/users/{uid}/exists                           | Check if user exists           | 1            |
  | GET         | /api/users/email/{email}/exists                   | Check if email exists          | 1            |
  | GET         | /api/skills                                       | Retrieve all skills            | 5            |
  | GET         | /api/skills/{id}                                  | Get skill by ID                | 5            |
  | GET         | /api/skills/label/{label}                         | Get skill by label             | 5            |
  | GET         | /api/skills/labels/{label}                        | Get skills by label like       | 5            |
  | POST        | /api/skills                                       | Create new skill               | 4            |
  | PUT         | /api/skills/{id}                                  | Update skill                   | 4            |
  | DELETE      | /api/skills/{id}                                  | Delete skill                   | 4            |
  | GET         | /api/skills/desired                               | Get all skills desired         | 5            |
  | GET         | /api/skills/desired/{id}                          | Get skill desired by ID        | 5            |
  | GET         | /api/skills/desired/user/{userUid}                | Get skills desired by user     | 4            |
  | GET         | /api/skills/desired/skill/{skillId}               | Get users who desire a skill   | 5, 6         |
  | POST        | /api/skills/desired                               | Create new skill desired       | 1, 4         |
  | PUT         | /api/skills/desired/{id}                          | Update skill desired           | 4            |
  | DELETE      | /api/skills/desired/{id}                          | Delete skill desired           | 4            |
  | GET         | /api/skills/offered                               | Get all skills offered         | 5            |
  | GET         | /api/skills/offered/{id}                          | Get skill offered by ID        | 5            |
  | GET         | /api/skills/offered/user/{userUid}                | Get skills offered by user     | 4            |
  | GET         | /api/skills/offered/skill/{skillId}               | Get users who offer a skill    | 5, 6         |
  | POST        | /api/skills/offered                               | Create new skill offered       | 1, 4         |
  | PUT         | /api/skills/offered/{id}                          | Update skill offered           | 4            |
  | DELETE      | /api/skills/offered/{id}                          | Delete skill offered           | 4            |
  | GET         | /api/swap-proposals                               | Retrieve all swap proposals    | 6, 7         |
  | GET         | /api/swap-proposals/{id}                          | Get swap proposal by ID        | 6, 7         |
  | GET         | /api/swap-proposals/request-user/{requestUserUid} | Get proposals by request user  | 7            |
  | GET         | /api/swap-proposals/offer-user/{offerUserUid}     | Get proposals by offer user    | 7            |
  | GET         | /api/swap-proposals/status/{status}               | Get proposals by status        | 7            |
  | POST        | /api/swap-proposals                               | Create new swap proposal       | 6            |
  | PUT         | /api/swap-proposals/{id}                          | Update swap proposal           | 6            |
  | DELETE      | /api/swap-proposals/{id}                          | Delete swap proposal           | 6            |
  | GET         | /api/feedbacks                                    | Retrieve all feedbacks         | 7, 10        |
  | GET         | /api/feedbacks/{id}                               | Get feedback by ID             | 7, 10        |
  | GET         | /api/feedbacks/reviewer/{reviewerUid}             | Get feedbacks by reviewer      | 7, 10        |
  | GET         | /api/feedbacks/reviewed/{reviewedUid}             | Get feedbacks by reviewed user | 7, 10        |
  | POST        | /api/feedbacks                                    | Create new feedback            | 10           |
  | PUT         | /api/feedbacks/{id}                               | Update feedback                | 10           |
  | DELETE      | /api/feedbacks/{id}                               | Delete feedback                | 10           |
  | GET         | /api/gcalendar/events                             | Get all calendar events        | 9            |
  | POST        | /api/gcalendar/events                             | Create new calendar event      | 6, 9         |

- DB STRUCTURE:

  **_User_** :	| **_uid_** | version | email | username | profile_picture | creation_time | last_update |

  **_Skill_** :	| **_id_** | version | label | metadata | description | creation_time | last_update |

  **_SkillOffered_** :	| **_id_** | version | user_uid | skill_id | creation_time | last_update |

  **_SkillDesired_** :	| **_id_** | version | user_uid | skill_id | creation_time | last_update |

  **_SwapProposal_** :	| **_id_** | version | date | start_time | end_time | presentation_letter | status | creation_time | last_update | skill_offered_id | skill_requested_id | request_user_uid | offer_user_uid |

  **_Feedback_** :	| **_id_** | version | rating | review | creation_time | last_update | reviewer_uid | reviewed_uid |


#### MICROSERVICE: db-mysql
- TYPE: database
- DESCRIPTION: Manages persistent storage of User, Skill, Swap Proposal and Feedback data.
- PORTS: 3306

#### MICROSERVICE: zookeper
- TYPE: backend
- DESCRIPTION: Used for Kafka clusters coordination.
- PORTS: 2181

#### MICROSERVICE: kafka-broker
- TYPE: backend
- DESCRIPTION: Manages topics and events exchanged between backend microservices.
- PORTS: 9092

#### MICROSERVICE: schema-registry
- TYPE: backend
- DESCRIPTION: Centralized repository for kafka message schemas
- PORTS: 8085



# CONTAINERS:

## CONTAINER_NAME: swapit-frontend

### DESCRIPTION:
Manage frontend web app for all functionalities offered by the systems.

### USER STORIES:
1) As a new user, I want to create an account and complete a short onboarding to set my interests and skills I can offer, so that I can access the platform's services.

2) As a registered user, I want to log in using my credentials, so that I can access my personal area and platform features.

3) As a registered user, I want to see the home page after login, so that I can quickly access matches, skill discovery, active chats, reviews, and my personal area.

4) As a registered user, I want to update my personal information and manage my skills, so that my profile reflects the correct information.

5) As a registered user, I want to search for skills or compatible partners, so that I can find skills of my interest to learn.

6) As a registered user, I want to be able to match with a partner who offers the skills that I want to learn, so that I can set up a meeting for the first lesson.

7) As a registered user, I want to view the history of my past matches and reviews, so that I can keep track of my activities.

8) As a registered user, I want to interact with other users via chat, so that I can understand better what they are offering and set up future meetings.

9) As a registered user, I want to see the upcoming sessions together with the completed sessions, so that I can prepare for the lessons.

10) As a registered user, I want to write a review rating another user’s skill and leaving a comment, so that other users can visualize my reviews and base their match better.



### PORTS:
3000:3000

### DESCRIPTION:
Manage frontend web app for all functionalities offered by the systems.

### PERSISTENCE EVALUATION
The Authentication container does not require data persistence to manage token creation and validation.

### EXTERNAL SERVICES CONNECTIONS
The swapit-frontend container requires connection to Firebase external services and swapit-be, recommendation service, and chat containers.

### MICROSERVICES:

#### MICROSERVICE: swapit-frontend

- TYPE: frontend
- DESCRIPTION: Manages all frontend functionalities including user authentication and profile management, skill catalog management UI (skills, skills desired, skills offered), swap proposal lifecycle management UI, feedback and rating system UI, real-time chat messaging, notifications, and Google Calendar integration UI for scheduling.
- PORTS: 3000
- TECHNOLOGICAL SPECIFICATION:
  The microservice is developed in TypeScript 5 and uses Next.js 14.2.16 framework with React 18.
  It uses the following libraries and technologies:
    - Next.js: For building the React-based web application with App Router architecture
    - React 18: For building user interfaces and component-based architecture
    - TypeScript 5: For type-safe development
    - Tailwind CSS: For utility-first CSS styling
    - Firebase: For user authentication (Firebase Auth)
    - Socket.io-client: For real-time bidirectional communication and chat functionality
    - Lucide React: For icon components
- SERVICE ARCHITECTURE:
  The service follows a modern Next.js App Router architecture pattern:
    - App Directory: Contains route pages and layouts (app/page.tsx, app/dashboard/page.tsx, app/layout.tsx)
    - Components: Reusable UI components organized by feature
        - UI Components: Radix UI-based components in components/ui/
        - Feature Components: Business logic components
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


## CONTAINER_NAME: rec-service-lab-ap

### DESCRIPTION:
Manage recommendation capabilities for SwapIt through graph analytics and event-driven updates.

### USER STORIES:
5) As a registered user, I want to search for skills or compatible partners, so that I can find skills of my interest to learn.

6) As a registered user, I want to be able to match with a partner who offers the skills that I want to learn, so that I can set up a meeting for the first lesson.



### PORTS:
3002:3002

### DESCRIPTION:
Manage recommendation capabilities for SwapIt through graph analytics and event-driven updates.

### PERSISTENCE EVALUATION
The rec-service-lab-ap container requires persistent storage through the external Neo4j database, where all graph nodes and relationships are stored and continuously updated based on Kafka events.

### EXTERNAL SERVICES CONNECTIONS
The rec-service-lab-ap container requires connections to the Kafka broker, the swapit-be event producers, and the Neo4j database service.

### MICROSERVICES:

#### MICROSERVICE: rec-service-lab-ap
- TYPE: backend
- DESCRIPTION: Generates swap recommendations by consuming domain events, projecting them into Neo4j, and exposing REST endpoints for recommendation retrieval.
- PORTS: 3002
- TECHNOLOGICAL SPECIFICATION:
  The microservice is developed in NestJS 11 with TypeScript 5.7.
  It leverages the following libraries and technologies:
    - NestJS HTTP layer with controllers/services modules
    - KafkaJS and NestJS Microservices for Kafka consumers
    - Neo4j Driver and neo4j-query-builder for graph persistence
    - Axios for HTTP integrations with other services when needed
    - Swagger (NestJS) for API documentation
- SERVICE ARCHITECTURE:
  The service follows a modular NestJS architecture:
    - `RecommendationsModule`: Exposes the REST API (`RecommendationsController`, `RecommendationsService`)
    - `KafkaModule`: Handles Kafka consumers for skills, feedback, and swap proposals (`SkillConsumer`, `FeedbackConsumer`, `SwapProposalConsumer`)
    - `GraphModule`: Encapsulates repositories and entities for managing graph nodes and relationships (`GraphRepository`, `UserEntity`, `SkillEntity`)
    - `Neo4jModule`: Configures the Neo4j driver connection and session lifecycle
    - `HttpModule`: Provides reusable HTTP client capabilities for cross-service calls
- ENDPOINTS:

  | HTTP METHOD | URL                                          | Description                                       | User Stories |
    |-------------|----------------------------------------------|---------------------------------------------------|--------------|
  | GET         | /recommendations/swaps/{userUid}             | Retrieve swap recommendations for a given user    | 5, 6, 7      |

- EVENT STREAMS:
  | TOPIC              | Payloads Consumed                                | Purpose                                  |
  |--------------------|--------------------------------------------------|------------------------------------------|
  | swapit.skill.event | SkillEvent (skill created/updated/removed)       | Updates graph skill nodes and relations  |
  | swapit.feedback    | FeedbackEvent (ratings between users)            | Updates user popularity and trust scores |
  | swapit.swap.event  | SwapProposalEvent (swap lifecycle changes)       | Tracks relationships and swap outcomes   |

- GRAPH MODEL:
  Maintains `User` and `Skill` nodes with relationships (`OWNS`, `DESIRES`, `RATES`, `SWAPPED_WITH`) to power scoring algorithms (intelligent matching, popularity fallback, recency fallback).



## CONTAINER_NAME: chat-microservice

### DESCRIPTION:
Manage real-time and REST chat capabilities for SwapIt users with secure authentication and persistence.

### USER STORIES:

8) As a registered user, I want to interact with other users via chat, so that I can understand better what they are offering and set up future meetings.



### PORTS:
3001:3001

### DESCRIPTION:
Manage real-time and REST chat capabilities for SwapIt users with secure authentication and persistence.

### PERSISTENCE EVALUATION
The chat-microservice container requires persistent storage for message history in MongoDB and leverages Redis for real time message delivery.

### EXTERNAL SERVICES CONNECTIONS
The chat-microservice container connects to Firebase Authentication services, the swapit-frontend client applications, and potentially swapit-be for user metadata enrichment.

### MICROSERVICES:

#### MICROSERVICE: chat-microservice
- TYPE: backend
- DESCRIPTION: Provides authenticated chat APIs and Socket.IO gateway for real-time messaging, handling message persistence, delivery, and history retrieval.
- PORTS: 3001
- TECHNOLOGICAL SPECIFICATION:
  The microservice is built with NestJS 11 on Node.js 18 and TypeScript 5.7.
  It uses the following libraries and technologies:
    - NestJS REST controllers and Socket.IO gateway
    - Mongoose ODM for MongoDB integration
    - Redis client module for caching and pub/sub
    - Firebase Admin SDK for ID token verification
    - Swagger for REST documentation
- SERVICE ARCHITECTURE:
  Modular NestJS architecture with:
    - `ChatModule`: Aggregates the chat controller, service, and Schemas (`MessageSchema`) for REST operations
    - `ChatGateway`: Handles WebSocket events (`send`, `receive`, typing notifications) through Socket.IO
    - `AuthModule`: Provides authentication endpoints and guards (`FirebaseAuthGuard`) using Firebase Admin
    - `RedisModule`: Manages Redis connections for session and channel management
    - `AppModule`: Composes all modules and global providers
- ENDPOINTS:

  | HTTP METHOD | URL            | Description                                     | User Stories |
    |-------------|----------------|-------------------------------------------------|--------------|
  | GET         | /chat/{userId} | Retrieve chat threads for an authenticated user | 8            |

- WEBSOCKET EVENTS:
  | EVENT   | Direction | Description                               |
  |---------|-----------|-------------------------------------------|
  | send    | Client → Server | Emits a new message payload for delivery |
  | receive | Server → Client | Broadcasts delivered messages to user if online    |

- DATA MODEL:
  Messages are stored in MongoDB documents (`senderId`, `receiverId`, `content`, timestamps). Redis channels accelerate message delivery and online state, while Firebase ensures only authenticated users access chat capabilities.