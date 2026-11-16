# SthayiNivas 🏡

### Real Estate Management Platform | Java • Spring Boot • MySQL

SthayiNivas is a web-based real estate platform that connects property seekers, agents, and administrators. It provides role-based dashboards, property browsing and management, saved listings, property inquiries, appointment views, email OTP delivery, and an Ollama-powered chatbot integration.

> **Project status:** Source-code portfolio project. Features described below are based on the implementation in this repository; deployment and end-to-end testing are not claimed.

## ✨ Features

- **Role-based experience:** Dedicated dashboards and workflows for users, agents, and administrators.
- **Property discovery:** Browse property listings, view property details, and access filtering interfaces.
- **Property management:** Agent-facing property workflows and administrator visibility into listings and user counts.
- **Favorites:** Save and view favorite properties.
- **Inquiries and appointments:** Property inquiry handling, notifications, and appointment-related pages.
- **Email OTP:** Generate and send six-digit OTPs through Spring Mail.
- **AI chat integration:** `/chat` endpoint forwards prompts to a locally running Ollama instance using `llama3.2:latest`.
- **Server-rendered interface:** JSP views for authentication, dashboards, property listings, profiles, and more.

## 🛠️ Tech Stack

| Layer | Technologies |
| --- | --- |
| Backend | Java 17, Spring Boot 3.4.5, Spring MVC |
| Persistence | Spring Data JPA, MySQL |
| Views | JSP, CSS |
| Email | Spring Boot Mail, SMTP |
| AI integration | Ollama, Llama 3.2, RestTemplate |
| Build | Maven, Maven Wrapper |
| Testing dependencies | Spring Boot Starter Test |

## 🏗️ Architecture

```text
Browser / JSP Views
        |
Spring MVC Controllers
        |
Service Interfaces & Implementations
        |
Spring Data JPA Repositories
        |
      MySQL

External integrations:
  Spring Mail -> SMTP server
  ChatController -> Local Ollama API (localhost:11434)
```

The codebase separates web controllers, service interfaces, service implementations, entities, repositories, and DTOs.

## 📂 Project Structure

```text
src/main/
├── java/com/example/Real_Estate/
│   ├── controller/       # Admin, agent, user, auth, queries, OTP, chat
│   ├── Services/         # Service contracts
│   ├── ServiceImpl/      # Business logic
│   ├── repository/       # Spring Data repositories
│   ├── entity/           # Domain models and enums
│   ├── dto/              # Data transfer objects
│   └── exception/        # Exception handling
├── resources/
│   └── application.properties
└── webapp/
    ├── WEB-INF/views/   # JSP pages
    └── css/             # Stylesheets
```

## 🚀 Run Locally

### Prerequisites

- JDK 17
- MySQL
- Maven (or the included Maven Wrapper)
- SMTP credentials for email features
- Optional: Ollama with the `llama3.2:latest` model for chatbot features

### 1. Clone the repository

```bash
git clone https://github.com/ShubhSharma23NOV/Real-Estate.git
cd Real-Estate
```

> Replace the repository URL above if you publish SthayiNivas under a different repository name.

### 2. Configure your database and mail settings

Create a MySQL database and set your local Spring configuration. For example:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/sthayinivas
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
spring.jpa.hibernate.ddl-auto=update

spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${MAIL_USERNAME}
spring.mail.password=${MAIL_PASSWORD}
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```

This is an **example configuration**, not a verified deployment configuration. Set the database name, credentials, and mail provider to match your environment. Never commit real passwords or API keys.

### 3. Start the application

On macOS/Linux:

```bash
./mvnw spring-boot:run
```

On Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Then visit `http://localhost:8080/` (assuming the default Spring Boot port).

### 4. Optional: Start the AI chatbot backend

```bash
ollama pull llama3.2
ollama serve
```

The chat controller expects Ollama at `http://localhost:11434/api/generate`. If Ollama is already running, you do not need to start it again.

## 👥 Application Roles

| Role | Main functionality |
| --- | --- |
| User | Browse listings, save favorites, submit property inquiries |
| Agent | Access an agent dashboard and property-related workflows |
| Admin | Access a dashboard with property listings and user/agent/admin counts |

## 🔍 Selected Routes

| Route | Purpose |
| --- | --- |
| `/` | Landing page |
| `/login` | Login page |
| `/user/dashboard` | User dashboard |
| `/agent/dashboard` | Agent dashboard |
| `/admin/dashboard` | Admin dashboard |
| `/api/otp/send` | Send an email OTP (`POST`) |
| `/chat` | Chat with local Ollama (`POST`) |
| `/query-form/{propertyId}` | Property inquiry form |

## 🔐 Security Notes

This repository uses session-based role checks in parts of the controller layer. It should **not** be presented as production-hardened authentication.

Before deploying publicly:
- Move database and SMTP secrets out of tracked configuration.
- Rotate any credentials that were previously committed.
- Review password storage, authorization, input validation, CSRF protection, and OTP verification/rate limiting.
- Exclude compiled output and local development artifacts from version control.

## 📸 Screenshots

Add screenshots of the landing page, property listings, agent dashboard, and admin dashboard here once captured from a working local build.

## 👨‍💻 Author

**Shubh Sharma**  
Java Backend Developer

[GitHub](https://github.com/ShubhSharma23NOV)

--
