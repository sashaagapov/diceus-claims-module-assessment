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
- Explain the intended change before large edits.
- Prefer backend correctness over frontend polish.
- Keep code simple, explicit, and explainable.
- Avoid full senior-level enterprise scope unless explicitly requested.
- Do not add features outside the MVP scope without updating documentation first.
- Use meaningful names and predictable folder structure.
- Avoid clever abstractions that hide important business rules.

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

After implementation steps, run build and tests when possible. If a step cannot be verified, document why.

Suggested checks for later phases:

- `dotnet build`
- `dotnet test`
- API smoke test through Swagger
- Database migration check

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

## Git Rules

Do not commit secrets, tokens, API keys, real credentials, local passwords, `.env` files, or generated junk.

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
