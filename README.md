# Airbnb Clone Project

## Overview
The Airbnb Clone Project is a full-stack web application designed to replicate core functionalities of Airbnb, focusing on backend architecture, database design, and secure API development. Built with Django (backend), MySQL (database), and GraphQL (API), the project emphasizes scalable workflows, CI/CD pipelines (e.g., GitHub Actions/Docker), and team collaboration via GitHub. Key goals include mastering relational database design, implementing security best practices, and delivering feature-driven user experiences like property listings and bookings, all while adhering to modern DevOps practices.

## Team Roles and Responsibilities Summary

### 1. Business Analyst (BA)
- Analyzes business processes and stakeholder needs
- Translates business goals into technical requirements
- Bridges gap between stakeholders and development team

### 2. Product Owner (PO)
- Defines product vision and strategy
- Manages product backlog and priorities
- Ensures product meets market/customer needs
- More customer-focused than BA

### 4. Project Manager (PM)
- Oversees timelines, budget, and deliverables
- Facilitates team communication
- Manages risks and process improvements

### 5. UI/UX Designer
- Designs intuitive interfaces (UI)
- Creates user journeys and prototypes (UX)
- Conducts user research and testing

### 6. Software Architect
- Designs high-level system architecture
- Selects technologies and tools
- Ensures scalability and security

### 7. Software Developers
- **Frontend**: Builds user interfaces
- **Backend**: Implements business logic and APIs

### 8. Quality Assurance (QA) Engineer
- Creates test plans and scenarios
- Identifies functional/non-functional defects
- Ensures quality standards are met

### 9. Test Automation Engineer
- Develops automated test scripts
- Implements test automation frameworks
- Integrates testing into CI/CD pipelines

### 10. DevOps Engineer
- Implements CI/CD pipelines
- Manages deployment and infrastructure
- Automates development workflows

## Technology Stack  

This project leverages the following technologies to build a scalable and secure Airbnb-like platform:  

- **Django**: A high-level Python web framework for rapid backend development, handling business logic, and building RESTful APIs.  
- **MySQL**: A relational database management system (RDBMS) used for structured data storage, ensuring efficient querying and scalability.  
- **GraphQL**: A query language for APIs that enables flexible and efficient data retrieval, allowing clients to request only the needed data.  
- **Docker**: A containerization platform used to create consistent development and deployment environments, ensuring app portability.  
- **GitHub Actions**: A CI/CD (Continuous Integration/Continuous Deployment) tool for automating testing, builds, and deployments.  
- **Markdown**: A lightweight markup language for documentation, ensuring clear and structured project guides (e.g., this README).  

## Database Design  

The database is structured around the following key entities, ensuring efficient data relationships for the Airbnb Clone:  

### **Users**  
- `id` (Primary Key)  
- `username`  
- `email`  
- `password` (hashed)  
- `role` (e.g., guest, host)  

**Relationships**:  
- A **User** (host) can own multiple **Properties**.  
- A **User** (guest) can make multiple **Bookings** and **Reviews**.  

### **Properties**  
- `id` (Primary Key)  
- `title`  
- `description`  
- `price_per_night`  
- `host_id` (Foreign Key → Users)  

**Relationships**:  
- A **Property** belongs to one **User** (host).  
- A **Property** can have multiple **Bookings** and **Reviews**.  

### **Bookings**  
- `id` (Primary Key)  
- `start_date`  
- `end_date`  
- `total_price`  
- `guest_id` (Foreign Key → Users)  
- `property_id` (Foreign Key → Properties)  

**Relationships**:  
- A **Booking** is created by a **User** (guest) and linked to one **Property**.  
- A **Booking** can have one associated **Payment**.  

### **Reviews**  
- `id` (Primary Key)  
- `rating` (e.g., 1-5)  
- `comment`  
- `guest_id` (Foreign Key → Users)  
- `property_id` (Foreign Key → Properties)  

**Relationships**:  
- A **Review** is written by a **User** (guest) about a **Property**.  
- A **Property** can have multiple **Reviews**.  

### **Payments**  
- `id` (Primary Key)  
- `amount`  
- `payment_method`  
- `status` (e.g., pending, completed)  
- `booking_id` (Foreign Key → Bookings)  

**Relationships**:  
- A **Payment** is tied to one **Booking**.  

## Feature Breakdown

### **User Management**
Allows users to register, log in, and manage profiles. Hosts and guests have distinct roles, enabling property hosting and booking capabilities. Secure authentication ensures data privacy.

### **Property Management**
Enables hosts to create, update, and list properties with details like pricing, descriptions, and availability. Guests can browse and filter properties based on preferences.

### **Booking System**
Facilitates reservation creation, modification, and cancellation with date validation and pricing calculations. Integrates with payments to confirm bookings.

### **Review System**
Lets guests leave ratings and feedback for properties they've booked. Helps maintain trust and quality by displaying honest user experiences.

### **Payment Processing**
Securely handles transactions for bookings via integrated payment gateways. Tracks payment statuses (pending, completed) and confirms successful reservations.

### **Search & Filtering**
Allows guests to find properties using filters (price, location, amenities). Ensures quick discovery of relevant listings through optimized queries.

### **Admin Dashboard**
Provides moderators with tools to manage users, properties, and bookings. Includes analytics and reporting for platform oversight.

## API Security

To ensure the integrity and safety of our platform, the following security measures will be implemented:

### **Authentication (JWT)**
- **Implementation**: JSON Web Tokens (JWT) for secure user sessions.
- **Why It Matters**: Protects against unauthorized access by verifying user identities before granting access to sensitive data or actions.

### **Authorization (Role-Based Access Control)**
- **Implementation**: Granular permissions for users (guests, hosts, admins).
- **Why It Matters**: Ensures users can only perform actions relevant to their role (e.g., hosts manage properties, guests make bookings).

### **Rate Limiting**
- **Implementation**: Throttle excessive API requests (e.g., 100 requests/minute).
- **Why It Matters**: Prevents brute-force attacks and API abuse, maintaining system stability.

### **Data Encryption (HTTPS & Database)**
- **Implementation**: TLS/SSL for data in transit; hashing (passwords) and encryption (PII) at rest.
- **Why It Matters**: Safeguards sensitive data (e.g., payment details, user credentials) from interception or leaks.

### **Input Validation & Sanitization**
- **Implementation**: Strict checks on API request data (e.g., SQL injection prevention).
- **Why It Matters**: Blocks malicious payloads that could exploit vulnerabilities in databases or services.

### **Payment Security (PCI Compliance)**
- **Implementation**: Tokenization for payment processing; no raw card data storage.
- **Why It Matters**: Reduces fraud risk and ensures compliance with financial security standards.

Security is prioritized across all layers to protect user privacy, maintain trust, and prevent disruptions to critical services like bookings and payments.

## CI/CD Pipeline

### What is CI/CD?
CI/CD (Continuous Integration and Continuous Deployment) is a development practice that automates the building, testing, and deployment of applications. CI ensures code changes are regularly merged and validated, while CD automates the delivery of these changes to production environments.

### Why It Matters for This Project
- **Quality Assurance**: Automated testing catches bugs early before they reach production
- **Faster Releases**: Enables frequent, reliable updates with minimal manual intervention
- **Consistency**: Eliminates "it works on my machine" issues through standardized environments
- **Rollback Safety**: Allows quick reverts if issues emerge in production

### Tools We Use
- **GitHub Actions**: For automating workflows (tests, builds, deployments)
- **Docker**: Ensures consistent environments across development, testing, and production
- **AWS/GCP**: Cloud platforms for deployment and hosting
- **SonarQube**: For continuous code quality inspection
- **Postman**: For automated API testing

This pipeline helps maintain development velocity while ensuring stability as we scale the Airbnb Clone platform.
