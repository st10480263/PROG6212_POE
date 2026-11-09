# RaceDay Event Management Platform

A distributed ASP.NET Core solution for managing athletic events, participant registrations, and live results. The application separates concerns into an MVC front-end client consuming an independent ASP.NET Core Web API with role-based access control and Azure Blob Storage.

---

## 1. Project Architecture

- **Frontend (MVC):** `POE_ST10480263` — Port `7011` (Consumes API via `HttpClient`, session-based auth).
- **Backend (Web API):** `RaceDayApp` — Port `7001` (Exposes REST endpoints, validates JWTs, executes business logic).
- **Data Access Layer:** `RaceDayData` — Entity Framework Core connecting to SQL Server (`RaceDay` database).
- **Domain Models:** `RaceDayModel` — Shared entities, DTOs, and view models.
- **Media Storage:** Azure Blob Storage for event banners and user profile assets.

---

## 2. Key Features

- **Decoupled Architecture:** MVC client contains zero direct database dependencies; all operations flow through the Web API.
- **Organisers:** Create/edit events, upload promotional banners to Azure Blob Storage, create event categories, and capture participant results.
- **Participants:** Browse upcoming events with category/date filters, enter races with one-click enrolment, and track personal race histories.
- **Security:** Stateless JWT token generation on API with claims-based access (`Organiser` / `Participant`).

---

## 3. Local Setup & Execution

### Prerequisites
- .NET 8.0 SDK
- SQL Server Express (`RaceDay` database)

### Running Both Applications
1. Open the solution file (`.sln`) in Visual Studio.
2. Right-click Solution > **Configure Startup Projects...**
3. Select **Multiple startup projects** and set:
   - `RaceDayApp` (API) -> **Start**
   - `POE_ST10480263` (MVC) -> **Start**
4. Press **F5** to run.

---

## 4. Docker Deployment

```bash
# Build the container image from repository root
docker build -t raceday-mvc:latest -f POE_ST10480263/Dockerfile .

# Run the containerized MVC application
docker run -d -p 8080:8080 --name raceday-mvc-container raceday-mvc:latest
