# RaceDay — ASP.NET Core MVC

RaceDay is a student race management web application with event listings, categories, participant enrolments, results and role-aware dashboards.

## Run locally

Requires .NET 8 SDK and a SQL Server instance configured in `appsettings.json` or user secrets. From the project directory:

```powershell
dotnet restore
dotnet build
dotnet run
```

The application uses Entity Framework Core migrations at startup. Configure `ConnectionStrings:DefaultConnection` for your machine.

### Optional development admin account

Set user secrets locally; do **not** commit passwords:

```powershell
dotnet user-secrets set "SeedAdmin:Email" "admin@example.test"
dotnet user-secrets set "SeedAdmin:Password" "CHOOSE-A-STRONG-UNIQUE-PASSWORD"
```

## Docker

```powershell
docker build -t raceday-mvc .
docker run --rm -p 8080:8080 -e ConnectionStrings__DefaultConnection="YOUR_REACHABLE_SQL_SERVER_CONNECTION_STRING" raceday-mvc
```

Open `http://localhost:8080`. SQL Server must be accessible from the container; a Windows LocalDB connection typically **does not work** from Linux Docker. Use a reachable SQL Server and an appropriately secured connection string. Container runtime has not been independently tested.

## Architecture and outstanding Part 3 requirements

This project is an **existing MVC + EF Core monolith**, not the Part 2 REST API client specified by the brief. Controllers still use `ApplicationDbContext` directly. Session-backed API authentication, API-based data access, and Azure Blob Storage via the Part 2 API are **not implemented** in this package. The existing Identity cookie authentication supports local login/logout and role checks, but is not equivalent to the required API session architecture. Event banner uploads are not implemented. UI views are provided for core controllers; some identity/administration screens still need verification.

## Submission

- Push changes to your own repository, using meaningful commits.
- Test the core user journeys (register, login, create event, add category, enrol, results).
- Record and upload an unlisted demonstration video and put its link here: **[add your video link]**.
- Be transparent in your video about the missing API and Azure components and any untested Docker behavior.
