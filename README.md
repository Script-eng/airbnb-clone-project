# Airbnb Clone Project

This repository contains the source code and documentation for a full-stack Airbnb Clone project. It is designed to be a comprehensive, real-world application that simulates the core functionalities of a modern booking platform. The primary focus is not just on the final product, but on mastering the entire professional software development lifecycle, from initial design to deployment and maintenance.

## 🎯 Project Goals

The main objective of this project is to develop a deep, practical understanding of modern software engineering principles. Key goals include:

-   **Backend & Database Architecture:** Design and develop a robust backend architecture and a scalable relational database schema that can support complex queries and relationships.
-   **Secure API Development:** Build a secure API using GraphQL, with a strong focus on authentication, authorization, and data protection best practices.
-   **CI/CD Pipeline Implementation:** Establish a complete CI/CD (Continuous Integration/Continuous Deployment) pipeline for automated testing and seamless deployment, improving development velocity and reliability.
-   **Collaborative Workflows:** Implement industry-standard collaborative workflows using Git and GitHub, including effective branching strategies and pull request management.
-   **Comprehensive Documentation:** Create thorough project documentation, from system design and database schemas to API specifications, ensuring the project is understandable and maintainable.
-   **Technology Integration:** Effectively integrate a modern tech stack to build a cohesive and performant application.

## 🛠️ Technology Stack

This project utilizes a modern, robust, and scalable set of technologies chosen to meet the demands of a real-world web application.

| Category                  | Technology                                                                          | Purpose                                                                                             |
| ------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Backend Framework**     | <img src="https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white">     | The core framework for building the application's business logic and serving the API.               |
| **Database**              | <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">         | A powerful and reliable relational database for storing all application data (users, listings, etc.). |
| **API**                   | <img src="https://img.shields.io/badge/GraphQL-E10098?style=for-the-badge&logo=graphql&logoColor=white">     | A modern query language for the API, allowing clients to request exactly the data they need.        |
| **Containerization**      | <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">       | Used for creating consistent and isolated development and production environments.                  |
| **Continuous Integration**| <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white"> | Automates the CI/CD pipeline, including running tests and deploying the application.                |

---

## 👥 Team Roles

This project simulates a real-world development environment where distinct roles collaborate to build, deploy, and maintain the application.

### Backend Developer

The Backend Developer is responsible for building and maintaining the server-side logic of the application. They are the primary architects of the core services that power the platform.

**Key Responsibilities:**
*   Implement business logic and application features using the **Django** framework.
*   Design and build the **GraphQL API** for client-server communication.
*   Implement user authentication, authorization, and session management.
*   Write unit and integration tests to ensure code quality and reliability.

### Database Administrator (DBA)

The Database Administrator designs, implements, and maintains the application's database. They ensure data integrity, performance, and security.

**Key Responsibilities:**
*   Design the relational database schema in **MySQL**, defining tables, relationships, and constraints.
*   Manage schema changes and data migrations as the application evolves.
*   Monitor database performance and optimize complex queries for efficiency.
*   Implement backup, recovery, and data security procedures.

### DevOps Engineer

The DevOps Engineer focuses on automating and streamlining the development pipeline. They build the bridge between development and operations to ensure a smooth, efficient, and reliable delivery process.

**Key Responsibilities:**
*   Create and manage **Docker** configurations for consistent development and production environments.
*   Set up and maintain the **CI/CD pipeline** using **GitHub Actions** to automate builds, testing, and deployments.
*   Manage application infrastructure, monitoring, and logging.

### Other Key Roles

*   **Security Specialist:** Responsible for application and data security, conducting vulnerability assessments, and implementing security best practices.


## 🗂️ Database Design

The database is the backbone of the application, designed using a relational model in **MySQL**. The structure is centered around a few key entities that manage users, properties, and the booking process.

### Core Entities

#### 1. Users
Stores information about individuals who sign up, whether they are guests or hosts.

*   `id` (Primary Key): Unique identifier for each user.
*   `email`: User's email address, used for login and communication.
*   `password_hash`: Hashed version of the user's password for secure storage.
*   `full_name`: The user's full name.
*   `created_at`: Timestamp when the user account was created.

#### 2. Properties
Represents the rental listings created by hosts.

*   `id` (Primary Key): Unique identifier for each property.
*   `owner_id` (Foreign Key -> Users.id): The user who owns and manages the property.
*   `title`: The name of the listing (e.g., "Cozy Downtown Loft").
*   `description`: Detailed information about the property.
*   `price_per_night`: The cost to rent the property for one night.
*   `location`: Address or geographical coordinates of the property.

#### 3. Bookings
Represents a confirmed reservation of a property by a user.

*   `id` (Primary Key): Unique identifier for each booking.
*   `user_id` (Foreign Key -> Users.id): The user who made the booking (the guest).
*   `property_id` (Foreign Key -> Properties.id): The property being booked.
*   `start_date`: The check-in date for the reservation.
*   `end_date`: The check-out date for the reservation.
*   `total_price`: The calculated total cost of the stay.

#### 4. Reviews
Contains feedback and ratings left by guests after their stay.

*   `id` (Primary Key): Unique identifier for each review.
*   `booking_id` (Foreign Key -> Bookings.id): The specific booking this review is for.
*   `rating`: A numerical score (e.g., 1-5) given by the guest.
*   `comment`: The textual feedback or comment from the guest.
*   `created_at`: Timestamp when the review was submitted.

#### 5. Payments
Tracks the financial transactions associated with bookings.

*   `id` (Primary Key): Unique identifier for each payment.
*   `booking_id` (Foreign Key -> Bookings.id): The booking this payment is for.
*   `amount`: The total amount paid.
*   `status`: The current state of the payment (e.g., `pending`, `completed`, `failed`).
*   `transaction_id`: The unique ID provided by the payment gateway (e.g., Stripe).

### Entity Relationships

*   **Users & Properties**: A `User` (as a host) can have many `Properties`, but each `Property` belongs to only one `User`. (One-to-Many)
*   **Users & Bookings**: A `User` (as a guest) can make many `Bookings`, but each `Booking` is made by a single `User`. (One-to-Many)
*   **Properties & Bookings**: A `Property` can have many `Bookings`, but a `Booking` is for exactly one `Property`. (One-to-Many)
*   **Bookings & Reviews**: A `Booking` can have at most one `Review`. This ensures a guest can only review a stay once. (One-to-One)
*   **Bookings & Payments**: Each `Booking` is associated with one `Payment` transaction. (One-to-One)


## ✨ Feature Breakdown

This project is broken down into several core features that collectively create a functional booking platform. Each feature is designed to handle a specific part of the user journey for both guests and hosts.

### 1. User Authentication & Profile Management
This feature handles all aspects of user identity. It allows individuals to sign up for a new account, log in securely, and manage their personal profile information. This system is the gateway to the platform, ensuring that all actions are tied to a verified user, which is critical for secure bookings and listings.

### 2. Property Listing & Management
This is the core toolset for hosts. It enables property owners to create, edit, and manage their listings with details like descriptions, photos, pricing, and amenities. This feature is responsible for building the platform's inventory, giving hosts the control they need to market their spaces effectively.

### 3. Search & Discovery
The primary feature for guests, allowing them to search for available properties using filters like location, dates, and number of guests. The search results will be displayed in an intuitive way, making it easy for users to find and compare potential stays. An effective search mechanism is crucial for converting visitors into bookers.

### 4. Booking & Reservation System
This feature manages the entire reservation workflow. Guests can select travel dates, see a final price breakdown including fees, and submit a booking request. The system handles availability checks and confirms the reservation, forming the central transactional engine of the application.

### 5. Review and Rating System
After a stay is completed, this feature allows guests to leave a rating and a written review for the property. This builds a foundation of trust and transparency on the platform. Reviews help future guests make informed decisions and incentivize hosts to provide high-quality experiences.


## 🛡️ API Security

Securing the API is a top priority for this project. Given that the application will handle sensitive user data, booking information, and financial transactions, a multi-layered security approach will be implemented to protect the platform and its users from threats.

### Key Security Measures

1.  **Authentication (Token-Based with JWT):**
    Every protected endpoint will require a valid JSON Web Token (JWT). When a user logs in, the server will issue a short-lived, signed token. This token must be included in the header of subsequent requests to verify the user's identity, ensuring that anonymous users cannot access or modify sensitive data.

2.  **Authorization (Permission-Based):**
    Authentication confirms *who* a user is, while authorization determines *what* they are allowed to do. We will implement a role-based permission system where actions are restricted based on user roles (e.g., a user can only edit their own profile, and a host can only modify their own properties). This prevents users from accessing or altering data that does not belong to them.

3.  **Rate Limiting:**
    To protect the API from abuse and denial-of-service (DoS) attacks, rate limiting will be enforced. This will restrict the number of requests a single user or IP address can make within a certain time frame, ensuring the application remains available and performant for all legitimate users.

4.  **Input Validation and Sanitization:**
    All data received from clients will be rigorously validated. GraphQL's strong typing system provides a first layer of defense, but we will add business-level validation (e.g., ensuring a booking's end date is after its start date). This prevents data corruption and protects against common vulnerabilities like injection attacks.

### Why Security is Crucial

*   **Protecting User Data:** The `Users` entity contains Personally Identifiable Information (PII). Strong authentication and authorization are essential to prevent data breaches, protect user privacy, and maintain trust.
*   **Securing Financial Transactions:** The `Bookings` and `Payments` systems are the financial core of the app. Security measures are critical to ensure that payment details are handled securely and to prevent fraudulent transactions or unauthorized access to financial history.
*   **Maintaining Platform Integrity:** Without proper security, the platform could be overrun with spam listings, fake reviews, or malicious user activity. Enforcing strict rules through authorization and rate limiting ensures the integrity and trustworthiness of the content on our platform.


## 🚀 CI/CD Pipeline

A CI/CD (Continuous Integration/Continuous Deployment) pipeline will be implemented to automate the process of building, testing, and deploying the application. This automated workflow is essential for ensuring code quality, improving development speed, and maintaining a stable production environment.

### Why is a CI/CD Pipeline Important?

For a project of this scale, a CI/CD pipeline is not just a "nice-to-have"—it's a necessity. It provides several key benefits:

*   **Reliability:** By automatically running a full suite of tests every time code is committed, we can catch bugs and regressions early, before they ever reach production.
*   **Velocity:** Automating the deployment process eliminates manual, error-prone steps. This allows developers to release new features and bug fixes to users faster and more frequently.
*   **Consistency:** The pipeline ensures that the application is built and deployed in a consistent and repeatable manner every single time, reducing the risk of environment-specific issues.

### Key Tools

The pipeline will be built using a combination of modern, industry-standard tools:

*   **GitHub Actions:** This will serve as the engine for our CI/CD pipeline. We will create workflows that automatically trigger on events like a `git push` or a `pull_request`. These workflows will define the steps for building, testing, and deploying the application.
*   **Docker:** We will use Docker to containerize our Django application and its services (like the MySQL database). This packages the application and its dependencies into a single, portable image, ensuring that the environment is identical across development, testing, and production.