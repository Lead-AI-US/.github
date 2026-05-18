# Lead.AI Technical Standards

## Repository Standards

- Every repository must include README, AGENTS, docs, issue templates, and a pull request template.
- Every repository must state product status honestly.
- Setup instructions must be real. If no runnable app exists, say so clearly.
- Use `.env.example` with placeholder names only.
- Keep docs updated when architecture, setup, or security assumptions change.

## Engineering Standards

- Prefer simple, modular architecture.
- Separate frontend, backend, AI orchestration, data storage, and integration code.
- Validate all user input.
- Avoid logging personally identifiable information.
- Add tests around scoring, qualification, auth, and data handling logic.
- Keep provider-specific logic behind adapters.

## API Standards

- Use structured request and response schemas.
- Return clear validation errors.
- Include example requests and responses in API docs.
- Add authentication before public or customer-facing use.
- Avoid exposing model internals, secrets, or private customer data.

## Documentation Standards

- Explain the business problem before the technical implementation.
- Include user flows and MVP plans.
- Include security and responsible AI notes.
- Add screenshots or demo links only when they exist.
