---
name: Gitee Commit Push
description: Commit all changes and push to Gitee repository (https://gitee.com/whalefox/yl2). Use when the user asks to submit, commit, or push the project.
---

# Gitee Commit Push

Commit all changes and push the current project to the Gitee repository.

## Workflow

1. Check the current git status and remote configuration.
2. If no remote is configured, add the Gitee remote:
   ```
   git remote add origin https://gitee.com/whalefox/yl2.git
   ```
3. Stage all files:
   ```
   git add -A
   ```
4. Commit with a descriptive message:
   ```
   git commit -m "更新：提交项目文件"
   ```
5. Push to the remote repository:
   ```
   git push -u origin master
   ```
   If the remote uses `main` as the default branch, use:
   ```
   git push -u origin main
   ```

## Notes

- If the push fails due to non-fast-forward, pull first with `git pull --rebase origin master` (or `main`), resolve any conflicts, then push again.
- If authentication fails, inform the user to configure their Gitee credentials.
- Use the current date or a brief summary of changes in the commit message when the user provides context.
