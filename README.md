# brain-damage

Agent Skills that make the agent **guide you** instead of doing the task for you.

> Are you tired about not doing by yourself? 
Are you tired about just watching the screen and everything get done by AI?! 
Did you get bored for just sitting and clicking? 
Don't worry, get back to the stone-age by installing this skill. 

---

Normal agent skills optimize for shipping fast: you ask, it writes, you merge. These do the
opposite. They put you at the keyboard and keep you there, because the point is that you get
better at the obstacle, not that the obstacle disappears.

Built on the [Agent Skills spec](https://github.com/anthropics/skills/blob/main/spec/agent-skills-spec.md).
Works in Claude Code and any agent that reads `SKILL.md`.

## Which one

| You want | Skill | Agent touches your files | Delivery |
| --- | --- | --- | --- |
| A skeleton to fill in — you're writing code now | [`no-spoon`](skills/no-spoon) | yes, scaffold + gap markers | incremental |
| The whole thing explained, you'll implement it | [`chalkboard`](skills/chalkboard) | never | one complete answer |

### `no-spoon`

Writes the scaffold into the real files — signatures, tests, and gaps marked `no-spoon:` with a
question that leads to the insight. You fill them. It escalates hints one rung at a time when you
stall, and never jumps to the answer.

Takes a guidance level, `1`–`4` (default `2`):

```
/no-spoon        signatures, docstrings, types and tests; empty bodies
/no-spoon 1      working code with 1-3 gaps
/no-spoon 3      file structure and tests only; you decide the decomposition
/no-spoon 4      blank file and a spec
```

Say `more` or `less` mid-task to move a level.

### `chalkboard`

Answers completely in chat — structure, mechanism, tables, diagrams, gotchas, what to do next —
and never writes implementation code or edits a file. Not coding-only; works for any subject.

```
/chalkboard      explain it fully, I'll do the doing
```

Both skills drop out of the way the moment you say "just fix it", and during a broken build,
a deploy, or an incident. Learning mode is not a hostage situation.

## Install

```
/plugin marketplace add <your-github-user>/brain-damage
/plugin install brain-damage@brain-damage
```

Or copy a skill folder into `~/.claude/skills/` (personal) or `.claude/skills/` (project).

## Layout

```
.claude-plugin/marketplace.json   plugin manifest
skills/<name>/SKILL.md            the skill
```

Adding a skill: make `skills/<name>/SKILL.md` with `name` and `description` frontmatter, then add
`./skills/<name>` to the `skills` array in the manifest. Keep `SKILL.md` short — the `description`
is the only part always in the agent's context, and it is what decides whether the skill fires at
all.
