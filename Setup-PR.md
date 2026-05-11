## chore(setup): initialise project foundation with core dependencies and tooling

This PR establishes the complete project foundation for the DAICA backend. It sets up all core dependencies, development tooling, code quality enforcement, API documentation, and security/performance middleware before any feature development begins.

---

## What was added and why

**Runtime & Framework**
- `express` v5 — core HTTP framework, v5 picked for improved async error handling
- `dotenv` — environment variable management
- `cors` — cross-origin request handling
- `compression` — gzip response compression for performance

**Security**
- `helmet` — sets 14 security HTTP headers on every response, protects against XSS, clickjacking and CSP violations
- `express-rate-limit` — limits each IP to 100 requests per 15 minutes, protects against DDoS and brute force attacks
- `express-basic-auth` — protects the `/docs` swagger route in production

**Logging**
- `pino` — high performance structured JSON logger with sensitive field redaction. Passwords, tokens and auth headers are automatically censored in logs
- `pino-pretty` — makes logs human readable in development

**Validation**
- `zod` — runtime schema validation and type inference for all incoming request data

**API Documentation**
- `swagger-jsdoc` — generates OpenAPI spec from JSDoc comments in route files
- `swagger-ui-express` — serves interactive API docs at `/docs`

**TypeScript & Build**
- `typescript` v6 — TypeScript compiler
- `tsx` — fast TypeScript runner for development, replaces `ts-node`. Zero config, works with all modern tsconfig settings
- `tsc-alias` — resolves path aliases in compiled output after `tsc` runs
- `tsconfig-paths` — path alias resolution at runtime
- `ts-node` — kept as a fallback TypeScript runner

**Code Quality & Git Hooks**
- `eslint` + `typescript-eslint` — static code analysis with TypeScript specific rules
- `prettier` — automatic code formatting
- `husky` + `lint-staged` — runs prettier and eslint automatically on every commit. Zero warning tolerance enforced via `--max-warnings 0`

---

## Scripts

```
dev   → tsx src/server.ts         run locally
build → tsc && tsc-alias          compile TS and resolve path aliases
start → node dist/server.js       run compiled output in production
```

---

## Notes for Reviewers

- `nodemon` is currently in `dependencies` — should be moved to `devDependencies` before first production deploy
- `express-basic-auth` appears in both `dependencies` and `devDependencies` — remove the `devDependencies` entry to avoid duplication
- Swagger `/docs` route should be confirmed as protected behind basic auth before going to production

---

## Checklist

- [x] All dependencies installed and justified
- [x] Dev and prod dependencies correctly separated
- [x] Scripts cover dev, build and production start
- [x] Git hooks enforcing formatting and linting on every commit
- [x] No secrets or `.env` files committed
- [x] Security middleware in place
- [x] API documentation setup
- [x] Logging configured with sensitive field redaction

---

**Branch:** `setup` → `dev`
**Type:** `chore`
**Breaking changes:** None — this is the initial setup before any features
