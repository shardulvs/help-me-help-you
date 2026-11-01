---
name: help-me-review
description: Review code together with the user instead of handing them a long report. First a fresh-eyes verdict on whether to fix or rewrite, then reverse grilling (pick-an-option questions about the decisions the code made), then quality fixes. Works the same for any code, whether the user's agent or a teammate wrote it. Only use this skill when the user explicitly invokes it by name; never start it on your own.
disable-model-invocation: true
---

# help-me-review

Turn a code review into a series of quick choices the user makes, instead of a report they have to read and answer.

## Why this works

A normal review produces a long list of findings that takes ages to read, and the user often can't tell what a good reply would be. But most of what matters in a review is decisions: the code already embodies choices someone made, and the real question is whether the user would have made the same ones. That's grilling in reverse: find those choices and let the user confirm or override each one. Code quality is handled separately, because the user isn't always the right judge of it, so there you make the call and they approve it.

## What to review

Use what the user pointed at: a PR, a branch, a diff, uncommitted changes, or specific files. If they didn't say, find the likely candidate (for example, uncommitted changes, or the current branch compared with its base) and confirm it with a quick question. The review works the same way whoever wrote the code.

## Step 1: Fix or rewrite?

Judge the code with fresh eyes. If you can hand this step to a subagent that hasn't seen this conversation, do so, because whoever wrote or discussed the code shares the blind spots that produced it.

Give one of three verdicts, backed by your three strongest reasons:

- **Fix**: the code is basically sound.
- **Rewrite part**: name the part. That part gets the rewrite path; the rest gets the fix path.
- **Rewrite**: fixing would cost more than starting over.

Don't give a numeric score; scores bunch up and don't answer the question that matters. Ask the user to accept your verdict or pick another.

## Step 2a: Rewrite

Don't review the details of code that's about to be thrown away. Instead, recover what it's supposed to do: list the decisions about its behavior (what it does, not how) and confirm them with the user as pick-an-option questions, since bad code often has the right intent. Then suggest running grill-me for the rewrite, starting from these confirmed decisions, and stop.

## Step 2b: Fix

1. **Reverse grill the decisions first.** Find the decisions the code makes that could reasonably have gone another way and that the user would plausibly care about. Start from any record of decisions you can find (a decisions file from grill-me, a list of calls an agent made on its own, the PR description), then look for decisions that aren't on it. For each one, say what the code does now and offer alternatives, with your recommendation first; "keep it as is" is often the right recommendation. Do this before any fixing, because changing a decision can change the code around it and throw away fixes made there.
2. **Then the quality problems.** Sort what's left:
   - **Clear-cut problems** (bugs, missing error handling, obvious mistakes): one line each with its location, as a single list the user can approve in one go or trim.
   - **Judgment calls** (tradeoffs where reasonable engineers would disagree): pick-an-option questions, recommended option first, with a one-line reason.

   Skip style nitpicks that a formatter or linter would handle, and put the problems that would cost the most if left alone first.

If there's nothing worth questioning and nothing to fix, say so and stop.

## Step 3: Finish

Ask whether to apply the agreed changes or write them up (for example, as review comments for the author), then do it. A write-up has one entry per change: where it is, what to change, and why, in a sentence or two.

## How to ask

Every question is pick-an-option: 2-4 options, your recommendation first and marked, and room for the user's own answer. You decide how many questions go in each round. If your environment has a tool for multiple-choice questions (such as AskUserQuestion in Claude Code), use it. Otherwise, write the questions in chat with lettered options so the user can reply with something like "1A, 2C".
