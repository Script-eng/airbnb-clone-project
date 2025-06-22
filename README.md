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