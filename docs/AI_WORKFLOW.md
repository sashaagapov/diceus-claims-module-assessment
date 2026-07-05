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

## Entry: 2026-07-05 - Phase 8B Frontend API Layer And App Shell

What I asked AI to do:

- Add the Angular frontend API layer, mock user context, HTTP interceptors, and app shell only.
- Do not implement claims list, FNOL, claim detail, reserve UI, or any later frontend phase.

What AI generated:

- Strict TypeScript DTO models for policies, reference data, claims, reserves, audit log entries, and request/response payloads.
- Angular API services for claims, policies, and reference data using `inject(HttpClient)`.
- A mock `AuthContextService` seeded with Handler, Supervisor, and Manager users.
- HTTP interceptors for the `X-User-Id` mock header and global API error snackbars.
- A Material toolbar shell with placeholder navigation and a mock user selector.
- Placeholder routed pages for future `Claims` and `New Claim` screens.

What I reviewed:

- Existing backend endpoint and DTO shapes.
- Current Angular scaffold structure.
- Phase 8B scope limits from `AGENTS.md`.

What I changed manually:

- Kept frontend routes as placeholders so business screens remain out of scope.
- Documented the mock-user-header simplification as a tradeoff.

What I accepted:

- Frontend infrastructure needed by later approved phases.
- Angular Material app shell and user selector.

What I rejected:

- Claims dashboard, FNOL form, claim detail UI, reserve actions UI, NgRx, real authentication, and backend business-rule changes.

What I learned:

- The backend currently receives actor IDs in request bodies; the frontend mock header is useful shell context but is not real authentication.

Files affected:

- `frontend/claims-module-web/src/environments/`
- `frontend/claims-module-web/src/app/core/`
- `frontend/claims-module-web/src/app/features/placeholder-page/`
- `frontend/claims-module-web/src/app/app.*`
- `frontend/claims-module-web/src/app/home/home.html`
- `README.md`
- `docs/AI_WORKFLOW.md`
- `docs/TRADEOFFS.md`

Verification performed:

- `npm run build`
- `npm test -- --watch=false`
- `npm start`
- Manual shell check at `http://localhost:4200` with toolbar, placeholder home page, navigation links, and mock user selector.
- Swagger check at `http://localhost:5188/swagger/index.html`.
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet test ClaimsModule.sln`

Follow-up needed:

- Review and approve Phase 8C before implementing the claims list dashboard.

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

## Entry: 2026-07-03 - Phase 6 Hangfire GL Posting Simulation

What I asked AI to do:

- Add only Hangfire-backed simulated GL posting for approved reserves.
- Do not add frontend, real authentication, real GL integration, payments, or documents.

What AI generated:

- Hangfire SQL Server configuration in API startup.
- Development-only Hangfire dashboard at `/hangfire`.
- `ReserveGlPostingJob`.
- `ReserveGlPostingJobQueue`.
- `IReserveGlPostingJobQueue`.
- GL posting enqueue from auto-approved reserve creation.
- GL posting enqueue from manual reserve approval.
- `GlPostedAtUtc` and `GlPostingReference` fields in claim detail reserve summaries.

What I reviewed:

- Required Phase 6 instructions and existing project documents.
- Repository cleanliness before coding.
- .NET SDK version through `global.json`.
- Build output before and after changes.

What I accepted:

- Hangfire uses the existing `DefaultConnection` SQL Server database.
- Hangfire creates its own storage tables; no EF migration was created.
- Approved reserves enqueue a posting job.
- Pending and rejected reserves are not enqueued for GL posting.
- The job no-ops when a reserve is not `Approved`.
- The job no-ops when `GlPostedAtUtc` is already set.
- Successful simulated posting sets `GlPostedAtUtc`, sets `GlPostingReference`, and writes `ReserveGlPosted`.

What I rejected:

- Real external GL or accounting integration.
- Frontend work.
- Real authentication.
- Payments or documents.

What I learned:

- The existing reserve schema already had the GL posting fields needed for the Phase 6 job.
- Exposing GL posting fields in claim detail makes the asynchronous job easy to verify through Swagger/API.

Files affected:

- `src/ClaimsModule.API/Program.cs`
- `src/ClaimsModule.API/ClaimsModule.API.csproj`
- `src/ClaimsModule.Application/Interfaces/IReserveGlPostingJobQueue.cs`
- `src/ClaimsModule.Application/Reserves/CreateReserve/CreateReserveCommandHandler.cs`
- `src/ClaimsModule.Application/Reserves/ApproveReserve/ApproveReserveCommandHandler.cs`
- `src/ClaimsModule.Application/Claims/GetClaimById/`
- `src/ClaimsModule.Infrastructure/BackgroundJobs/`
- `src/ClaimsModule.Infrastructure/DependencyInjection.cs`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- Development Hangfire dashboard at `/hangfire` returned `200 OK`
- API startup created Hangfire SQL storage tables through Hangfire storage, not EF migrations
- `POST /api/claims` returned `201 Created`
- `POST /api/claims/{claimId}/reserves` with amount 5000 returned status `Approved`
- the auto-approved reserve was posted by Hangfire and claim detail showed `GlPostedAtUtc`, `GlPostingReference`, and `ReserveGlPosted`
- `POST /api/claims/{claimId}/reserves` with amount 15000 returned status `PendingApproval`
- pending reserve detail showed no GL posting before approval
- approving the pending reserve returned `200 OK`, then Hangfire posted it and claim detail showed `ReserveGlPosted`
- rejecting another pending reserve returned `200 OK`, and claim detail showed no GL posting fields for the rejected reserve
- manually invoking the GL posting job twice for an already-posted reserve did not change its `GlPostingReference` and did not add another `ReserveGlPosted` audit entry

Follow-up needed:

- Review the completed backend MVP flow before deciding whether to polish Swagger samples or add an optional frontend.

## Entry: 2026-07-03 - Phase 7A Backend MVP Hardening And Swagger Demo Polish

What I asked AI to do:

- Harden and polish the completed backend MVP demo flow.
- Do not add frontend, real authentication, real GL integration, payments, documents, automated tests, or new business features.

What AI generated:

- README demo flow with run commands, endpoint sequence, seeded IDs, and sample JSON bodies.
- `docs/DEMO_CHECKLIST.md` with commands, endpoints, expected outputs, and common errors.
- Tradeoff status update for the completed backend demo polish phase.

What I reviewed:

- Required Phase 7A instructions and existing project documents.
- Repository cleanliness before edits.
- .NET SDK version through `global.json`.
- Existing API surface and obvious issue scan.
- Build output before documentation changes.

What I accepted:

- Documentation-first Swagger/demo polish.
- README sample requests instead of heavier Swagger customization packages.
- A concise checklist for reviewers and future manual demos.

What I rejected:

- Frontend work.
- Real authentication.
- Real GL integration.
- Payments or documents.
- New business behavior.
- Automated tests in this phase.

What I learned:

- The current API surface is reviewable through Swagger without adding new Swagger packages.
- A checklist is enough to make the backend MVP demo repeatable while keeping Phase 7A low risk.

Files affected:

- `README.md`
- `docs/DEMO_CHECKLIST.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet tool run dotnet-ef database update --project src/ClaimsModule.Persistence --startup-project src/ClaimsModule.API`
- API smoke test: `GET /health` returned `200 OK` with response body `OK`
- Swagger UI at `/swagger/index.html` returned `200 OK`
- Development Hangfire dashboard at `/hangfire` returned `200 OK`
- `GET /api/policies` returned seeded policies
- `GET /api/cause-of-loss-codes` returned seeded cause-of-loss codes
- `POST /api/claims` returned `201 Created`
- `GET /api/claims/{id}` returned claim detail with parties, risk objects, and audit log entries
- `PATCH /api/claims/{id}/status` from `Open` to `UnderInvestigation` returned `200 OK`
- invalid status transition returned `422 Unprocessable Entity`
- `POST /api/claims/{claimId}/reserves` with amount 5000 returned `Approved`, and Hangfire added GL posting fields plus `ReserveGlPosted`
- `POST /api/claims/{claimId}/reserves` with amount 15000 returned `PendingApproval`
- approving the pending reserve as supervisor returned `200 OK`, and Hangfire added GL posting fields plus `ReserveGlPosted`
- rejecting another pending reserve as manager returned `200 OK`, and the rejected reserve had no GL posting fields
- handler approval attempt returned `403 Forbidden`
- self-approval attempt returned `422 Unprocessable Entity`

Follow-up needed:

- Consider automated integration tests as a separate hardening phase.

## Entry: 2026-07-05 - Phase 7B Automated Backend Integration Tests

What I asked AI to do:

- Add automated integration tests for the existing backend MVP flow only.
- Do not add frontend, real authentication, real GL integration, payments, documents, or new business features.

What AI generated:

- `tests/ClaimsModule.IntegrationTests` xUnit project.
- `Microsoft.AspNetCore.Mvc.Testing` API test host setup.
- SQL Server-backed test factory that creates and drops a temporary database per test run.
- Integration tests for health, lookup endpoints, FNOL claim creation, claim list/detail, status transitions, reserve rules, Hangfire GL posting, and GL posting idempotency.
- Test setup notes in `tests/ClaimsModule.IntegrationTests/README.md`.

What I reviewed:

- Required Phase 7B prompt and repository documents.
- Repository cleanliness before changes.
- .NET SDK version through `global.json`.
- Baseline restore/build output.
- Test failures from unavailable Docker, SQL Server Testcontainers instability, and enum JSON deserialization.

What I changed manually:

- Added `public partial class Program` so `WebApplicationFactory<Program>` can host the API.
- Switched from Testcontainers to the existing Docker Compose SQL Server after SQL Server Testcontainers proved unstable under local Docker Desktop resource limits.
- Added JSON enum converter options to the test helpers to match API enum serialization.

What I accepted:

- Real HTTP-level integration tests using the API pipeline and SQL Server persistence.
- A temporary database per test run for isolation.
- Direct `ReserveGlPostingJob` idempotency verification after Hangfire posts the approved reserve once.

What I rejected:

- Frontend work.
- Real authentication.
- Real GL integration.
- Payments or documents.
- Any production business-rule changes.

What I learned:

- The backend MVP flow is now covered by repeatable automated tests.
- SQL Server Testcontainers can be heavier than the local Docker Desktop resource limits in this environment; the existing compose SQL Server is simpler and explainable for this assessment.

Files affected:

- `ClaimsModule.sln`
- `src/ClaimsModule.API/Program.cs`
- `tests/ClaimsModule.IntegrationTests/`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet --version` returned `9.0.315`
- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `docker compose up -d`
- `dotnet test ClaimsModule.sln` passed with 5 tests

Follow-up needed:

- Review the automated test coverage and then decide whether Phase 8 documentation/cleanup is enough or whether any additional backend hardening is needed.

## Entry: 2026-07-05 - Phase 8A Angular Scaffold Only

What I asked AI to do:

- Create only the Angular frontend scaffold.
- Add routing, Angular Material, a basic app shell, a placeholder home page, and environment-based API base URL.
- Do not implement claims list, FNOL form, claim detail, reserves UI, mock auth, deployment, CI/CD, or backend business-rule changes.

What AI generated:

- Angular app under `frontend/claims-module-web`.
- Angular routing with a placeholder home route.
- Angular Material toolbar and placeholder card shell.
- Environment files with `apiBaseUrl` set to `http://localhost:5188`.
- Frontend local run documentation.

What I reviewed:

- `AGENTS.md`.
- Clean git status before the phase.
- Baseline backend restore, build, and integration test results.
- Local Node, npm, Angular CLI, and Angular Material compatibility.

What I changed manually:

- Replaced the generated Angular starter page with a minimal Claims Module app shell.
- Added a project-specific frontend README.
- Documented the frontend run commands in the root README.

What I accepted:

- Angular 21 scaffold because it is Angular 18+ and compatible with the local Node 25 runtime.
- Angular Material as the UI library.
- No backend CORS change yet because the scaffold does not call the API.

What I rejected:

- Claims list.
- FNOL form.
- Claim detail.
- Reserve actions.
- Mock authentication.
- Backend business logic changes.
- Azure deployment or CI/CD.

What I learned:

- Angular CLI 22 requires Node versions that exclude the local Node 25 runtime, while Angular CLI 21 supports it.
- The frontend can be scaffolded cleanly without changing backend behavior.

Files affected:

- `frontend/claims-module-web/`
- `README.md`
- `docs/TRADEOFFS.md`
- `docs/AI_WORKFLOW.md`

Verification performed:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet test ClaimsModule.sln`
- `npm install`
- `npm run build`
- `npm start`
- Manual browser check at `http://localhost:4200`
- Manual Swagger check at `http://localhost:5188/swagger/index.html`

Follow-up needed:

- Review and approve Phase 8B before adding the frontend API layer, mock user context, or app shell expansion.

## Entry: 2026-07-05 - Phase 8C Claims List Dashboard

What I asked AI to do:

- Add only the Angular claims list dashboard.
- Do not implement the FNOL form, claim detail screen, reserve UI, or any later frontend phase.

What AI generated:

- Standalone `ClaimsList` component under `frontend/claims-module-web/src/app/features/claims/`.
- Angular route wiring so `/` redirects to `/claims` and `/claims` loads the claims list.
- A placeholder `/claims/:id` route for future claim detail work.
- Material table UI with Claim Number, Loss Date, Status, and Actions columns.
- Loading and empty states for the claims list.
- Development-only CORS for the local Angular origin.

What I reviewed:

- `AGENTS.md`.
- MVP scope, implementation plan, project context, and architecture decisions.
- Existing Angular app shell and frontend API service.
- Backend API startup to keep the CORS change minimal and Development-only.

What I changed manually:

- Kept the `View` action as a placeholder route link instead of implementing detail UI.
- Updated documentation to show that the frontend now has a claims list but not FNOL/detail/reserve screens.

What I accepted:

- A simple Material table backed by `ClaimsApiService.getClaims()`.
- The smallest backend startup change needed for local browser API access.

What I rejected:

- FNOL form.
- Claim detail implementation.
- Reserve actions.
- Backend business-rule changes.
- Real authentication.

What I learned:

- Once Angular calls the API from the browser, local Development CORS is required for `http://localhost:4200`.

Files affected:

- `src/ClaimsModule.API/Program.cs`
- `frontend/claims-module-web/src/app/app.routes.ts`
- `frontend/claims-module-web/src/app/features/claims/`
- `README.md`
- `docs/AI_WORKFLOW.md`
- `docs/TRADEOFFS.md`

Verification performed:

- `npm run build`
- `npm test -- --watch=false`
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet test ClaimsModule.sln`
- `npm start`
- Manual browser check at `http://localhost:4200/claims`: claims table rendered backend data with Claim Number, Loss Date, Status, and Actions columns.
- Manual `View` action check: table link navigated to `/claims/:id` placeholder route.
- API smoke check: `GET http://localhost:5188/api/claims` returned local database claims.

Follow-up needed:

- Review and approve Phase 8D before implementing the FNOL create claim form.
