# AI Workflow Log

This project uses AI as an engineering partner. AI output must be reviewed, understood, and adapted before acceptance.

Use this file to log important AI-assisted work.

## Workflow Principles

- Ask AI for small, focused tasks.
- Review generated code before accepting it.
- Prefer explainable code over complex generated patterns.
- Reject code that adds unnecessary scope.
- Update documentation when scope or architecture changes.
- Run build/tests when possible after implementation steps.

## Log Template

Copy this section for each meaningful AI-assisted step.

### Entry: YYYY-MM-DD - Short Title

What I asked AI to do:

- 

What AI generated:

- 

What I reviewed:

- 

What I changed manually:

- 

What I accepted:

- 

What I rejected:

- 

What I learned:

- 

Files affected:

- 

Verification performed:

- 

Follow-up needed:

- 

## Initial Entry: 2026-07-03 - Repository Context Setup

What I asked AI to do:

- Prepare repository context, scope, rules, planning documents, and prompt files before implementation.

What AI generated:

- Agent instructions
- README
- project context
- MVP scope
- implementation plan
- architecture decisions
- AI workflow template
- tradeoff template
- demo script
- starter prompts

What I reviewed:

- Pending manual review after commit.

What I changed manually:

- Pending manual review.

What I accepted:

- Pending manual review.

What I rejected:

- Pending manual review.

What I learned:

- Pending manual review.

Files affected:

- `AGENTS.md`
- `README.md`
- `docs/PROJECT_CONTEXT.md`
- `docs/MVP_SCOPE.md`
- `docs/IMPLEMENTATION_PLAN.md`
- `docs/ARCHITECTURE_DECISIONS.md`
- `docs/AI_WORKFLOW.md`
- `docs/TRADEOFFS.md`
- `docs/DEMO_SCRIPT.md`
- `prompts/001-initial-analysis.md`
- `prompts/002-backend-first-mvp-plan.md`
- `prompts/003-implementation-rules.md`

Verification performed:

- Pending git status review.

Follow-up needed:

- Review and approve Phase 1 before any application code is implemented.

## Entry: 2026-07-03 - Phase 1 Backend Solution Scaffold

What I asked AI to do:

- Create the .NET 9 backend Clean Architecture scaffold only.
- Do not implement claim logic, reserve logic, EF entities, migrations, authentication, or frontend code.

What AI generated:

- `ClaimsModule.sln`
- five backend projects under `src/`
- project references matching the planned Clean Architecture dependency direction
- initial package references for MediatR, FluentValidation, EF Core, Hangfire, and Swagger
- a minimal API startup with Swagger in development and `GET /health`
- future folder structure for each project
- `global.json` pinned to the installed .NET 9 SDK
- `.gitignore`
- `src/README.md`

What I reviewed:

- Required Phase 1 documents before coding
- Installed SDK versions
- Repository cleanliness before scaffold
- Project references
- Package references
- API startup contents

What I changed manually:

- Removed the unnecessary `Microsoft.AspNetCore.OpenApi` package because Swagger is handled by Swashbuckle for this scaffold.
- Removed template `Class1.cs` files.
- Added placeholder folders with `.gitkeep`.

What I accepted:

- Clean Architecture project layout
- Minimal dependency injection extension methods
- Swagger and health endpoint startup
- Documentation updates

What I rejected:

- Any claim, reserve, EF entity, migration, authentication, or frontend implementation in Phase 1.

What I learned:

- The repository uses .NET SDK `9.0.315` through `global.json`.
- The first API surface is intentionally tiny so future business logic can be added in controlled vertical slices.

Files affected:

- `global.json`
- `.gitignore`
- `ClaimsModule.sln`
- `src/`
- `README.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`

Follow-up needed:

- Review and approve Phase 2 before adding domain entities, EF Core DbContext, configurations, migrations, or seed data.

## Entry: 2026-07-03 - Phase 2 Domain Model And EF Core Persistence

What I asked AI to do:

- Add the Phase 2 domain model and EF Core persistence setup only.
- Do not add claim API endpoints, MediatR commands/queries, reserve approval workflow, Hangfire GL posting, Angular, or real authentication.

What AI generated:

- Domain entities for policies, claims, parties, risk objects, reserves, audit logs, cause-of-loss codes, and mock users.
- Domain enums for claim status, policy status, reserve status, party type, risk object type, and user role.
- `ClaimsModuleDbContext` with DbSet properties.
- EF Core entity configuration classes.
- Seed data for 3 policies, 5 cause-of-loss codes, and 3 mock users.
- Local SQL Server Docker Compose setup.
- Development connection string for local SQL Server.
- EF Core `InitialCreate` migration.

What I reviewed:

- Required Phase 2 instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- EF migration creation output.
- Build and health endpoint verification.

What I changed manually:

- Used a local `dotnet-ef` 9.0.0 tool manifest because the globally available EF tool was version 10.0.9.
- Added `Microsoft.EntityFrameworkCore.Design` to the API startup project for EF tooling support.
- Documented that local SQL Server credentials are fake development configuration only.

What I accepted:

- Simple, beginner-friendly entity model.
- Explicit EF Core configurations with max lengths, money precision, relationships, seed data, and restrictive delete behavior where audit/history could be affected.
- Docker-based local SQL Server setup.

What I rejected:

- Claim creation endpoints.
- MediatR use cases.
- Reserve approval workflow.
- Hangfire GL posting implementation.
- Real authentication.
- Frontend work.

What I learned:

- The migration can be created successfully with EF Core 9 tooling.
- Docker is not available in the current shell, so the database update cannot be verified locally yet.

Files affected:

- `src/ClaimsModule.Domain/Entities/`
- `src/ClaimsModule.Domain/Enums/`
- `src/ClaimsModule.Persistence/`
- `src/ClaimsModule.API/appsettings.Development.json`
- `docker-compose.yml`
- `.config/dotnet-tools.json`
- `README.md`
- `docs/ARCHITECTURE_DECISIONS.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet tool run dotnet-ef migrations add InitialCreate --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API --output-dir Migrations`
- `dotnet tool run dotnet-ef migrations list --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`

Follow-up needed:

- Install/start Docker or provide another SQL Server instance, then run `dotnet ef database update`.
- Review and approve Phase 3 before adding claim creation endpoints or MediatR use cases.
