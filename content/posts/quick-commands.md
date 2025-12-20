---
title: "quick commands"
date: 2025-12-20T09:00:00+05:30
draft: false
---

here is a list of quick commands that can come in handy.

## initialize and push a local repo

command:
```bash
mkdir DentRAG && cd DentRAG && git init && git branch -M main && gh repo create DentRAG --public --source=. --remote=origin
```

breakdown:
- `mkdir DentRAG`: create a new directory named DentRAG.
- `cd DentRAG`: move into the new directory.
- `git init`: initialize a new git repository.
- `git branch -M main`: rename the current branch to main.
- `gh repo create DentRAG --public --source=. --remote=origin`: create a public repository on github from the current directory and set the remote.

## open a file in antigravity in the same window

command:
```bash
antigravity -r .
```
