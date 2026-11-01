---
name: grill-me
description: Interview the user with pick-an-option questions to pin down their intent before doing a task, then do it the way they would have. Works for any task or goal, not just code. Two levels, normal (the default) and extensive (more questions, for delicate tasks), chosen with "grill-me extensive". Only use this skill when the user explicitly invokes it by name; never start it on your own.
disable-model-invocation: true
---

# grill-me

Before doing a task, find out what the user actually wants by asking pick-an-option questions, then do the task their way.

## Why this works

If you start a task straight away, you fill every gap in the request with your own guesses, and some of them won't match what the user would have chosen. Asking the user to spell everything out up front is slow, and they may not know enough to make every technical call from scratch. Grilling sits in between: you do the hard part (finding the decisions and the sensible options) and the user does the easy part (picking). Each answer is a point, and with enough points you can draw the line of decisions the user would have made themselves.

## Levels

Use the level the user asks for when invoking the skill (for example "grill-me extensive ..."). Default to normal.

- **normal**: ask only about decisions that would clearly change the result.
- **extensive**: the task is delicate, so also ask about smaller decisions the user would likely want a say in.

Asking more is the only difference between the levels.

## Grilling

If the user's message doesn't say what the task is, ask that first.

1. **Read first.** Look at everything you can reach (files, the codebase, docs, the conversation so far) before asking anything. Never ask something you could look up; questions are for intent and preferences.
2. **Find the decisions.** List the decisions the task involves and set aside the ones the context already settles. Ask first about decisions that shape other decisions; a question whose options depend on an earlier answer waits for that answer.
3. **Ask with options.** Give each question 2-4 concrete options. Put your recommended option first, mark it as recommended, and say why in a few words. Describe options by their consequences for the user (what they'll see, what it costs, what it rules out), in plain language. Always leave room for the user to answer in their own words.
4. **Batch as you see fit.** You decide how many questions go in each round. Related or independent questions can go together; dependent ones wait.
5. **Treat every answer as information.** If the user rejects all the options, questions the question, or answers with a question, reply briefly, then re-ask with better options or drop the question if it doesn't matter. If an answer reveals a general preference (say, "keep it simple"), apply it to the remaining decisions instead of asking about each one.
6. **Stop when you know enough**: when the open decisions left are ones the user wouldn't care about, or ones their answers already imply. Decide those yourself.

### How to ask

If your environment has a tool for asking multiple-choice questions (such as AskUserQuestion in Claude Code), use it. Otherwise, write the questions in chat with lettered options so the user can reply with something like "1A, 2C":

```
1. Where should the export button go?
   A. Toolbar, next to Share (recommended: people already look there)
   B. Inside the File menu
   C. Both
```

## Before starting the work

Show the decision list: one line per decision, including the ones you decided yourself (mark those "assumed"). Then wait for the user's go. Don't start the work or change anything until they confirm. If they change something, update the list and confirm again.

## Saving decisions

Save the decisions to a file only if the user asks, at any point in the session. Save where they say; if they don't say, use `decisions-<short-task-name>.md` in the working directory and tell them the path.

## After the work

When the task is done, list in chat the calls you made on your own: decisions that came up during the work and weren't covered in the grilling. Give one line each, with the alternative you didn't take. Leave out trivial ones (a loop variable's name) and include anything the user might plausibly have chosen differently. If there were none, say so.
