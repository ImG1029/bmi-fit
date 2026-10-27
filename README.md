# BMI Fit - Backend & AI Integration Service

A RESTful API built with FastAPI that processes user physical assessment data and leverages OpenAI's LLM via dynamic prompt engineering to generate strictly formatted, personalized diet and training plans.
## Technical Architecture & My Specific Contributions

> **Note on Authorship:** This repository is a fork from an academic group project. My specific role was focused on the core backend infrastructure, database configuration, and the automated testing suite, providing a stable foundation for the application's AI integrations.

*   **API Design (FastAPI):** Structured the foundational backend routing and business logic (`services/`), ensuring clean separation of concerns and reliable endpoints.
*   **Quality Assurance & Testing (Pytest):** Built and maintained the automated testing suite. Developed unit and integration tests to validate route stability, core BMI logic, and robust error handling during external service calls.
*   **Database Infrastructure:** Configured the database sessions and ORM models (SQLAlchemy) for PostgreSQL, ensuring reliable data persistence for user profiles and biometric data.
*   **Integration Support:** Provided backend support and manual testing for the OpenAI API integration pipeline, ensuring payload structures met system requirements.

## Tech Stack

*   **Language & Framework:** Python 3.11, FastAPI 0.115.12
*   **Database:** PostgreSQL 15.8 (ORM: SQLAlchemy), Redis (Rate Limiting)
*   **AI Integration:** OpenAI API (GPT-3.5 Turbo)
*   **Testing:** Pytest
*   **Infrastructure:** Docker, Docker Compose

## Running the Project Locally with Docker

The entire application environment (Backend, PostgreSQL, and Redis) is containerized.

Prerequisites

    Docker and Docker Compose installed
    Ports 8000, 6379 and 5432 must be available on your machine

### 1. Set environment variables

Rename `.env.example` to `.env` file in root directory, `.env` example:
```env
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=bmi-fit

REDIS_HOST=redis
REDIS_PASSWORD=password
REDIS_PORT=6379

SECRET_KEY=your_secret_key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=1000

OPENAI_API_KEY=your_openai_key
```

### 2. Build and Execute

Run the following command to spin up the FastAPI server, PostgreSQL database, and Redis rate limiting simultaneously:

```bash
docker compose up --build -d
```

### 3. Run Migrations

With the containers running, execute Alembic to build the database schema:


```bash
docker exec -it <backend_container_name> alembic upgrade head
```

### 4. Access the API

 - Swagger UI: `http://localhost:8000/docs`
 - ReDoc: `http://localhost:8000/redoc`