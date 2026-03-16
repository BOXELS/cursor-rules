---
description: Project folder structure and file placement conventions. Applies to all file creation and organization.
globs:
alwaysApply: true
---

# Structure Rules

## Project layout

<!-- Replace the tree below with your actual project structure. -->
<!-- Use comments to explain what each directory is for. -->

```
[project-root]/
├── [src or app directory]/
│   ├── [features or modules]/      # Feature-based grouping
│   │   ├── [feature-name]/
│   │   │   ├── [components]/       # Feature-specific components
│   │   │   ├── [hooks or utils]/   # Feature-specific logic
│   │   │   └── [tests]/            # Feature-specific tests
│   ├── [shared or common]/         # Shared utilities, types, constants
│   ├── [components]/               # Shared/global UI components
│   └── [styles or theme]/          # Global styles or theme configuration
├── [api or server directory]/      # API routes, server actions, or backend
├── [public or static]/             # Static assets
├── [config]/                       # Configuration files
├── [tests or __tests__]/           # Global/integration tests
└── [database or migrations]/       # Database schema and migrations
```

## File placement rules

- New features go in [feature directory path, e.g. "src/features/[feature-name]/", "app/(routes)/[feature-name]/"]. Each feature directory contains its own components, hooks, utils, and tests.
- Shared components used by 2+ features go in [shared components path, e.g. "src/components/", "src/shared/components/"].
- Utility functions go in [utils path, e.g. "src/lib/", "src/utils/", "src/shared/utils/"].
- Type definitions go in [types path, e.g. "src/types/", "co-located with the feature that owns them", "src/shared/types/"].
- API routes go in [API path, e.g. "app/api/", "src/pages/api/", "server/routes/"].
- Database migrations go in [migration path, e.g. "supabase/migrations/", "prisma/migrations/", "alembic/versions/"].
- Test files go [test location, e.g. "next to the file they test with .test.ts suffix", "in a __tests__/ directory mirroring src/", "in a top-level tests/ directory"].
- Configuration files (env, linting, build) stay in the project root.

## Naming conventions

- Directories: [convention, e.g. "kebab-case", "camelCase", "snake_case"].
- Components: [convention, e.g. "PascalCase files matching component name — Button.tsx exports Button", "kebab-case files — button.vue exports default"].
- Utilities and hooks: [convention, e.g. "camelCase — useAuth.ts, formatDate.ts", "snake_case — format_date.py"].
- Tests: [convention, e.g. "same name as source with .test.ts suffix", "test_ prefix for Python", ".spec.ts suffix"].
- Constants: [convention, e.g. "UPPER_SNAKE_CASE for values, camelCase for the file name"].

## When creating new files

1. Before creating a new file, check if a similar file already exists that could be extended.
2. Never create a file outside the defined structure without asking first.
3. If a new directory is needed, propose it and explain why before creating it.
4. [Max file length guideline, e.g. "If a file exceeds 300 lines, consider splitting it by responsibility." Remove this line if no preference.]
