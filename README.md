# :gem: capstone_project :gem:

## Project Overview

A microservices-based e-commerce platform, designed with a modular architecture to handle various aspects of an online store, including user authentication, product catalog management, email notifications, and payment processing. The project leverages Spring Boot for service development and Eureka for service discovery, creating a robust and scalable backend system.

## :star: Features

*   :busts_in_silhouette:   **User Authentication Service:** Manages user registration, login, and authorization using JWT and Spring Security.
*   :books:   **Product Catalog Service:** Handles product information, including storage and retrieval, potentially integrating with a database and Redis for caching.
*   :email:   **Email Service:** Facilitates sending email notifications, likely for order confirmations, password resets, etc., integrating with Kafka for asynchronous communication.
*   :credit_card:   **Payment Service:** Integrates with popular payment gateways like Razorpay and Stripe for processing transactions.
*   :world_map:   **Service Discovery:** Utilizes Spring Cloud Netflix Eureka Server to enable dynamic service discovery among microservices.
*   :rocket:   **Microservices Architecture:** Deployed as independent, loosely coupled services for scalability and maintainability.
*   :atom:   **Java & Spring Boot:** Built with modern Java versions and the Spring Boot framework for efficient development.

## :computer: Tech Stack

*   **Languages:** Java
*   **Frameworks:** Spring Boot, Spring Cloud, Spring Kafka, Spring Security
*   **Databases:** MySQL (inferred from dependencies)
*   **Caching:** Redis (inferred from dependencies)
*   **Service Discovery:** Eureka Server
*   **Build Tool:** Maven
*   **API Security:** JWT
*   **Payment Gateways:** Razorpay, Stripe
*   **Messaging:** Kafka (inferred from dependencies)

## :arrow_down: Installation

This project is a collection of Spring Boot microservices. To set up and run the project, you will need to:

1.  **Prerequisites:**
    *   Java Development Kit (JDK) 17 or higher installed.
    *   Apache Maven installed.
    *   A MySQL database instance running.
    *   A Redis instance running.
    *   A Kafka cluster running.

2.  **Clone the Repository:**
    ```bash
    git clone https://github.com/HarshRajIN/capstone_project.git
    cd capstone_project
    ```

3.  **Configure Each Service:**
    Navigate to each service directory (e.g., `ServiceDiscovery`, `UserAuthService`, `ProductCatalogService`, `EmailService`, `PaymentService`) and update the `application.properties` file with your specific configurations for:
    *   Database connection (MySQL)
    *   Redis connection
    *   Kafka broker details
    *   JWT secret keys and expiration times
    *   Payment gateway API keys (Stripe, Razorpay)
    *   Email service configurations (if applicable)

    **Example `application.properties` (for UserAuthService, adapt as needed):**
    ```properties
    # Database Configuration
    spring.datasource.url=jdbc:mysql://localhost:3306/your_auth_db?createDatabaseIfNotExist=true
    spring.datasource.username=your_db_user
    spring.datasource.password=your_db_password
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.show-sql=true

    # JWT Configuration
    jwt.secret=your_super_secret_key_that_is_long_enough
    jwt.expirationMs=86400000

    # Eureka Client Configuration
    eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/

    # Kafka Configuration
    spring.kafka.bootstrap-servers=localhost:9092
    # ... other Kafka properties

    # Server Port
    server.port=8081
    ```

4.  **Build and Run Services:**
    Use Maven to build and run each Spring Boot application. It is recommended to start the `ServiceDiscovery` first.

    *   **Service Discovery:**
        ```bash
        cd ServiceDiscovery
        ./mvnw clean install
        ./mvnw spring-boot:run
        ```

    *   **User Authentication Service:**
        ```bash
        cd ../UserAuthService
        ./mvnw clean install
        ./mvnw spring-boot:run
        ```

    *   **Product Catalog Service:**
        ```bash
        cd ../ProductCatalogService
        ./mvnw clean install
        ./mvnw spring-boot:run
        ```

    *   **Email Service:**
        ```bash
        cd ../EmailService
        ./mvnw clean install
        ./mvnw spring-boot:run
        ```

    *   **Payment Service:**
        ```bash
        cd ../PaymentService
        ./mvnw clean install
        ./mvnw spring-boot:run
        ```

    **Note:** Ensure that all necessary external services (MySQL, Redis, Kafka) are running before starting the microservices.

## :mag: Usage

This project is designed as a backend for an e-commerce platform. The services interact with each other through REST APIs and Kafka for asynchronous communication. Below are potential use cases and how to interact with the services:

1.  **User Registration and Login:**
    *   The `UserAuthService` will handle user registration and authentication. You can interact with it via its REST endpoints to create users and obtain JWT tokens for subsequent requests.

2.  **Product Management:**
    *   The `ProductCatalogService` exposes endpoints to manage and retrieve product information. This service likely interacts with a database and Redis for caching.

3.  **Payment Processing:**
    *   The `PaymentService` integrates with Razorpay and Stripe. You would typically call this service from a frontend or another backend service to initiate and confirm payments.

4.  **Email Notifications:**
    *   The `EmailService` likely consumes events from Kafka (e.g., order placed, shipment notification) and sends out emails. Its integration with Kafka suggests asynchronous processing for non-critical notification tasks.

5.  **Service Discovery:**
    *   The `ServiceDiscovery` (Eureka Server) allows services to register themselves and discover other services. This is crucial for inter-service communication in a microservices architecture.

**Example Interaction Flow (Conceptual):**

1.  A user registers via the `UserAuthService`.
2.  The user logs in, receiving a JWT token.
3.  The user browses products, with requests routed to `ProductCatalogService` (potentially via a gateway).
4.  When a user makes a purchase, a request is sent to `PaymentService` to initiate payment.
5.  Upon successful payment, `PaymentService` might publish an event to Kafka.
6.  `EmailService` consumes the event and sends a confirmation email.

**Note:** Specific API endpoints and request/response formats would need to be examined within the code of each service for precise interaction details.

## :file_folder: Project Structure

The project is organized into several microservices, each residing in its own directory:

```
capstone_project/
├── EmailService/
│   ├── src/main/java/com/example/emailservice/
│   │   └── EmailServiceApplication.java
│   ├── src/test/java/com/example/emailservice/
│   │   └── EmailServiceApplicationTests.java
│   ├── pom.xml
│   ├── HELP.md
│   ├── mvnw
│   └── mvnw.cmd
├── PaymentService/
│   ├── src/main/resources/application.properties
│   ├── pom.xml
│   ├── HELP.md
│   ├── mvnw
│   └── mvnw.cmd
├── ProductCatalogService/
│   ├── src/main/java/com/example/productcatalogservice/
│   │   └── ProductCatalogServiceApplication.java
│   ├── src/main/resources/application.properties
│   ├── src/test/java/com/example/productcatalogservice/
│   │   └── ProductCatalogServiceApplicationTests.java
│   ├── pom.xml
│   ├── HELP.md
│   ├── mvnw
│   └── mvnw.cmd
├── ServiceDiscovery/
│   ├── src/main/java/
│   ├── src/main/resources/application.properties
│   ├── src/test/java/com/example/servicediscovery/
│   │   └── ServiceDiscoveryApplicationTests.java
│   ├── pom.xml
│   ├── HELP.md
│   ├── mvnw
│   └── mvnw.cmd
├── UserAuthService/
│   ├── src/main/resources/application.properties
│   ├── pom.xml
│   ├── HELP.md
│   ├── mvnw
│   └── mvnw.cmd
└── README.md
```

## :computer: API Reference

Detailed API endpoints are not explicitly defined in the provided file snippets. However, based on the service responsibilities and Spring Boot conventions, you can anticipate the following:

*   **UserAuthService:**
    *   `POST /api/auth/register`: User registration.
    *   `POST /api/auth/login`: User login, returns JWT.
    *   Endpoints for managing user profiles and roles.
*   **ProductCatalogService:**
    *   `GET /api/products`: Retrieve a list of products.
    *   `GET /api/products/{id}`: Retrieve a specific product.
    *   `POST /api/products`: Add a new product (admin).
    *   `PUT /api/products/{id}`: Update a product (admin).
    *   `DELETE /api/products/{id}`: Delete a product (admin).
*   **PaymentService:**
    *   `POST /api/payments/initiate`: Initiate a payment transaction (e.g., with Razorpay/Stripe).
    *   `POST /api/payments/webhook`: Endpoint for payment gateway webhooks.
*   **EmailService:**
    *   Likely consumes messages from Kafka topics rather than exposing direct REST APIs for sending emails.
*   **ServiceDiscovery:**
    *   Typically provides a UI at `http://localhost:8761` (default) for monitoring registered services.

**Note:** These are inferred endpoints. Actual implementation details should be verified by examining the controller classes within each service.

## :raising_hands: Contributing

Contributions are welcome! Please feel free to:

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix (`git checkout -b feature/YourFeature` or `git checkout -b fix/YourBug`).
3.  Make your changes and commit them (`git commit -am 'Add some feature'`)
4.  Push to the branch (`git push origin feature/YourFeature`)
5.  Create a new Pull Request.

Please ensure your code adheres to the project's coding standards and includes relevant tests.

## :balance_scale: License

No license information was found in the repository. It is recommended to choose an open-source license (e.g., MIT, Apache 2.0) to clarify usage rights.

## :link: Important Links

*   **Repository URL:** [https://github.com/HarshRajIN/capstone_project](https://github.com/HarshRajIN/capstone_project)

## :handshake: Footer

© 2023 HarshRajIN. All rights reserved.

This project is maintained by HarshRajIN. Feel free to:

*   ⭐ Star this repository if you found it helpful!
*   :fork_and_knife: Fork the repository to contribute or build upon it.
*   :bug: Report any issues you encounter.

Developed with :heart: and :coffee:.