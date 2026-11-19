# SimpleLedger

SimpleLedger is a full-stack banking and ledger application designed to explore backend software engineering concepts, particularly transaction integrity, concurrency control, and reliable financial operations.

The project aims to implement a simplified banking system in which users can manage accounts, transfer funds, and view transaction histories.

Beyond basic CRUD operations, SimpleLedger will focus on building a reliable backend using database transactions, concurrency control, and eventually asynchronous processing.

**Project Status:** Early development — environment setup complete.

## Tech Stack

| Component | Technology |
|---|---|
| Backend | Java 21, Spring Boot 4 |
| Build Tool | Gradle |
| Database | PostgreSQL 17 |
| Database Access | Spring Data JPA / Hibernate |
| Database Migrations | Flyway |
| Security | Spring Security |
| Containerization | Docker, Docker Compose |
| Frontend (Planned) | React |
| Messaging (Planned) | RabbitMQ |
| Caching (Optional) | Redis |

## Planned Features

- User registration and authentication
- Account creation and balance management
- Money transfers between accounts
- Transaction history and ledger entries
- Atomic database transactions
- Concurrency-safe balance updates
- Idempotent transfer requests
- Asynchronous processing using RabbitMQ
- Simple React-based user interface

Features will be implemented incrementally.

## Prerequisites

To run SimpleLedger locally, install:

- **Java Development Kit (JDK) 21**
- **Docker Engine**
- **Docker Compose plugin**
- **Git**

Gradle does not need to be installed separately, as the project includes the Gradle Wrapper.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/SimpleLedger.git
cd SimpleLedger
```

### 2. Configure Environment Variables

Create a local `.env` file from the provided template:

```bash
cp .env.example .env
```

Set the PostgreSQL password:

```dotenv
POSTGRES_PASSWORD=your_local_password
```

The `.env` file is excluded from Git to prevent accidental exposure of credentials.

### 3. Start PostgreSQL

Start the database container using Docker Compose:

```bash
sudo docker compose up -d
```

Verify that the container is running:

```bash
sudo docker compose ps
```

PostgreSQL is exposed locally on port `5432`.

The database uses a persistent Docker volume, allowing data to survive container restarts.

### 4. Configure Spring Boot Environment

Spring Boot reads the PostgreSQL password from the `POSTGRES_PASSWORD` environment variable.

On Linux/macOS, load the variables from `.env`:

```bash
set -a
source .env
set +a
```

### 5. Build the Application

Compile the Java source code:

```bash
./gradlew compileJava
```

To run the complete build, including tests:

```bash
./gradlew build
```

### 6. Run Spring Boot

Start the backend:

```bash
./gradlew bootRun
```

The application runs at:

**http://localhost:8080**

Spring Security currently uses its default development authentication configuration. A temporary password is generated and displayed in the application logs.

REST API endpoints will be introduced during development.

## Stopping the Application

To stop Spring Boot, press `Ctrl+C` in the terminal running `bootRun`.

To stop PostgreSQL without deleting its data:

```bash
sudo docker compose stop
```

To restart the database:

```bash
sudo docker compose start
```

To stop and remove the Compose-managed containers and network:

```bash
sudo docker compose down
```

Named database volumes are preserved by default when using `docker compose down`.

**Warning:** Running `docker compose down -v` also removes named volumes, which will delete the locally stored PostgreSQL database data.

## Project Structure

```text
simpleledger/
├── src/
│   ├── main/
│   │   ├── java/          # Spring Boot application
│   │   └── resources/     # Configuration and migrations
│   └── test/              # Backend tests
├── gradle/                # Gradle Wrapper
├── build.gradle
├── settings.gradle
├── compose.yaml           # Docker Compose configuration
├── .env.example           # Environment variable template
├── .gitignore
└── README.md
```

The project structure will evolve as the backend and frontend are implemented.

## Development Roadmap

- [x] Initialize Spring Boot project
- [x] Configure Java and Gradle
- [x] Set up Docker and PostgreSQL
- [x] Establish Spring Boot–PostgreSQL connectivity
- [ ] Design database schema
- [ ] Implement Flyway migrations
- [ ] Implement user authentication and authorization
- [ ] Implement accounts and ledger entries
- [ ] Implement atomic money transfers
- [ ] Add concurrency control and idempotency
- [ ] Introduce RabbitMQ for asynchronous processing
- [ ] Develop React frontend
- [ ] Add integration tests and deployment configuration

## License

No license has been selected yet.