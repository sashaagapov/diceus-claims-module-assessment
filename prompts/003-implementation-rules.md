# Prompt 003: Implementation Rules

Use these rules for every future implementation step in this repository.

Before coding:

1. Read `AGENTS.md`.
2. Read `docs/MVP_SCOPE.md`.
3. Read the current phase in `docs/IMPLEMENTATION_PLAN.md`.
4. Check `git status`.
5. Confirm that the requested work fits the current phase.

During coding:

- Work in small vertical slices.
- Keep controllers thin.
- Use MediatR for commands and queries.
- Use FluentValidation for request validation.
- Keep business rules visible and explainable.
- Use simple names.
- Avoid unnecessary abstractions.
- Add comments only for non-obvious rules or architecture boundaries.
- Do not add frontend work unless explicitly approved.
- Do not add real authentication unless explicitly approved.
- Do not commit secrets, tokens, `.env` files, or local credentials.

After coding:

1. Run relevant build/tests when possible.
2. Run `git status`.
3. Review changed files.
4. Update docs if scope or architecture changed.
5. Commit with a small meaningful message.
6. Push after the logical phase is complete.

Explain in the final response:

- what changed
- what was verified
- what was not verified and why
- what should be reviewed manually
- the recommended next step
