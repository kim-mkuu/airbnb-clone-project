# Airbnb Clone Project

## Overview

The **Airbnb Clone Project** aims to replicate the core functionality of Airbnb by building a robust backend that manages users, property listings, bookings, payments, and reviews. The system is designed for scalability, performance, and clean API integration (REST + GraphQL). The goal is to deliver a production-grade backend foundation that can be extended into a full-featured platform.

## Project Goals

- Secure user registration, authentication, and profile management  
- CRUD operations for property listings  
- Booking system with check-in/check-out management  
- Payment processing and transaction recording  
- User review and rating system  
- Optimized performance via indexing and caching  
- Clean and documented APIs for easy integration

## Technology Stack

- **Backend Framework:** Django + Django REST Framework  
- **Database:** PostgreSQL  
- **API:** REST (OpenAPI) + GraphQL  
- **Async Tasks:** Celery  
- **Caching / Session:** Redis  
- **Containerization:** Docker  
- **CI/CD:** Automated pipelines for testing and deployment

## Team Roles

### Product Owner (PO)

- Defines the product vision and priorities. Ensures features align with user needs and business goals. Manages the backlog and approves deliverables.

### Project Manager (PM)

- Coordinates the team, manages timelines, resources, and communication. Ensures the project stays on track and resolves blockers.

### Business Analyst (BA)

- Gathers and clarifies requirements. Translates business needs into clear technical specifications for the development team.

### Backend Developer

- Implements API endpoints, business logic, and integrations. Works with Django, DRF, GraphQL, Celery, and Redis to build core system functionality.

### Database Administrator (DBA)

- Designs and optimizes the PostgreSQL database. Handles indexing, performance tuning, backup, and data integrity.

### Frontend Developer (if added later)

- Builds the UI and consumes APIs. Ensures a smooth user experience and integrates frontend logic with backend endpoints.

### DevOps Engineer

- Sets up Docker, CI/CD pipelines, deployment environments, monitoring, and scaling. Ensures reliability and automation.

### QA Engineer / Tester

- Designs and executes test plans. Validates API functionality, performance, and edge cases to ensure system quality.

### UI/UX Designer (optional but valuable)

- Designs user flows and interface layouts. Ensures the product is visually appealing and intuitive.

### Security Specialist (optional or part-time)

- Ensures authentication, authorization, data protection, and compliance with security standards.

## Database Design

### Key Entities

#### User

- **user_id:** Unique identifier (Primary Key)
- **email:** User email address (unique)
- **password_hash:** Encrypted password
- **role:** User role (guest, host, admin)
- **created_at:** Account creation timestamp

**Relations:** A user can have multiple properties (as host), multiple bookings (as guest), multiple reviews, and multiple payments.

#### Property

- **property_id:** Unique identifier (Primary Key)
- **host_id:** Foreign Key to User
- **title:** Property name/title
- **price_per_night:** Nightly rate
- **location:** Property address/coordinates

**Relations:** A property belongs to one user (host). A property can have multiple bookings and multiple reviews.

#### Booking

- **booking_id:** Unique identifier (Primary Key)
- **property_id:** Foreign Key to Property
- **user_id:** Foreign Key to User (guest)
- **check_in_date:** Start date of booking
- **check_out_date:** End date of booking
- **status:** Booking status (pending, confirmed, cancelled)

**Relations:** A booking belongs to one property and one user (guest). A booking is associated with one payment.

#### Review

- **review_id:** Unique identifier (Primary Key)
- **property_id:** Foreign Key to Property
- **user_id:** Foreign Key to User
- **rating:** Numeric rating (1-5)
- **comment:** Review text

**Relations:** A review belongs to one property and one user. Each booking can optionally have one review.

#### Payment

- **payment_id:** Unique identifier (Primary Key)
- **booking_id:** Foreign Key to Booking
- **amount:** Payment amount
- **payment_method:** Payment type (credit card, PayPal, etc.)
- **transaction_date:** Timestamp of payment

**Relations:** A payment belongs to one booking. Each booking has one associated payment.
