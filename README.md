# claude-skills

My Claude Code skills, packaged as a plugin marketplace so they can be installed on any machine.

## Install

In a Claude Code session:

```
/plugin marketplace add sherifzayed/claude-skills
/plugin install sherif-skills@sherifzayed-skills
```

Or from a shell:

```
claude plugin marketplace add sherifzayed/claude-skills
claude plugin install sherif-skills@sherifzayed-skills
```

To pick up new skills later, run `/plugin marketplace update sherifzayed-skills`.

## Skills

| Skill | What it does |
| :- | :- |
| `r3f-declarative-jsx` | Keeps React Three Fiber scenes as declarative JSX: no `scene.add`, `<primitive>` or `new THREE.*` materials. |

## Adding a skill

Add a folder under `plugins/sherif-skills/skills/<skill-name>/` with a `SKILL.md`, bump `version` in `plugins/sherif-skills/.claude-plugin/plugin.json`, and run `claude plugin validate .` before pushing.
