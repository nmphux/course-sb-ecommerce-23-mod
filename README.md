# SpringCommerce

SpringCommerce is a Java Spring Boot e-commerce web application for browsing and managing technology products. It started as a course capstone project and has since been developed into a portfolio project.

## Features

- Browse products by category and brand, search the catalog, and filter results.
- View product details and submit reviews.
- Create an account, sign in, and manage account settings.
- Add products to a shopping cart, update quantities, and place orders.
- Save products to a wishlist and review order history.
- Use an admin area to manage products, users, brands, and categories.

## Tech stack

- Java 18
- Spring Boot 3.1.5
- Spring MVC and Thymeleaf
- Spring Security
- Spring Data JPA and PostgreSQL
- Maven
- Docker Compose for local PostgreSQL

## Getting started

### Prerequisites

- JDK 18
- Docker with the Docker Compose plugin

### Run locally

1. Start the PostgreSQL service:

   ```bash
   docker compose up -d db
   ```

2. Set the datasource URL for a locally running application, then start SpringCommerce. The URL below uses the PostgreSQL port published by Docker Compose.

   **Windows PowerShell**

   ```powershell
   $env:SPRING_DATASOURCE_URL = "jdbc:postgresql://localhost:5432/springcommerce"
   .\mvnw.cmd spring-boot:run
   ```

   **macOS or Linux**

   ```bash
   SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/springcommerce ./mvnw spring-boot:run
   ```

3. Open [http://localhost:8080](http://localhost:8080) in your browser.

The Compose file starts the database only; the application runs on your machine through the Maven Wrapper.

### Run tests

**Windows PowerShell**

```powershell
.\mvnw.cmd test
```

**macOS or Linux**

```bash
./mvnw test
```

## Project structure

```text
src/
├── main/
│   ├── java/vn/com/ecommerce/springcommerce/
│   │   ├── config/       # Application and security configuration
│   │   ├── controller/   # HTTP request handling
│   │   ├── domain/       # Domain entities
│   │   ├── DTO/          # Data transfer objects
│   │   ├── repository/  # Data access
│   │   └── service/     # Application and business logic
│   └── resources/
│       ├── static/      # CSS, JavaScript, fonts, and images
│       └── templates/   # Thymeleaf views
└── test/                # Automated tests
```

The application follows a layered MVC structure: controllers handle web requests, services contain application logic, and repositories access PostgreSQL through JPA. Thymeleaf templates render the web pages.

## Data and configuration

The local database settings are defined in `docker-compose.yaml` and `src/main/resources/application.properties`. The current JPA setting uses `create-drop`, which recreates the schema when the application starts and removes it when the application stops. **Do not use this setting if you need to keep local data between runs.**

The default database credentials and application settings are intended for local development. Replace them and use a persistent schema strategy before deploying the application.
