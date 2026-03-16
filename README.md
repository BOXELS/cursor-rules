# cursor-rules

A starter template for [Cursor's](https://cursor.com) `.cursor/rules` — six template files that teach AI everything about your project so it builds what you actually want.

## What is this?

When you use Cursor to build an app, the AI starts every conversation knowing nothing about your project — your tech stack, your design preferences, who your users are, or how your code is organized. You end up repeating yourself constantly, and the AI makes generic choices that don't fit your vision.

**Cursor rules fix that.** They're markdown files that live in your project and automatically feed context to the AI in every conversation. The problem is, writing them from scratch is intimidating — especially if you're new to coding.

This template gives you six pre-structured rule files with `[bracketed placeholders]`. You don't need to fill them in manually. Just paste the starter prompt below into Cursor, and the AI will ask you about your project and fill everything in for you — including recommending a tech stack if you don't have one yet.

## What's included

```
.cursor/
└── rules/
    ├── global-rules.md   # How the AI should behave and communicate with you
    ├── product.md         # What you're building, who it's for, where it's going
    ├── tech.md            # Tech stack, coding conventions, security, deployment
    ├── security.md        # XSS prevention, secrets, auth, admin access, headers
    ├── design.md          # Visual style, components, colors, accessibility
    └── structure.md       # Folder layout, file naming, where things go
```

| File | What it does | Why it matters |
|---|---|---|
| **global-rules.md** | Sets the AI's behavior — when to ask vs. act, how to communicate, security awareness, MCP usage | Prevents the AI from changing things you didn't ask about or making assumptions |
| **product.md** | Describes your product, your users, key workflows, roadmap, and brand voice | The AI understands *what* you're building and makes decisions that fit your product |
| **tech.md** | Documents your tech stack, coding patterns, database, API structure, testing, deployment | Every file the AI generates follows your stack and conventions consistently |
| **security.md** | Covers output sanitization, secret management, auth/RBAC, database security, input validation, security headers | The AI never introduces XSS vulnerabilities, exposes API keys client-side, or skips server-side auth checks |
| **design.md** | Covers your component library, UI states, spacing, colors, accessibility | The AI produces polished UI with proper loading states, empty states, and responsive design |
| **structure.md** | Maps your folder layout, file naming rules, and where new files should go | The AI puts files in the right place instead of scattering them randomly |

## Quick start

### 1. Copy the rules into your project

Copy the entire `.cursor` folder (including the dot — it's a hidden folder that Cursor looks for automatically) into your project root. If you don't have a project yet, create an empty folder, open it in Cursor, and the AI will help you scaffold it.

### 2. Paste this prompt into Cursor

Open a **new chat** in Cursor (Agent mode) and paste this:
-----------------------------------------------------------
```
Switch to Plan mode. Read all six files in .cursor/rules/ — they are templates with
[bracketed placeholders] that need to be filled in for this project.

Your job is to interview me about my project and then fill in every bracket across all
six files. I may not be technical, so explain things in plain language and make
recommendations when I'm unsure.

Start with product.md:
- Ask me what I'm building, who it's for, and how it will make money (if that is a goal of the user).
- Ask about key user flows, roadmap priorities, brand voice, and competitors.

Then move to tech.md:
- Based on what I described, RECOMMEND a tech stack with clear reasoning.
- Present 2-3 options with pros and cons if there are meaningful tradeoffs.
- Ask about any preferences I already have (languages, frameworks, services).
- Once we agree on a stack, fill in all the tech conventions and patterns.

Then security.md:
- Based on the agreed tech stack, fill in the security placeholders.
- Ask which third-party APIs will be used and whether they need server-side proxying.
- Ask about admin/privileged access needs and how roles will be managed.
- Recommend a sanitization library and security header configuration for the stack.
- The non-placeholder rules in this file apply to every project — don't skip them.

Then design.md:
- Recommend a component library, icon set, and animation approach that fits the stack.
- Ask about visual style preferences (minimal, bold, playful, etc.).
- Fill in spacing, color approach, and accessibility level.

Then structure.md:
- Based on the agreed tech stack, propose a folder structure.
- Explain what each directory is for in simple terms.

Finally global-rules.md:
- Ask me about my experience level and how I prefer to work with AI.
- Fill in the role and behavioral preferences.
- Ask about MCP servers in use and fill in the MCP section.

For anything I say "not sure yet" or "skip" to, fill in sensible defaults based on
the rest of my answers and mark them with a comment so I can revisit later.

After filling in each file, show me a summary of what you wrote so I can approve or
adjust before you move to the next one. Don't edit any file until I confirm.

Start now — ask me about my product.
```
-----------------------------------------------------------

### 3. Answer the AI's questions

The AI will walk you through each file one at a time, starting with "what are you building?" You don't need to know technical details — it will explain options in plain language and make recommendations. Just describe your vision and the AI handles the rest.

### 4. Start building

Once all six files are filled in, every future Cursor conversation in your project automatically has full context. The AI knows your stack, your design system, your users, and your conventions. Start a new chat and begin building.

## How it works

All six files use `alwaysApply: true` in their [Cursor frontmatter](https://docs.cursor.com/context/rules-for-ai), which means they're automatically included in every AI interaction. You never need to reference them manually — they're always working in the background.

The `[bracketed placeholders]` include inline examples for many tech stacks (Next.js, Django, Rails, SvelteKit, FastAPI, Flutter, and more), so the AI has concrete options to recommend regardless of what you're building.

## FAQ

**Do I need to know how to code?**
No. The starter prompt is designed so the AI asks you about your *product* first (what are you building, who's it for) and then recommends technical decisions with explanations. You just need to know what you want to build.

**What if I don't know what tech stack to use?**
That's the point. Tell the AI what you're building and it will recommend a stack with reasoning. You pick the one that sounds right.

**Can I change things later?**
Yes. The rule files are just markdown. You can edit them anytime, or start a new chat and ask the AI to update a specific file based on how your project has evolved.

**What if I already have a tech stack?**
The starter prompt handles that too. When it gets to tech.md, just tell it what you're already using and it will fill in conventions for your stack instead of recommending a new one.

**Does this work with any programming language?**
Yes. The templates are completely stack-agnostic. The brackets contain examples for web, mobile, backend, and full-stack projects across many languages and frameworks.

## Contributing

Found a gap? Have a section that's made your projects better? PRs and issues are welcome.

## License

MIT — use it however you want.
