Promixa: AI-Powered Transcription Platform - Technical Documentation
[promixa.me](https://promixa.me/)
1. Introduction & Project Goal
Promixa (promixa.me) is an AI-powered platform designed to provide users with advanced audio and video transcription services. Future plans include adding AI image generation features. The application is built using modern web technologies with a secure and scalable architecture.

While the frontend provides a user-friendly interface with the help of AI-assisted development, the core focus during development has been on building a robust, scalable, and efficient backend system, showcasing advanced backend engineering skills.

2. System Architecture Overview
The project utilizes a decoupled architecture with separate frontend and backend components:

Frontend: Developed with Next.js (v15+, App Router), TypeScript, React (v19+), and Tailwind CSS (v4+), hosted on Vercel (promixa.me). State management uses React Context API, and UI incorporates custom components similar to Shadcn/ui. Frontend development was significantly assisted by AI tools.
Backend: A Java 17 Spring Boot (v3.4+) application responsible for API endpoints, business logic (user management, transcription routing), database operations, authentication/authorization, and communication with external services (Deepgram, AssemblyAI). Hosted on AWS EC2 (Ubuntu Linux) using the Free Tier.
Database: PostgreSQL hosted on AWS RDS, storing persistent data including user information, roles, authentication details, trial status, and usage statistics.
Communication & Security: The frontend communicates with the backend API (https://api.promixa.me) via HTTP requests (RESTful). Authentication is handled with HttpOnly Cookie-based JWT. Cloudflare is used to manage DNS settings and mitigate security issues with HTTP requests.
3. Deployment Journey & Strategy
Achieving a cost-effective and reliable production deployment was a key learning objective. The journey involved several iterations:

Render & Free Services: Initial trials were conducted on Render, a free hosting service. While functional, various challenges led to exploring alternative solutions.
AWS Challenges: Migrating to AWS presented its own set of challenges, particularly resource constraints when working with the Free Tier and configuration issues that needed to be resolved.
EC2 & Ubuntu Linux: Through careful configuration and optimization, a stable deployment was achieved on AWS EC2 using Ubuntu Linux, providing a balance of performance and cost-effectiveness while staying within Free Tier limits.
Cloudflare Security: Cloudflare integration was implemented to manage DNS settings and enhance security, enabling better control over HTTP requests and providing an additional layer of protection.
4. Backend Deep Dive
Technology Stack: Technology Stack: Java 17, Spring Boot (v3.4+), Spring Security (JWT, OAuth2 Client, BCrypt), Spring Data JPA, Hibernate, Spring WebFlux WebClient, Lombok, Spring Boot Actuator, Spring Validation, Maven.

Dual-API Transcription Strategy: Recognizing that no single API excels at all languages, Promixa implements a dynamic approach:
Deepgram: Deepgram: Utilizes the Nova-3 model for supported languages (e.g., English) in audio transcription. For video transcription, where Nova-3 support is lacking, it uses Deepgram's Nova-2 model.
AssemblyAI: AssemblyAI: Employed for languages where it offers better accuracy compared to Deepgram models, such as Turkish, and for automatic language detection using Direct API Streaming.
The backend intelligently routes transcription requests to the appropriate API based on the selected language, optimizing accuracy and performance.

Database: Database: Leverages AWS RDS PostgreSQL for storing user data, authentication details, transcription metadata, and usage tracking information.

Infrastructure: Infrastructure: Runs on AWS EC2 using Ubuntu Linux (Free Tier), providing a stable environment for learning and development purposes.

5. User Management & Authentication
The platform offers comprehensive user management features:

Registration: Registration: Users can sign up with Email/Password or Google accounts (OAuth2).
Authentication: Authentication: JWT-based authentication with secure HttpOnly Cookies (auth_token).
Authorization: Authorization: Role-based authorization (@PreAuthorize annotations on backend, protected routes with withAuth HOC on frontend).
Profile: User Profile: Dashboard for viewing account details with the ability to update name and password (for email/password users only).
Trial System: Trial System: New users receive a 30-day trial period with active tracking of trial status and usage limitations.
6. Frontend Overview
The frontend, built with Next.js, React, and Tailwind CSS, provides the user interface for file uploads, language selection, and displaying transcription results. While functional and responsive, its development utilized AI-assisted development approaches as the main focus remained on the backend implementation.

Key features include separate file handling for audio and video tabs, an organized language selection dropdown with specific display order, and a clean user interface that simplifies the transcription process.

7. Recent Improvements & Current Status
The project has undergone several significant improvements to enhance stability and security:

Authentication Flow: Authentication Flow: Backend logout integration, API cookie handling improvements, and enhanced redirect functionality after login.
State Management: State Management: Simplified by removing localStorage dependencies and consolidating state in AuthContext.
OAuth Integration: OAuth Integration: Fixed role issues for Google sign-in users by ensuring proper role assignments in OAuth2SuccessHandler.
API Optimization: API Optimization: Consolidated AssemblyAI operations through WebClient with Direct Streaming API for memory efficiency.
Security Enhancements: Security Enhancements: Production settings adjustments for better security, including environment-specific database configuration.
Current Status: The project is stable and ready for deployment with working authentication, transcription, and user management functionality.
