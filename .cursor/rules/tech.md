---
description: Tech stack, coding conventions, and engineering standards. Applies to all code files.
globs:
alwaysApply: true
---

# Tech Rules

## Language and framework

- [Primary language, e.g. "TypeScript strict mode", "Python 3.12+", "Go 1.22", "Rust stable"]. [Key constraint, e.g. "No 'any' types unless explicitly approved", "Type hints on all function signatures", etc.]
- [Primary framework, e.g. "Next.js App Router", "Django 5", "Rails 7", "SvelteKit", "FastAPI"]. [Default pattern, e.g. "Server Components by default, 'use client' only when interactivity is needed", "class-based views unless logic is trivial", etc.]
- [Styling approach, e.g. "Tailwind CSS utility classes", "CSS Modules", "styled-components", "SCSS with BEM"]. [Constraint, e.g. "Never write custom CSS unless the framework can't do it."]
- [Primary backend service, e.g. "Supabase", "Firebase", "AWS Amplify", "self-hosted Postgres"]. Don't introduce alternative services without asking.

## Code organization

- File naming: [convention, e.g. "kebab-case for files, PascalCase for components", "snake_case for all files", "PascalCase for classes, camelCase for utilities"].
- Group by [organization strategy, e.g. "feature, not by type", "module", "domain layer"].
- Imports: [import convention, e.g. "absolute paths with @/ alias", "relative imports within modules, absolute across modules"]. Group by: external libs → internal modules → components → types. Separate groups with blank lines.
- Functions should do one thing. If a function exceeds [threshold, e.g. "30 lines", "50 lines"], it should be split.

## Data and state management

- Validation: [validation library, e.g. "Zod", "Pydantic", "Joi", "class-validator"]. Never trust external data without validating. Validate at every trust boundary — client input, API params, webhook payloads, URL params. Prefer allowlists over denylists.
- Data fetching: [approach, e.g. "TanStack Query for client-side, server components for initial loads", "SWR", "RTK Query", "built-in framework loaders"]. [Anti-pattern to avoid, e.g. "Never use useEffect for data fetching", "No raw fetch calls without error handling."]
- State management: [approach, e.g. "React state + context for UI, server state libraries for async data", "Pinia for global state", "Zustand", "Redux Toolkit"]. [Constraint, e.g. "Never mix UI state and server state."]

## API and security

- API structure: [pattern, e.g. "Next.js Route Handlers in app/api/", "Django REST Framework viewsets", "FastAPI routers", "Express controllers", "Supabase Edge Functions"]. Always return proper status codes and typed responses.
- Database access: [constraint, e.g. "Never run raw queries from the client — all access goes through server-side routes or server actions", "Use the ORM for all queries", "Parameterized queries only — no string concatenation."]
- Auth: [approach, e.g. "Middleware for auth checks on protected routes", "Decorator-based auth", "Guard clauses"]. [Anti-pattern, e.g. "Never check auth inside individual page components."]
- Rate limiting: [approach, e.g. "upstash/ratelimit on all API endpoints", "Django throttle classes", "nginx rate limiting"]. Never expose unprotected endpoints to the public.

### Secrets and API keys

- [Secret management approach, e.g. "Environment variables with NEXT_PUBLIC_ prefix for client-safe values", ".env files with python-dotenv"]. Never hardcode API keys, URLs, or secrets.
- Distinguish between **public keys** (safe for the client — e.g. Supabase anon key, Stripe publishable key) and **secret keys** (server-only — e.g. OpenAI, Stripe secret key, service role keys). Secret keys must never appear in client-side code or bundles.
- Third-party API calls that require secret keys must go through server-side routes or edge functions. Never call external APIs with secrets directly from the browser. [Proxy approach, e.g. "Supabase Edge Functions", "Next.js Route Handlers", "Express API on Railway".]
- [Service role key pattern, e.g. "Supabase service role key is used only in Edge Functions and server-side code, never in the client." Remove this line if not applicable.]

### Output sanitization (XSS prevention)

- Never render raw HTML from user input, database content, or external APIs without sanitization.
- [Sanitization library, e.g. "DOMPurify", "sanitize-html", "bleach"]. Use it at every point where HTML is rendered from a non-hardcoded source.
- If the framework provides a raw-HTML escape hatch (`dangerouslySetInnerHTML`, `innerHTML`, `v-html`, `{@html}`), it requires sanitized input. Treat every use as a security-sensitive code path.
- For variable interpolation into HTML templates, escape the values. Never concatenate user-provided strings into HTML.
- [Content Security Policy, e.g. "CSP headers configured in next.config.js / netlify.toml / helmet middleware." Remove this line if not configured yet.]

### Admin and privileged access

- [Admin route protection, e.g. "Admin pages use ProtectedAdminRoute wrapper", "Django staff_member_required decorator", "RBAC middleware"]. Admin routes must have server-side role verification — never rely solely on hiding UI elements.
- [Role system, e.g. "Roles stored in user_roles table, checked via roles.includes('admin')", "Django groups and permissions", "CASL ability definitions"]. Describe where roles live and how they're checked.
- [Audit logging, e.g. "All admin actions logged to security_audit_logs table", "Django admin log", "custom audit middleware". Remove this line if not applicable yet.]
- Register new admin pages in [admin registry, e.g. "admin_pages table", "admin route config", "Django admin.py". Remove this line if not applicable.]

## Error handling

- [Strategy, e.g. "try/catch at the API boundary", "Result types", "Exception middleware"]. User-facing errors as [presentation, e.g. "toast notifications", "flash messages", "inline error states"]. Never swallow errors silently.

## Database

- [Database system, e.g. "PostgreSQL via Supabase", "MySQL", "MongoDB", "SQLite for dev, Postgres for prod"].
- [ORM or query approach, e.g. "Prisma", "Drizzle", "SQLAlchemy", "raw SQL with parameterized queries", "Supabase client SDK"].
- Migrations: [approach, e.g. "Supabase migrations in supabase/migrations/", "Alembic", "Prisma Migrate", "Django migrations"]. Never modify production data without a migration.
- [Naming convention, e.g. "snake_case table names, pluralized", "prefix all tables with app_", etc.]
- [Row-level security / access control, e.g. "RLS enabled on ALL tables. Every new table must have RLS enabled and at least one policy before it's used", "Multi-tenant row isolation via org_id", "Application-level access control in the ORM layer." Remove this line if not applicable.]
- Always verify table structure via MCP or type definitions before writing queries. Never assume column names or types from memory.

## Assets and storage

- Static assets: [approach, e.g. "public/ directory", "static/ directory", "CDN"]. User-uploaded content: [approach, e.g. "Supabase Storage", "S3", "Cloudinary"]. [Constraint, e.g. "Never store base64 in the database", "Always optimize images before upload."]

## Git

- Commits: [format, e.g. "conventional commits (feat:, fix:, chore:)", "descriptive present-tense messages"]. One logical change per commit. Never commit secrets or .env files.
- [Branch strategy if applicable, e.g. "Feature branches off main, squash merge PRs." Remove this line if not applicable.]

## Testing

- [Test framework, e.g. "Vitest for unit tests, Playwright for E2E", "pytest", "Jest + React Testing Library", "Go table-driven tests"]. Write tests for [scope, e.g. "every API route and critical user flow", "all business logic", "public API surface"]. [Constraint, e.g. "Don't skip tests to ship faster", "Tests required before merging to main."]

## Deployment

- [Hosting platform, e.g. "Vercel", "Railway", "AWS", "Fly.io", "self-hosted"]. [Deployment method, e.g. "Auto-deploy on push to main", "Docker containers", "serverless functions."]
- [Environments, e.g. "dev → staging → production", "local + production only"]. [Constraint, e.g. "Never deploy directly to production without staging verification." Remove this section if not decided yet.]
