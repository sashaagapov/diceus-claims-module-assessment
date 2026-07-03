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

## Entry: 2026-07-03 - Phase 3 Claim/FNOL Creation

What I asked AI to do:

- Implement only the first FNOL claim creation vertical slice.
- Add minimal lookup endpoints for policies and cause-of-loss codes.
- Do not add claim list/detail, status transitions, reserves, Hangfire, frontend, or real authentication.

What AI generated:

- MediatR query for policy lookup.
- MediatR query for active cause-of-loss code lookup.
- MediatR command, validator, handler, DTOs, and response for claim creation.
- Thin API controllers for policies, cause-of-loss codes, and claims.
- Validation middleware for FluentValidation errors.
- A small result type for simple business-rule failures.
- `IClaimsModuleDbContext` abstraction implemented by `ClaimsModuleDbContext`.

What I reviewed:

- Required Phase 3 instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Existing Phase 2 migration.
- Docker/SQL Server availability.
- API and database verification output.

What I changed manually:

- Downgraded MediatR from 14.2.0 to 12.5.0 to avoid development license warning noise during the assessment demo.
- Configured API JSON options to serialize enums as strings for clearer Swagger requests/responses.

What I accepted:

- Controller -> MediatR -> FluentValidation -> Handler -> EF Core -> SQL Server flow.
- Business checks for active policy, active cause-of-loss code, and active mock user.
- Claim creation with status `Open`, generated claim number, parties, risk objects, and `ClaimCreated` audit entry.

What I rejected:

- Claim list/detail endpoints.
- Claim status transitions.
- Reserve creation or approval workflow.
- Hangfire GL posting.
- Frontend work.
- Real authentication.

What I learned:

- SQL Server Docker container is available in the current environment.
- The FNOL creation flow can be verified end-to-end against the local database.

Files affected:

- `src/ClaimsModule.Application/Claims/CreateClaim/`
- `src/ClaimsModule.Application/Policies/GetPolicies/`
- `src/ClaimsModule.Application/CauseOfLossCodes/GetCauseOfLossCodes/`
- `src/ClaimsModule.Application/Common/`
- `src/ClaimsModule.Application/Interfaces/`
- `src/ClaimsModule.API/Controllers/`
- `src/ClaimsModule.API/Middleware/`
- `src/ClaimsModule.API/Program.cs`
- `src/ClaimsModule.Persistence/`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- `GET /api/policies` returned seeded policies
- `GET /api/cause-of-loss-codes` returned seeded cause-of-loss codes
- `POST /api/claims` returned `201 Created`
- SQL Server check confirmed the created claim and `ClaimCreated` audit log entry were saved

Follow-up needed:

- Review and approve Phase 4 before adding claim list/detail or status transitions.

## Entry: 2026-07-03 - Phase 4A Claim List And Detail

What I asked AI to do:

- Add read-only claim browsing only.
- Do not add status transitions, reserves, Hangfire, frontend, or real authentication.

What AI generated:

- `GetClaimsQuery`, handler, and list DTO.
- `GetClaimByIdQuery`, handler, and detail DTOs for parties, risk objects, reserves, and audit log entries.
- `GET /api/claims`.
- `GET /api/claims/{id}`.

What I reviewed:

- Required Phase 4A instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Build output before and after changes.
- API verification output for list, detail, and not-found behavior.

What I changed manually:

- Kept claim detail as several small `AsNoTracking` read queries instead of one large multi-collection projection. This avoids EF Core's multiple collection single-query warning and stays easy to explain.
- Added `Reserves` to `IClaimsModuleDbContext` so claim detail can return an empty or populated reserve summary without exposing the concrete DbContext.

What I accepted:

- Read-only query handlers using `AsNoTracking`.
- Thin controller actions that only call MediatR and shape HTTP responses.
- `404 Not Found` with a simple error for missing claim detail.

What I rejected:

- Claim status transitions.
- Reserve creation or approval workflow.
- Hangfire GL posting.
- Frontend work.
- Real authentication.

What I learned:

- The existing FNOL-created claims can now be browsed through Swagger/API.
- Detail reads should avoid a single large joined query when loading multiple child collections.

Files affected:

- `src/ClaimsModule.Application/Claims/GetClaims/`
- `src/ClaimsModule.Application/Claims/GetClaimById/`
- `src/ClaimsModule.Application/Interfaces/IClaimsModuleDbContext.cs`
- `src/ClaimsModule.API/Controllers/ClaimsController.cs`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- `GET /api/policies` returned seeded policies
- `GET /api/cause-of-loss-codes` returned seeded cause-of-loss codes
- `POST /api/claims` returned `201 Created`
- `GET /api/claims` returned the created claim first
- `GET /api/claims/{id}` returned full claim detail
- `GET /api/claims/{missingId}` returned `404 Not Found`

Follow-up needed:

- Review and approve Phase 4B before adding claim status transitions.

## Entry: 2026-07-03 - Phase 4B Claim Status Transitions

What I asked AI to do:

- Add only controlled claim status transitions.
- Do not add reserve creation, reserve approval, Hangfire, frontend, real authentication, documents, or payments.

What AI generated:

- `UpdateClaimStatusCommand`.
- `UpdateClaimStatusCommandValidator`.
- `UpdateClaimStatusCommandHandler`.
- `UpdateClaimStatusResponse`.
- `PATCH /api/claims/{id}/status`.
- Visible allowed transition rules.

What I reviewed:

- Required Phase 4B instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Build output before and after changes.
- API verification output for valid transition, invalid transition, missing claim, and audit log behavior.

What I changed manually:

- Extended `ClaimStatus` with the statuses required by the Phase 4B workflow: `UnderInvestigation`, `PendingPayment`, `Reopened`, and `Withdrawn`.
- Kept previous enum values as legacy/unused values to avoid breaking any existing stored strings.
- Inserted status-change audit entries through `dbContext.AuditLogEntries.Add(...)` with `ClaimId` set explicitly. This keeps the audit insert clear and avoids EF treating a new audit entry with a non-default Guid as an update.

What I accepted:

- Simple allowed-transition set in the handler.
- `200 OK` for valid status change.
- `404 Not Found` for non-empty missing claim IDs.
- `422 Unprocessable Entity` for disallowed transitions.
- `ClaimStatusChanged` audit entry with old and new status in details.

What I rejected:

- Reserve creation.
- Reserve approval workflow.
- Hangfire GL posting.
- Frontend work.
- Real authentication.
- Documents or payments.

What I learned:

- Since claim statuses are stored as strings, adding enum members does not require a database migration.
- Explicit audit inserts are easier to explain and safer than adding a new audit record through an unloaded navigation collection.

Files affected:

- `src/ClaimsModule.Domain/Enums/ClaimStatus.cs`
- `src/ClaimsModule.Application/Claims/UpdateClaimStatus/`
- `src/ClaimsModule.API/Controllers/ClaimsController.cs`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- `POST /api/claims` returned `201 Created`
- `GET /api/claims/{id}` showed initial status `Open`
- `PATCH /api/claims/{id}/status` from `Open` to `UnderInvestigation` returned `200 OK`
- `GET /api/claims/{id}` showed updated status `UnderInvestigation`
- claim detail audit log included `ClaimStatusChanged`
- invalid transition `UnderInvestigation` to `Closed` returned `422 Unprocessable Entity`
- non-empty missing claim ID returned `404 Not Found`

Follow-up needed:

- Review and approve Phase 5 before adding reserve creation and approval workflow.

## Entry: 2026-07-03 - Phase 5A Reserve Creation

What I asked AI to do:

- Add only reserve creation for existing claims.
- Do not add reserve approval, rejection, self-approval prevention, Hangfire, frontend, real authentication, payments, or documents.

What AI generated:

- `CreateReserveCommand`.
- `CreateReserveCommandValidator`.
- `CreateReserveCommandHandler`.
- `CreateReserveResponse`.
- `POST /api/claims/{claimId}/reserves`.

What I reviewed:

- Required Phase 5A instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Build output before and after changes.

What I accepted:

- `201 Created` for successful reserve creation.
- `404 Not Found` for non-empty missing claim IDs.
- `400 Bad Request` for validation and inactive or missing creator users.
- Auto-approved status for reserves up to 10,000.
- Pending approval status for reserves above 10,000.
- `ReserveCreated` audit entry with amount, currency, and resulting status.

What I rejected:

- Manual reserve approval or rejection.
- Self-approval validation.
- Hangfire GL posting.
- Frontend work.
- Real authentication.
- Payments or documents.

What I learned:

- Reserve creation can reuse the existing Phase 2 schema, so no migration is needed.
- Claim detail already includes reserve and audit summaries, which makes the new flow easy to verify through existing read endpoints.

Files affected:

- `src/ClaimsModule.Application/Reserves/CreateReserve/`
- `src/ClaimsModule.API/Controllers/ClaimsController.cs`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- `POST /api/claims` returned `201 Created`
- `POST /api/claims/{claimId}/reserves` with amount 5000 returned `201 Created` and status `Approved`
- `POST /api/claims/{claimId}/reserves` with amount 15000 returned `201 Created` and status `PendingApproval`
- `GET /api/claims/{id}` showed the created reserves in claim detail
- claim detail audit log included `ReserveCreated`
- non-empty missing claim ID returned `404 Not Found`
- invalid reserve amount returned `400 Bad Request`

Follow-up needed:

- Review and approve Phase 5B before adding manual reserve approval and rejection.

## Entry: 2026-07-03 - Phase 5B Reserve Approval And Rejection

What I asked AI to do:

- Add only manual approval and rejection for pending reserves.
- Do not add Hangfire GL posting, actual GL posting, frontend, real authentication, payments, or documents.

What AI generated:

- `ApproveReserveCommand`.
- `ApproveReserveCommandValidator`.
- `ApproveReserveCommandHandler`.
- `ApproveReserveResponse`.
- `RejectReserveCommand`.
- `RejectReserveCommandValidator`.
- `RejectReserveCommandHandler`.
- `RejectReserveResponse`.
- `PATCH /api/claims/{claimId}/reserves/{reserveId}/approve`.
- `PATCH /api/claims/{claimId}/reserves/{reserveId}/reject`.

What I reviewed:

- Required Phase 5B instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Build output before and after changes.

What I accepted:

- `200 OK` for successful approval or rejection.
- `404 Not Found` for non-empty missing claim or reserve IDs.
- `400 Bad Request` for validation and missing or inactive actor users.
- `403 Forbidden` when a handler tries to approve or reject.
- `422 Unprocessable Entity` for self-approval, self-rejection, and invalid reserve state.
- `ReserveApproved` and `ReserveRejected` audit entries with reserve, amount, currency, actor, and reason details.

What I rejected:

- Hangfire GL posting.
- Actual GL posting.
- Real authentication or authorization framework.
- Frontend work.
- Payments or documents.

What I learned:

- Seeded mock users are enough to demonstrate supervisor and manager authorization for the MVP.
- Manual reserve workflow can reuse the existing Phase 2 reserve fields, so no migration is needed.

Files affected:

- `src/ClaimsModule.Application/Reserves/ApproveReserve/`
- `src/ClaimsModule.Application/Reserves/RejectReserve/`
- `src/ClaimsModule.API/Controllers/ClaimsController.cs`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- `POST /api/claims` returned `201 Created`
- `POST /api/claims/{claimId}/reserves` with amount 15000 returned `PendingApproval`
- approving as the same user who created the reserve returned `422 Unprocessable Entity`
- approving as handler returned `403 Forbidden`
- approving as supervisor returned `200 OK` and status `Approved`
- claim detail audit log included `ReserveApproved`
- creating another pending reserve and rejecting as manager returned `200 OK` and status `Rejected`
- claim detail audit log included `ReserveRejected`
- approving/rejecting a missing reserve returned `404 Not Found`
- approving an already approved reserve returned `422 Unprocessable Entity`
- rejecting as the same user who created the reserve returned `422 Unprocessable Entity`

Follow-up needed:

- Review and approve Phase 6 before adding Hangfire GL posting simulation.
