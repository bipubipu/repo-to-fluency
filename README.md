# repo-to-fluency

A Claude [Agent Skill](https://support.claude.com/en/articles/12512176-what-are-skills) that turns a well-maintained open-source repository into a structured engineering-skill workout — for intermediate-and-up developers building real code-reading *judgment* (spotting good vs. bad design on sight), not just language familiarity.

Part of a planned `repo-to-` family of skills, each pointed at a different goal you can pursue by reading a real codebase:
- **`repo-to-fluency`** (this one) — level up your programming/engineering skill: language idioms, design judgment, code-quality instincts.
- `repo-to-contributor` *(planned)* — the opposite goal: onboarding as a first-time contributor to a *specific* project — its conventions, contribution process, and how to land a good PR. Different problem, different skill, even though both start with "open a repo."

## What it does

When activated, Claude will:
- Help pick an appropriately-sized, well-regarded repo to study based on your language/domain
- Sequence the reading in architectural order (entry point → core data model → state layer → abstractions → error handling → utilities), not file-tree order
- Run a repeatable per-file loop: read cold → check your read → ask "what would a junior dev do differently, and why is this better" → generalize one unfamiliar construct
- Design active-recall exercises once you're warmed up: rewrite-from-memory, bug injection, PR-review simulation

It's language-agnostic — built for Python originally but written to generalize. It explicitly does **not** cover contributor-onboarding tasks (contribution guidelines, project conventions, PR etiquette) — that's a different skill in the family.

## Install

### Claude Code
```bash
git clone https://github.com/bipubipu/repo-to-fluency.git
```
(Use `.claude/skills/` inside a specific project instead of `~/.claude/skills/` if you only want it scoped to that repo.) Start a new session — ask "what skills do you have available?" to confirm it loaded.

### Claude.ai
Download this repo as a zip, then upload the `repo-to-fluency` folder via **Settings > Features > Skills**. Requires a Pro, Max, Team, or Enterprise plan with code execution enabled. Note: custom skills uploaded this way are personal to your account, not shared org-wide.

### Claude API
Upload via the [Skills API](https://docs.claude.com/en/api/skills-guide#creating-a-skill).

## Usage

Just ask naturally — no special syntax needed:
- "Help me learn from the requests library"
- "Recommend a repo to study to get better at reading production code"
- "Review this function like a strict senior engineer would"

## License

Apache 2.0 — see [LICENSE](LICENSE).
