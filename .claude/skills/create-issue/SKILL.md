---
name: create-issue
description: Create a GitHub issue in this repo. Use whenever the user asks to add, file, log or create an issue, bug or feature request.
---

# Create an issue

Repo: `Digital-Tijori/digital-tijori-releases`. Issues are public. Write the title and body from the user's words, and do not invent details.

## Check for duplicates first

Before creating, list the open issues and compare by meaning, not exact wording:

```sh
gh issue list --state open --limit 100 --json number,title,body
```

If an open issue already covers it, do not create a new one. Tell the user the issue number and URL, and ask whether to add the new detail as a comment on it (`gh issue comment <n> --body "..."`) or to create a separate issue anyway.

## Use issue types, not labels

Never pass `--label`. Never add `bug` or `enhancement` labels. Kind of issue is an issue **type**, set at the org level:

| Type | Use for |
|------|---------|
| `Bug` | Something works wrongly or broke |
| `Feature` | New or improved behavior (replaces the old `enhancement` label) |
| `Task` | Chore, setup, docs, cleanup with no user-facing behavior change |

`gh issue create` cannot set a type. Create the issue, then set the type with the API:

```sh
url=$(gh issue create --title "<title>" --body "<body>")
gh api -X PATCH "repos/Digital-Tijori/digital-tijori-releases/issues/${url##*/}" -f type=Bug   # or Feature / Task
```

Do not write `Type: feature` in the body. The type field carries it.

To fix an existing issue: `gh issue edit <n> --remove-label <label>`, then the same PATCH.

## Title

One line, plain words, says the problem or the outcome. No `[Bug]` or `feat:` prefix.

## Body template

Bug:

```md
## Problem
What goes wrong, and for whom.

## Expected
What should happen.

## Actual
What happens now. Add steps to reproduce, app version and OS if the user gave them.
```

Feature:

```md
## Problem
What the user cannot do or finds hard today.

## Proposal
What the app should do instead.

## Expected
The visible result when it works.
```

Task:

```md
## What
The work to do.

## Why
The reason it is needed.
```

Leave out a section if the user gave nothing for it. Do not fill it with guesses.

## After

Report the issue URL and the type set.
