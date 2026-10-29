---
name: commit-push
description: Commit and push changes in this repo. Use when the user asks to commit, push, or "commit push".
---

# Commit & push

1. `git status` to review changes (never commit secrets).
2. Commit message: **English, short** (one line, imperative, ~50-70 chars).
3. Always add Copilot as co-author, as the last trailer:

```bash
git commit -m "Short English message" -m "Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>"
```

4. Let the user do the git push alone. Don't do it. Just tell him that the repo is ready is pushù
