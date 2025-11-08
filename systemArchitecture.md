# WrkMan – System Architecture Blueprint

##  Overview
WrkMan is a service platform connecting artisans to customers in real time.  
This file explains how each technical layer interacts to bring that experience to life.

## Core Stack
 Component | Technology | Purpose |
 *Frontend* | React (web) / React Native (mobile) | User interface for browsing and booking |
 *Backend* | Node.js + Express | API logic, authentication, and booking flow |
 *Database* | PostgreSQL | Central data hub (users, bookings, reviews) |
 *Storage* | Cloudinary / AWS S3 | Media uploads (photos, certificates) |
 *Auth* | JWT or Firebase | Secure login for artisans and customers |
 *Notifications* | Firebase Cloud Messaging | Real-time alerts |
 *Hosting* | Vercel (frontend), Render/Heroku (backend) | CI/CD deployment from GitHub |

## Database Model (Simplified)
*Users* - id, name, email, phone, password, role (artisan/customer), rating, location
*Services* - id, name, category, description, price_range
*Bookings* - id, customer_id, artisan_id, service_id, date, status, payment_status
*Chats* - id, booking_id, sender_id, message, timestamp
*Reviews* - id, booking_id, rating, comment

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

## Mermaid Architecture Diagram
mermaid
flowchart LR
  User[Client App]:|API Calls| Backend[(Node.js)]
  Backend >|SQL| DB[(PostgreSQL)]
  Backend >|Uploads| Storage[(Cloudinary/S3)]
  Backend >|Notifications| Firebase[(FCM)]
  User: Chat| WebSocket[(Realtime Chat Server)]