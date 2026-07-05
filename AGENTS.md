# AI Agent Instructions

This repository is for a DICEUS Claims Module technical assessment. It must stay focused on a clear, backend-first MVP that an intern-level .NET developer can understand and explain.

## Read Before Coding

Before implementing any application code, read these files:

1. `docs/MVP_SCOPE.md`
2. `docs/IMPLEMENTATION_PLAN.md`
3. `docs/PROJECT_CONTEXT.md`
4. `docs/ARCHITECTURE_DECISIONS.md`

Do not start coding until the current phase and scope are clear.

## Working Style

- Work in small vertical slices.
- Split work into short, safe, reviewable phases.
- Give each phase one clear goal and avoid large multi-feature changes.
- Prefer commits that can be safely reverted independently.
- Do not bundle scaffold, business screens, backend changes, docs, and deployment into one commit.
- Explain the intended change before large edits.
- Prefer backend correctness over frontend polish.
- Keep code simple, explicit, and explainable.
- Avoid full senior-level enterprise scope unless explicitly requested.
- Do not add features outside the MVP scope without updating documentation first.
- Use meaningful names and predictable folder structure.
- Avoid clever abstractions that hide important business rules.

## Phase Discipline

- At the start of every phase, state the exact phase name and scope.
- Do only that phase, then stop.
- Do not continue into the next phase without explicit user approval.
- If a requested phase reveals a prerequisite, stop and report before doing unrelated work.
- Never leave large uncommitted work between phases.

## Architecture Rules

The planned backend follows Clean Architecture:

- `ClaimsModule.Domain`
- `ClaimsModule.Application`
- `ClaimsModule.Persistence`
- `ClaimsModule.Infrastructure`
- `ClaimsModule.API`

Expected request flow:

`Controller -> MediatR Command/Query -> FluentValidation -> Handler -> EF Core / DbContext -> Database -> Response`

Respect basic OOP principles:

- Encapsulate core domain behavior where practical.
- Keep controllers thin.
- Keep handlers focused on one use case.
- Keep validators focused on input validation.
- Avoid duplicated business rules.
- Avoid giant classes.

## Business Rules To Keep Visible

The following rules must be easy to find and explain:

- Claim/FNOL creation
- Claim status transitions
- Reserve approval thresholds
- Self-approval prevention
- Append-only audit log behavior
- Hangfire GL posting simulation
- GL posting idempotency protection

Add helpful comments for non-obvious business rules, but do not add comments that simply repeat the code.

## Testing And Verification

After implementation steps, run the smallest relevant verification set before committing. If a step cannot be verified, document why.

Backend-affecting changes:

- `dotnet restore ClaimsModule.sln`
- `dotnet build ClaimsModule.sln --no-restore`
- `dotnet test ClaimsModule.sln`

Frontend-affecting changes:

- `npm install` if dependencies changed or `node_modules` is missing
- `npm run build`
- `npm test` only if configured and stable

Documentation-only changes:

- Inspect changed Markdown.
- Confirm commands, paths, phase names, and limitations are accurate.

Use extra checks when relevant:

- API smoke test through Swagger
- Database migration check

## Commit And Push Policy

- Commit after each successful phase.
- Push after each successful commit unless the user explicitly says not to.
- Use clear commit messages, for example:
  - `chore: update agent workflow rules`
  - `chore: scaffold Angular frontend`
  - `feat: add claims dashboard`
  - `feat: add FNOL form`
  - `feat: add claim detail view`
  - `feat: add reserve actions`
  - `docs: update fullstack delivery notes`
- Do not commit secrets, tokens, API keys, real credentials, local passwords, `.env` files, or generated junk.

## Documentation

Update documentation after important architecture, scope, or tradeoff decisions.

Use `docs/AI_WORKFLOW.md` to log AI-assisted work:

- what was asked
- what was generated
- what was reviewed
- what was changed
- what was accepted or rejected
- what was learned
- which files were affected

## Safety Rules

- Never weaken backend business rules to make UI work easier.
- Never remove existing tests or reduce coverage without explicit user approval.
- Never replace the working backend architecture with a broad rewrite.
- Keep backend changes minimal when implementing frontend compatibility.
- Use Development-only CORS if a frontend phase needs browser access.
- Do not introduce real authentication, real GL integration, Azure deployment, CI/CD, or document upload unless the current phase explicitly asks for it.

## DICEUS Scope Awareness

- The current implementation started as a backend-first MVP.
- The original DICEUS assessment is fullstack and expects Angular frontend, backend, database, background jobs, documentation, and deployment.
- Frontend and deployment must be handled in later approved phases.
- Known gaps should be documented honestly rather than hidden.

## Recommended Frontend Phase Breakdown

Each frontend phase must build, be manually smoke-checked where applicable, committed, and pushed before moving on.

- Phase 8A: Angular scaffold only
- Phase 8B: frontend API layer, mock user context, app shell
- Phase 8C: claims list dashboard
- Phase 8D: FNOL create claim form
- Phase 8E: claim detail screen
- Phase 8F: reserve actions and status transitions
- Phase 8G: frontend docs and polish

## Future Phase Final Response

Every future phase response should report:

- phase completed
- files changed
- verification commands and results
- manual checks performed
- commit hash
- push result
- remaining gaps
- recommended next phase

## Git Rules

After every completed logical phase:

1. Run `git status`.
2. Review changed files.
3. Create a small meaningful commit.
4. Push to `origin`.

Example commit messages:

- `docs: initialize project context`
- `docs: define backend-first MVP scope`
- `docs: add implementation roadmap`
- `scaffold: create clean architecture solution`
- `feat: add claim creation flow`
- `feat: add reserve approval workflow`
- `infra: add Hangfire GL posting simulation`
- `docs: add demo script and tradeoffs`
