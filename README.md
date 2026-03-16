# cursor-rules

A starter template for [Cursor's](https://cursor.com) `.cursor/rules` — five markdown files that give AI full context on your project before you write a single line of code.

## Why this exists

Cursor rules are the single highest-leverage thing you can configure in a project. They tell the AI *what* you're building, *how* you build it, *what it should look like*, *where things go*, and *how to behave*. Without them, every conversation starts from zero. With them, the AI already knows your stack, your conventions, your design system, and your product.

These five files are stack-agnostic templates. They work for React, Python, Go, Rails, Swift, Flutter — anything. Every technology-specific decision is a `[bracketed placeholder]` with inline examples so you know what to fill in.

## What's included

```
.cursor/
└── rules/
    ├── global-rules.md   # AI behavior, communication style, guardrails
    ├── product.md         # What the product is, who it's for, roadmap
    ├── tech.md            # Stack, conventions, security, testing, deployment
    ├── design.md          # Components, states, spacing, colors, accessibility
    └── structure.md       # Folder layout, file placement, naming conventions
```

| File | What it does | Why it matters |
|---|---|---|
| **global-rules.md** | Defines how the AI should behave — when to ask vs. act, communication style, code quality standards | Prevents scope creep, unnecessary refactors, and verbose responses |
| **product.md** | Describes the product, users, key flows, roadmap, tone of voice, competitors | Lets the AI make contextually appropriate decisions instead of generic ones |
| **tech.md** | Documents the tech stack, coding conventions, data patterns, API structure, testing, deployment | Ensures consistent code that follows your standards without constant reminders |
| **design.md** | Covers component library, interaction states, spacing, colors, accessibility | Produces polished UI with proper loading states, empty states, and a11y from the start |
| **structure.md** | Maps the folder layout, file placement rules, naming conventions | Tells the AI exactly where to put new files — no more misplaced components |

## How to use

1. **Copy** the `.cursor/rules/` folder into your project root
2. **Open** each file and replace every `[bracketed placeholder]` with your project's details
3. **Delete** any lines marked *"Remove this line if not applicable"*
4. **Done** — every Cursor conversation in that project now has full context

All five files use `alwaysApply: true` in their frontmatter, so Cursor automatically includes them in every interaction. No need to `@` reference them manually.

## Tips for filling in the templates

- **Start with `product.md`** — it's the fastest to fill in and has the biggest impact. Even a rough draft dramatically improves AI output.
- **`tech.md` and `design.md`** include inline examples for many stacks (Next.js, Django, Rails, SvelteKit, etc.). Pick the ones that match yours and delete the rest.
- **`structure.md`** is most useful once you have an established folder layout. For brand new projects, fill it in after your initial scaffolding.
- **`global-rules.md`** works well with minimal changes — the behavioral guardrails are fairly universal. Focus on the Role section.
- **Don't fill in everything at once.** Start with what you know, and add detail as the project takes shape.

## Example: filled-in placeholder

Template version:
```
- [Primary framework, e.g. "Next.js App Router", "Django 5", "Rails 7", "SvelteKit", "FastAPI"].
  [Default pattern, e.g. "Server Components by default, 'use client' only when interactivity is needed".]
```

Filled-in version:
```
- Next.js 14 App Router. Server Components by default — only add 'use client' when you need
  browser APIs or interactivity.
```

## Contributing

Found a gap? Have a section that's helped your projects? PRs and issues are welcome.

## License

MIT — use it however you want.
