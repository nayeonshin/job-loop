# AGENTS.md

## Project overview
- Build a job-search automation loop for sourcing, filtering, deduping, ranking, and tracking job listings.
- Treat the spreadsheet as the primary user interface; avoid requiring the user to interact with the agent directly.
- Prefer small working loops over a large end-to-end system that is not reliable yet.
- Design each step so it is useful alone: gather jobs, filter jobs, check applied status, update spreadsheet, draft application content.
- Start with simple sources and workflows before adding harder browser automation such as LinkedIn.

## Commands that matter (build/test/lint)
- No build, test, lint, or run commands exist yet.
- Before claiming work is done, inspect the repo for newly added manifests or scripts and run the relevant verification commands.
- If no automated verification exists, perform a focused manual smoke test and describe exactly what was checked.
- Do not invent a command in this file unless it exists in the repo.

## Conventions
- Keep pipeline stages separate: gather first, filter second, dedupe/check applied status third, rank/recommend fourth, notify or update spreadsheet last.
- Gathering should collect broadly but prioritize jobs posted within the last day.
- Filtering should apply user criteria after gathering; do not discard raw gathered listings too early.
- Always preserve enough metadata to trace a recommendation back to the source listing.
- Store whether the user has already applied and use it to suppress duplicates.
- Prefer spreadsheet-readable outputs over agent-only summaries.
- Document manual user loops before automating them.
- When confused, model what the user would do manually and automate the smallest repeatable step.

## Boundaries (never touch)
- Do not modify `.git/` directly.
- Do not change global Git, shell, browser, or credential settings without explicit approval.
- Do not store secrets, passwords, cookies, or session tokens in the repo.
- Do not automate applying to jobs without explicit user approval.
- Do not send emails, submit forms, or contact employers unless the user explicitly asks for that action.
- Do not scrape or automate a site in a way that ignores its access rules or risks the user's account.

## How to verify your work before telling me it's done
- Confirm new outputs can be consumed from the spreadsheet or another explicit user-facing artifact.
- Verify dedupe behavior against already-applied or already-seen listings when that data exists.
- Verify gathered jobs include source URL, title, company, location, posting date if available, and retrieval date.
- Verify filtering criteria are documented in code or config, not hidden in an agent prompt.
- Report what was run, what passed, and what was not verified.
