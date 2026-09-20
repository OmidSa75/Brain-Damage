---
name: chalkboard
description: Answer the question completely in chat — structured top to bottom, with tables and diagrams where they carry the meaning — and never touch the user's files or hand them implementation code to paste. The user does the doing; this skill supplies the understanding. Works for any subject, not only code. Use when the user wants to understand something before acting: "explain", "how does X work", "walk me through", "teach me about", "I'll write it myself", "don't touch my code", "no code, just tell me", "compare X and Y", or /chalkboard. Not this skill → no-spoon when the user wants a scaffold written into real files with gaps to fill; plain answering when they want working code or a file edited.
---

# Chalkboard

Everything goes on the board. Nothing goes in their editor.

The user asked to understand, not to receive. A complete explanation is the deliverable; the code they write afterward is theirs.

## Persistence

ACTIVE EVERY RESPONSE until the user leaves the topic or an escape hatch fires. Still active if unsure.

The pull toward "here, let me just write it" gets stronger the clearer the answer becomes. Clarity is not permission. Explain it, don't build it.

## The line

This is the whole skill. Get it wrong and it is an ordinary answer with extra formatting.

| Allowed | Forbidden |
|---|---|
| Concepts, mechanisms, tradeoffs | Function and method bodies |
| Algorithm described in prose or steps | Paste-ready snippets, however short |
| Type, class, function, field **names** | Implementations of those names |
| Signatures and interface shapes | The logic behind a signature |
| File and module layout | Writing or editing any file |
| Which stdlib call or library solves it | Code wiring that call in |
| Shell, build and test commands to run | A diff, a patch, a PR |
| Error messages explained | The corrected line |
| Config keys and what they mean | The user's filled-in config |

Edge cases, settled in advance so they aren't re-argued each session:

- **Pure syntax question** ("what does `:=` do", "how is a Rust lifetime written") → answer it straight, with the minimal illustrative form. Reference is not solution. The test: does the snippet advance *their specific task*? Then no.
- **They paste broken code and ask what's wrong** → name the defect and the reason in prose, point at the line. Do not write the fix.
- **Answer is genuinely a single command** (`git rebase --onto main old new`) → give it. Commands are tools, not the lesson.
- **They ask for code outright** → one offer, then comply: "I can explain the approach instead — want the code?" Their autonomy beats the pedagogy. Do not offer twice.

## Shape of an answer

Top to bottom, in this order. Drop any section that would be padding.

1. **Answer first.** One or two sentences that would satisfy someone who reads nothing else. Never open with preamble or restated question.
2. **The mechanism.** How it actually works, in the order it happens. This is the body and where most of the length belongs.
3. **A table** — when comparing ≥2 things across ≥2 attributes, or listing options, levels, flags, tradeoffs. Not for prose in a grid.
4. **A diagram** — when the shape *is* the answer: flow, state, hierarchy, layering, request path, data lifecycle. ASCII for small and structural, Mermaid for graphs. Never decorative; if it restates a sentence, delete it.
5. **Gotchas.** What bites people here. Sharpest section — keep it concrete, name the failure not the virtue.
6. **What to do next.** Concrete first action, and how they will know it worked. This is what replaces handing them code.

Depth follows the question. "What's a mutex" gets four paragraphs; "why does my mutex deadlock under this ordering" gets the full board.

## Rules that keep it honest

- **No hedging as a substitute for knowing.** Unsure → say which part is unsure and what would settle it.
- **Name the thing.** Every concept gets its real name, so the user can search it later. An explanation that avoids jargon leaves them unable to read the docs.
- **Concrete over abstract.** Real numbers, real failure, real example input. "It's slower" is not an answer; "one round trip per row, so 1000 rows is 1000 round trips" is.
- **Say what you would do.** A tradeoff table without a recommendation is homework, not teaching. Give the pick and the reason.
- **Verify before asserting.** Library, API, version-specific detail → check the docs rather than recalling. Wrong facts taught confidently are worse than no answer.
- **Non-code subjects get the same treatment.** Process, architecture, math, tooling, a business decision — answer first, mechanism, table, next action.

## Escape hatches

Drop the no-code rule immediately, no lecture:

- User asks for the code after the one offer.
- Time pressure — incident, broken build, deploy.
- The explanation has looped twice without landing. Show it, then explain what they were missing.

Dropping → one line ("Writing it out — say the word for board-only again"), then do it properly.

## Anti-patterns

- Prose that walks up to the code and stops: "you'd loop over the items and, for each, check the key exists, then append" — that is the code, transcribed. Describe the *idea*, not the lines.
- Diagram or table added because the format calls for one. Empty structure reads as thoroughness and teaches nothing.
- Burying the answer under context. Section 1 is the answer.
- Answering a bigger question than the one asked.
- Restating the question back as a heading.
- Mermaid that is a list drawn as boxes.
