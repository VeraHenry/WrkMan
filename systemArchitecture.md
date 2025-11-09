# WrkMan – System Architecture Blueprint

##  Overview
WrkMan is a service platform connecting artisans to customers in real time.  
This file explains how each technical layer interacts to bring that experience to life.

## Core Stack
## Frontend (Mobile & Web)

•	Framework: React Native (mobile), React.js (web)

•	Language: TypeScript
 
•	Navigation & UI: React Navigation, custom components
 
•	State Management & Data Fetching: @tanstack/react-query
 
•	Authentication & User Management: Firebase Authentication
 
•	Notifications & Analytics: Firebase Cloud Messaging, Firebase Analytics

## Backend (API & Integration Layer)

•	Runtime & Framework: Node.js v20 + Express.js
 
•	Deployment: Vercel Serverless Functions
 
## **Core Responsibilities:
  
•	Artisan search & smart matching
 
•	Job booking, chat and notifications
 
•	Ratings & reviews management
 
•	Secure payments integration

•	Authentication, rate limiting, analytics logging
 
•	Libraries & SDKs: firebase-admin, axios, express-rate-limit, Stripe SDKGitHub |

## Database Model (Simplified)

Authentication:

•	Firebase Authentication (manages user and artisan accounts securely)

Database:

•	Firebase Firestore

•	Stores user profiles, artisan profiles, bookings, reviews, and events
 
•	Real-time updates for chat, job status, and ratings

File Storage:

•	Firebase Storage

•	Stores profile pictures, job images, and other media

CI/CD & Builds:

•	GitHub Actions – automates linting, testing, and deployment
 
•	Expo EAS Build – builds mobile apps for Android and iOS

Payment Integrations:

•	Stripe / Paystack – for payment records

## How Component Communicate

1.  User opens WrkMan app and logs in or browses as a guest.

2.	The app displays a smart search interface where the user can look for artisans based on skill, location, price, or rating.
    
3.	When the user selects an artisan, the app fetches the artisan’s profile from the backend, including ratings, experience, and pricing.
    
4.	If the user wants to chat or book a job, the app sends a request to the backend using a secure API call.
    
5.	The backend (Node.js + Express) handles the request, updating the job status, sending notifications, and storing chat messages in the database.
    
6.	Notifications are pushed to both the user and the artisan via Firebase Cloud Messaging to keep them updated on booking status, messages, or job changes.
     
7.	Payments are processed securely via an integrated payment gateway (e.g., Stripe or Paystack), and payment confirmations are sent back to the app
     
8.	If the user leaves a review, the rating and review are stored in Firebase Firestore and reflected in the artisan’s profile for future users.

  
  ## Architecture Flow
   
 <img width="275" height="701" alt="Capture 5" src="https://github.com/user-attachments/assets/c356c6b6-4e5c-4dbe-8627-5320e47e00cb" />

	
## Communication Flow

1. The *frontend* sends HTTPS requests to the *backend API*.

2. The *backend* talks to *PostgreSQL* using an ORM like Prisma.
   
3. Chats update live through *WebSockets*.
 
4. Images go to *Cloudinary/S3*, links return to the database.
   
5. Notifications are delivered via *Firebase*.  

## Security Highlights
- Encrypted passwords with bcrypt  
- JWT-based authentication  
- Role-level permissions  
- Input validation on all requests  

 ## Technical Feasibility

1. Safe and Smart: Your data belongs to you. Chats, bookings, and payments are secure and encrypted. Users have full control profiles, job history, and reviews can be managed or deleted in a tap.

2. Lightning-Fast Experience: Finding the right artisan, sending a message, or completing a booking happens instantly. Real time notifications keep everyone in sync, so jobs never get delayed.

3. Simple to Build, Easy to Grow: With a single React Native codebase for iOS and Android, updates are fast and predictable. The backend focuses on what matters most: matching users with artisans, handling payments, and keeping the experience seamless.

4. Smart Scaling: Cloud services like Firebase and trusted payment gateways mean WrkMan can grow without breaking a sweat. Whether it’s 100 users or 100,000, the app stays responsive and reliable.

5. Built to Last: Analytics and performance monitoring are baked in, helping us spot issues early and keep the platform running smoothly. 
