# Vocab Voyage — OpenClaw Quickstart

Add Vocab Voyage's vocabulary tools to OpenClaw in under a minute. No account required for public tools (60 requests/min anonymous). Sign in for personalized study queue, missed words, and adaptive plans (600 requests/hour authenticated).

- Server endpoint: `https://gponcrussdahcdyrlhcr.supabase.co/functions/v1/mcp-server`
- Transport: streamable-http
- Homepage: <https://vocab.voyage/mcp>

---

## Install (2 paths)

### Option 1 — ClawHub (recommended)

```bash
openclaw skills install vocab-voyage
```

This pulls the published skill from ClawHub (<https://clawhub.ai/jaideepdhanoa/vocab-voyage-mcp>) and registers it with your local OpenClaw runtime.

### Option 2 — Manual skill folder

Create the file `~/.openclaw/skills/vocab-voyage/SKILL.md` with the following contents:

```markdown
---
name: vocab-voyage
description: Vocabulary tools for SAT, ISEE, SSAT, GRE, GMAT, LSAT, PSAT prep — word of the day, definitions, quizzes, study plans.
metadata: { "openclaw": { "emoji": "📚", "homepage": "https://vocab.voyage" } }
---

This skill connects to the Vocab Voyage MCP server.

Server URL: https://gponcrussdahcdyrlhcr.supabase.co/functions/v1/mcp-server
Transport: streamable-http
Auth: optional Bearer token (vv_mcp_…) for personalized tools

Use this skill when the user asks for vocabulary definitions, quizzes, word of the day, or test prep word lists. Available tools: get_word_of_the_day, get_definition, generate_quiz, list_courses, get_course_word_list, explain_word_in_context, study_plan_preview.
```

Restart OpenClaw — the skill auto-loads from `~/.openclaw/skills`.

---

## Verify

```bash
openclaw skills list
```

You should see `vocab-voyage` in the output. If you do not, confirm the skill folder path and restart OpenClaw.

---

## Available tools

- `get_word_of_the_day` — today's vocab word, optionally scoped to a test family (ISEE, SAT, GRE, etc.)
- `get_definition` — definition, part of speech, example sentence, synonyms, antonyms
- `generate_quiz` — build a 1–10 question multiple-choice vocabulary quiz
- `list_courses` — discover available courses and their slugs
- `get_course_word_list` — sample words from any of the 13 test prep courses
- `explain_word_in_context` — explain what a word means inside a specific sentence
- `study_plan_preview` — a sample 7-day plan for a chosen test family

---

## Example prompts

### Word of the Day

- "What's today's SAT word of the day?"
- "Give me an ISEE word of the day with an example sentence I'd hear in 7th grade."
- "Show me today's GRE word of the day and use it in a science context."

### Quiz

- "Quiz me on 5 SAT vocabulary words."
- "Generate a 10-question GRE vocab quiz, then grade my answers as I go."
- "Give me a 5-question SSAT Upper Level quiz and explain every wrong answer."

### Mixed workflows

- "Define 'aberrant' and then quiz me on 3 similar SAT words."
- "Build me a 7-day SSAT study plan and start with today's word."
- "List the LSAT courses, sample 10 words from the hardest one, and quiz me on them."

---

## Optional auth (personalized tools)

Sign in at <https://vocab.voyage/mcp>, generate a personal MCP token (begins with `vv_mcp_`), and pass it as a bearer token. OpenClaw will forward it to authenticated tools that need your study queue or progress data.

```
Authorization: Bearer vv_mcp_YOUR_TOKEN
```

Token scopes: `mcp.read`, `mcp.tools`, `profile.read`, `progress.read`. See <https://vocab.voyage/developers/auth> for the full reference.

---

## Troubleshooting

- **Skill not appearing** — restart OpenClaw and re-run `openclaw skills list`. Confirm the file is at `~/.openclaw/skills/vocab-voyage/SKILL.md` (not nested in a subfolder).
- **`rate_limited` errors** — anonymous calls are capped at 60/min per IP. Authenticated tokens raise the cap to 600/hour. Honor the `Retry-After` header.
- **`unauthorized` errors on a personalized tool** — the tool requires a `vv_mcp_` token. Generate one at <https://vocab.voyage/mcp>.
- **`insufficient_scope` errors** — re-issue the token and include the scope listed in the `required_scopes` array of the error.
- **Server unreachable** — check <https://vocab.voyage/status> for live operational guidance.

---

## Links

- Install hub: <https://vocab.voyage/mcp>
- Auth & scopes: <https://vocab.voyage/developers/auth>
- Developer docs: <https://vocab.voyage/developers>
- Status: <https://vocab.voyage/status>
- ClawHub listing: <https://clawhub.ai/jaideepdhanoa/vocab-voyage-mcp>