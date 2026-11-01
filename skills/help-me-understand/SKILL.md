---
name: help-me-understand
description: Help the user understand code, documentation, or any other material by quizzing them in small rounds and explaining only what they got wrong, instead of explaining everything up front. Only use this skill when the user explicitly invokes it by name; never start it on your own.
disable-model-invocation: true
---

# help-me-understand

Help the user understand something by quizzing them a little at a time and explaining only what they miss.

## Why this works

A full explanation wastes the user's attention: much of it covers things they already know or could guess, and the few points that matter get buried. A quiz finds out what they already know. When they get something wrong, you know both what they believed and what's actually true, so you can explain exactly that gap. Small rounds keep each explanation easy to digest.

## Setup

Work out what the material is (files, a function, a module, a doc, a URL, a concept) and read all of it before asking anything. If the scope is unclear, ask with options. Then split it into small chunks: big picture first (what it's for, its main parts), then the details that matter most.

## The loop

Repeat for each chunk:

1. **Quiz.** Ask about 3 multiple-choice questions on the chunk. Don't explain anything first; one line saying what the round covers is enough.
2. **Explain the misses.** For each wrong or "Not sure" answer, explain just that point: what's actually true, why, and where to see it (for code, the file and function or line). If a wrong answer shows a specific misconception, address it head-on ("B would be right if X, but here it's Y, because Z"). For correct answers, a word of confirmation is enough.
3. **Move on.** Go to the next chunk. Now and then, fold in a question about an earlier miss to check that it stuck.

Keep going until the material is covered or the user stops. If they ask something along the way, answer briefly and continue. When you finish, name in one line anything that's still shaky, if there is anything.

## Writing good questions

- Test understanding that matters: what happens when..., why does..., what would break if..., where does this value come from. Skip trivia like exact names or line numbers.
- Make the wrong options plausible misconceptions, so a wrong answer tells you something.
- Add a "Not sure" option to every question, because a lucky guess hides a gap.
- Vary where the correct answer sits, and don't reveal any answers until the user has answered the whole round.
- If a question hinges on a few specific lines, quote them in the question.
- It's fine to quiz before the user has read the material. Let them predict from names, structure, and what they already know; a wrong prediction marks exactly where the material is surprising.

## How to ask

If your environment has a tool for multiple-choice questions (such as AskUserQuestion in Claude Code), use it. Otherwise, write the round in chat with lettered options so the user can reply with something like "1B, 2 not sure, 3A".
