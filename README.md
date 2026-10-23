# m-skills

Personal Claude skills.

| Skill | What it does |
|---|---|
| [no-slop-grenade](skills/no-slop-grenade/SKILL.md) | Turns a session's findings into one sentence, "I observe X, based on Y it can be Z.", with the right detail for a colleague, manager or client. |

## Install

Copy a skill folder into `~/.claude/skills/` (personal) or `.claude/skills/` (per project):

```sh
cp -r skills/no-slop-grenade ~/.claude/skills/
```

Then invoke with `/no-slop-grenade`, or let it trigger automatically when you ask to share findings.
