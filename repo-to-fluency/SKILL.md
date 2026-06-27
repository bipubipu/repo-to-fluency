---
name: repo-to-fluency
description: Use this for intermediate-and-up engineers who want to level up programming/engineering skill — language fluency, idioms, and design judgment — by reading a real-world codebase or open-source repo. The goal is judgment about code quality (reading code fast and telling if it's well-written), not just syntax. Trigger for "how do I learn from this repo", "recommend repos to study to get better at X", "help me get better at reading code", "I want to understand production-quality code", "how do I level up from intermediate to advanced." Also use to pick a repo to study, sequence which files to read first, or design active-recall exercises (rewrite-from-memory, bug-spotting, PR-review simulation) for a specific codebase. Works for any language. Do NOT use for onboarding a first-time contributor onto a specific project (contribution guidelines, conventions, submitting a PR) — that's contributor onboarding, not skill-building, even though both involve reading a repo.
---

# Repo to Fluency

A method for using a real, well-maintained codebase as a training ground for engineering skill — building two things at once: deeper language fluency, and the harder-to-teach skill of judging whether code is *good* — spotting smells, design tradeoffs, and idioms on sight rather than from memorized rules.

This skill is for someone who already knows the basics of a language but has a gap between "I can write code" and "I can read someone else's code fast and form a confident opinion about it." That gap doesn't close by reading best-practices articles — it closes by repeatedly predicting, then checking, against real code. It is explicitly aimed at intermediate-and-up engineers leveling up their craft — not at someone trying to learn a project's contribution process for their first PR.

## When to reach for this vs. just answering generically

If the person already named a specific repo or file, skip straight to the per-file loop below. If they haven't picked a repo yet, help them pick one first — repo choice matters more than people expect.

## Step 1: Pick the repo

Good criteria, in priority order:
1. **Well-regarded for its design**, not just popular. Popularity ≠ readable internals.
2. **Small enough to hold in your head.** A handful of core files, not a sprawling framework. You want to finish reading the core in days, not months.
3. **Matches the person's domain interest** (web backend, data, CLI tooling, etc.) so the patterns they learn transfer to what they'll actually build.
4. **Actively maintained**, so what they learn reflects current idiom, not a 10-year-old style.

If the person hasn't specified a language/domain, ask one quick question rather than guessing. If they have, recommend 2-4 repos with a one-line reason each, and suggest starting with the smallest/most approachable one to build confidence before moving to denser codebases.

## Step 2: Sequence the reading

Don't read alphabetically or top-to-bottom in the file tree. Read in *architectural* order — the order that mirrors how the system actually works:

1. **Public entry point** — the smallest file showing how a user of the library actually calls it. Builds orientation fast.
2. **Core data model** — the classes/structs representing the central concept (a `Request`, an `Order`, a `Document`). Good source of property/encapsulation patterns.
3. **State / orchestration layer** — wherever the real decision-making and statefulness lives (a `Session`, a `Manager`, a `Service`). This is usually where the most interesting design choices are.
4. **Abstraction / plugin layer** — interfaces, adapters, strategy patterns. Great for seeing *why* abstraction earns its complexity cost.
5. **Error handling** — the exception hierarchy or error-handling module. Small file, disproportionately instructive.
6. **Utilities and the rest** — lower priority, good for spotting small idioms once the core clicks.

Produce this as a concrete numbered list of actual filenames for the chosen repo, not generic categories — look up the real file structure rather than guessing from general familiarity, since repos restructure over time.

## Step 3: The per-file loop (repeat for each file)

This loop is the core mechanism — it works because it forces prediction *before* explanation, which is what actually builds judgment instead of just familiarity.

1. **Read cold.** No AI yet. Write 2-3 sentences: what does this file do, and what's one thing about its design you'd question or don't fully understand?
2. **Check your read.** Share your summary and question. Get confirmation or correction on what the file does.
3. **Ask the judgment question, every time:** "What's one design decision here a junior dev might do differently, and why is this version better?" This single question is the highest-leverage move in the whole method — it's what trains "good vs. bad" instinct rather than just comprehension.
4. **Generalize one construct.** Pick one unfamiliar language feature or pattern used in the file (a decorator, a context manager, a particular generic, whatever). Ask for 2 more real-world examples of that same construct elsewhere, so it's recognized in the wild, not just in this one file.

## Step 4: Active exercises (once 3-4 files feel comfortable)

These move the person from passive reading to retrieval, which is what makes it stick:

- **Rewrite-from-memory**: pick a small function, close the file, reimplement it from understanding alone, then diff against the real version line by line.
- **Bug injection**: take a real function and quietly introduce one subtle, realistic bug (off-by-one, wrong exception type, mutable default argument, swapped condition). The person finds it. This is the single best exercise for training a "this looks off" radar, because it mimics real code review.
- **PR-review simulation**: pick a function and review it as if it were just submitted as a pull request, as a strict senior engineer would. Do this once for a genuinely well-written function and once for a deliberately weaker one, so the contrast is explicit rather than abstract.

## Step 5: Checkpoint

Periodically check for architectural understanding, not just file-level understanding: "Could you explain this system's overall design to a teammate in five sentences?" If not, that's a signal to revisit the state/orchestration layer (step 2.3) — that's usually where the real design thinking lives, more than in any single function.

## Out of scope

If someone's actual goal is figuring out how to make their first contribution to a specific open-source project (understanding its contribution guidelines, codebase conventions, how to file a good PR), that's a different problem — onboarding into a community/process, not building general engineering judgment. Don't force this skill's exercises onto that situation; flag the distinction and hand off to a contributor-onboarding workflow instead, if one exists.

## Notes for whoever is running this skill (the AI side)

- Don't dump the whole plan as a wall of text upfront if the person is mid-conversation about a specific repo — deliver it as the next 1-2 concrete steps, and let the loop unfold turn by turn.
- When asked to quiz or review, actually *do* the exercise (paste a real-ish snippet, inject the bug, ask the judgment question) rather than describing the exercise in the abstract.
- Resist over-explaining a fix when the person hits a bug or confusion mid-exercise — ask "what would you check first" before giving the answer, to preserve the retrieval benefit.
