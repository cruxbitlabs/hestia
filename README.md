# Hestia Todo for AI agents

[Hestia Todo](https://cruxbitlabs.com/) is a to-do app that keeps your lists on your own computer. This repository
holds what AI tools need to use Hestia as your to-do list: when you plan a trip, your bills or your chores with an
agent, it saves the plan in Hestia instead of leaving it in the chat.

- `skills/hestia-todo/SKILL.md`: the skill. It tells an agent when and how to use Hestia.
- `rules/`: a short always-on rule, for tools that read one at every start.
- `.claude-plugin/`: the same skill as a Claude plugin, for the Claude app and Claude Code.

Nothing here holds a key, a path or a program. Every tool still needs the **Hestia app** on the computer: the app adds
the `hestia-todo` connection to each tool and keeps its key in the computer's credential store.

## The easy way: from the Hestia app

In Hestia, open **Settings → Agent connections → Add agent**, pick **Claude**, **Codex**, **Gemini** or **Grok**, then
click **Add to …**. Hestia sets up the tool and its desktop app (Claude Desktop, the Codex app, Antigravity), and
installs the skill and the rule. Nothing else on this page is needed.

## The Claude app (Claude Desktop and claude.ai)

Claude keeps skills in your Claude account, so they are added in Claude itself:

- From Hestia: after adding Claude, click **Add Hestia's skill to Claude**. Claude opens and asks you to install it.
- Or in Claude: **Customize → Plugins → Add → Add marketplace**, enter `cruxbitlabs/hestia`, then install
  **hestia-todo**.
- Or with a file: in Hestia, **Save it as a file**, then in Claude **Customize → Plugins → Add → Upload plugin** and
  pick that file.

## Claude Code

```
/plugin marketplace add cruxbitlabs/hestia
/plugin install hestia-todo@cruxbitlabs
```

## Codex, Gemini CLI, Grok Build and other agents that read skills

```
npx skills add cruxbitlabs/hestia -g
```

Or copy the folder and the rule by hand:

| Tool | Skill: copy `skills/hestia-todo/` into | Always-on rule |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `rules/hestia-todo.md` into `~/.claude/rules/` |
| Codex (CLI and app) | `~/.agents/skills/` | add `rules/codex-AGENTS-section.md` at the end of `~/.codex/AGENTS.md` |
| Gemini CLI | `~/.agents/skills/` | none needed: it reads Hestia's server instructions |
| Grok Build | `~/.grok/skills/` | `rules/hestia-todo.md` into `~/.grok/rules/` |
| Antigravity | — | `rules/antigravity/hestia-todo.md` into `~/.gemini/config/rules/` |

On Windows, `~` is your user folder, for example `C:\Users\<you>`.

## For AI agents

If a user asks you to set up Hestia Todo for you:

1. **The connection comes from the Hestia app**, never from this repository. If your `hestia-todo` tools aren't
   available, ask the user to open Hestia, go to **Settings → Agent connections → Add agent**, pick your tool and click
   **Add to …**. Never ask the user for a key, and never put one in a settings file.
2. **Install the skill:** run `npx skills add cruxbitlabs/hestia -g`, or copy `skills/hestia-todo/` into your skills
   folder (see the table above). In Claude Code, use the two `/plugin` commands above.
3. **Add the always-on rule** where your tool reads one (see the table). When a file such as `AGENTS.md` already
   exists, add Hestia's section at the end and leave everything else as it is.
4. **From then on**, whenever the user plans, organises or wants to remember something they'll do, save it in Hestia
   as the skill describes, and tell them in a line or two what you saved.

## About these files

They are generated from the Hestia app's source (`agent-kit/` in the app's repository) and updated here with each
release that changes them. The skill's text inside `<!-- hestia-todo … -->` lets the Hestia app replace an old copy
with its own on the next setup; a copy you edit and that loses that line is left alone.
