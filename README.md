# help-me-help-you

Three agent skills built on one idea: rather than guessing what you want or handing you a wall of text, the agent asks pick-an-option questions. It does the hard part (finding the decisions and the sensible options) and you do the easy part (picking).

| Skill | What it does |
|---|---|
| [`grill-me`](skills/grill-me/SKILL.md) | Before a task, asks about the decisions it involves, recommended option first, then does the task your way. Use `grill-me extensive` for delicate tasks. |
| [`help-me-review`](skills/help-me-review/SKILL.md) | Turns a code review into choices: a fix-or-rewrite verdict, then the decisions the code made for you to confirm or override, then the quality fixes. |
| [`help-me-understand`](skills/help-me-understand/SKILL.md) | Teaches code, docs or any material through short quizzes and explains only what you got wrong. |

They work in Claude Code, Cursor, and any agent that supports [Agent Skills](https://agentskills.io). In environments with a multiple-choice tool (such as AskUserQuestion in Claude Code) they use it. Elsewhere they write lettered options in chat so you can reply with something like `1A, 2C`.

All three run only when you invoke them by name. The agent never starts them on its own.

## Install

### Any agent (Claude Code, Cursor, Codex, ...)

```sh
npx skills add shardulvs/help-me-help-you
```

Add `-g` to install for your user rather than the current project.

### Claude Code plugin

```
/plugin marketplace add shardulvs/help-me-help-you
/plugin install help-me-help-you@help-me-help-you
```

Plugin skills are namespaced, so you invoke them as `/help-me-help-you:grill-me` and so on.

## Usage

```
/grill-me add CSV export to the reports page
/grill-me extensive migrate the auth service to the new session store
/help-me-review the current branch
/help-me-understand src/scheduler/
```

## License

[MIT](LICENSE)
