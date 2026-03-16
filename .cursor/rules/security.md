---
description: Security checklist and guardrails. Applies to all code that handles user input, authentication, authorization, or external data.
globs:
alwaysApply: true
---

# Security Rules

These rules are non-negotiable. Unlike other template sections, most items here are not placeholders — they apply to every project regardless of stack.

## Output sanitization (XSS / HTML injection)

- Never render raw HTML from users, databases, or external APIs without sanitization. This includes rich text editors (TipTap, Quill, CKEditor), markdown renderers, and any content stored as HTML.
- If the framework provides a raw-HTML escape hatch (`dangerouslySetInnerHTML`, `innerHTML`, `v-html`, `{@html}`, `| safe`), treat every use as a security review point. The input must be sanitized before rendering.
- Use [sanitization library, e.g. "DOMPurify", "sanitize-html", "bleach", "bluemonday"] for all HTML rendering from non-hardcoded sources.
- When interpolating variables into HTML strings, escape them. Never concatenate user-provided strings directly into HTML markup.
- Sanitize on output, not just on input. Data may be safe when stored but dangerous in a new rendering context.
- When writing a sanitization function, use an allowlist of tags and attributes — not a denylist. Denylists miss new attack vectors.

## Secrets and API key management

- **Public keys** (safe for client): [list, e.g. "Supabase anon key, Stripe publishable key, analytics IDs"]. These can appear in client-side code.
- **Secret keys** (server-only): [list, e.g. "OpenAI API key, Stripe secret key, Supabase service role key, SMTP credentials"]. These must NEVER appear in client-side code, environment variables prefixed for client exposure, or client bundles.
- Third-party API calls requiring secret keys go through [server-side proxy, e.g. "Supabase Edge Functions", "Next.js Route Handlers", "Express API", "Django views"]. Never call OpenAI, Stripe (secret), or similar APIs directly from the browser.
- [Environment variable convention, e.g. "NEXT_PUBLIC_ prefix = client-visible. Everything else = server-only", "VITE_ prefix = client-visible". Audit your .env to verify no secret keys have the client prefix.]
- Never log secret keys, even in development. Never include them in error messages or API responses.
- [Secret rotation / vault, e.g. "Secrets managed in Vercel environment variables", "AWS Secrets Manager", "Doppler". Remove this line if not applicable yet.]

## Authentication and authorization

- Auth checks happen server-side. Client-side checks (hiding buttons, conditional rendering) are UX conveniences, not security.
- [Auth approach, e.g. "Supabase Auth with middleware on protected routes", "NextAuth.js session checks in Route Handlers", "Django login_required decorator".]
- Every API endpoint and server action must verify the caller's identity and permissions before performing work. No endpoint should assume "if the client called it, the user is authorized."
- [Role system, e.g. "Roles in user_roles table, checked via roles.includes('admin')", "Django groups", "CASL abilities". Describe where roles are stored and how they're checked.]
- Admin and privileged routes must use [admin protection, e.g. "ProtectedAdminRoute wrapper", "staff_member_required", "RBAC middleware"]. Never use the same route guard for regular users and admins.

## Database security

- [RLS policy, e.g. "Row Level Security enabled on ALL tables in Supabase. Every new table must have RLS enabled and at least one policy before it's used", "Application-level access control via ORM scoping". Remove this line if not applicable.]
- Parameterized queries only. Never concatenate user input into SQL strings — not in application code, not in migrations, not in seed scripts.
- [Service role usage, e.g. "Supabase service role key used only in Edge Functions for admin operations that bypass RLS. Every use must be justified and reviewed", "Django superuser queries scoped explicitly". Remove this line if not applicable.]
- Verify table structure via MCP or type definitions before writing queries. Column names and types change — don't rely on memory.
- [Audit logging, e.g. "Admin and privileged operations logged to security_audit_logs table with user ID, action, timestamp, and affected resource", "Django admin log". Remove this line if not applicable yet.]

## Input validation

- Validate at every trust boundary: form submissions, API parameters, URL params, webhook payloads, file uploads. Never trust client-side validation alone — it can be bypassed.
- [Validation library, e.g. "Zod schemas for all API inputs", "Pydantic models", "Joi", "class-validator"]. Define schemas once, reuse them.
- Prefer allowlists over denylists for accepted values (enum fields, file types, URL schemes).
- File uploads: validate type (check magic bytes, not just extension), enforce size limits [approach, e.g. "via SiteSettingsService", "configurable per route"], and store in [storage, e.g. "Supabase Storage", "S3"] — never on the application server's filesystem.

## Security headers and browser protections

- [CSP, e.g. "Content-Security-Policy configured in next.config.js / netlify.toml / helmet middleware. Script sources restricted to 'self' and explicitly trusted CDNs." Remove this line if not configured yet.]
- [CORS, e.g. "CORS configured to allow only the production domain and localhost in dev." Remove this line if not applicable.]
- [Cookie security, e.g. "All cookies set with httpOnly, secure, and sameSite=strict/lax." Remove this line if not managing cookies directly.]
- [CSRF, e.g. "CSRF tokens on all state-changing forms and API calls", "Framework handles CSRF automatically (Django, Rails)", "SameSite cookies provide CSRF protection". Remove this line if handled by the framework.]
- [Frame protection, e.g. "X-Frame-Options: DENY or CSP frame-ancestors: 'none'" to prevent clickjacking. Remove this line if not configured yet.]

## Sensitive operations

- Destructive or irreversible actions (account deletion, data purge, role changes) must require explicit confirmation and should be logged.
- Financial operations (charges, refunds, subscription changes) must happen server-side with idempotency protections.
- [Rate limiting on sensitive endpoints, e.g. "Login, signup, password reset, and API key generation are rate-limited via upstash/ratelimit", "Django throttle classes on auth views".]
- Never expose internal IDs, stack traces, or system details in production error responses.
