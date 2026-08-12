# [git commands I run before reading any code](https://piechowski.io/post/git-commands-before-reading-code/)

## What Changes the Most
```bash
git log --format=format: --name-only --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

I run this from `app/` or `src/`, not the repo root. Lockfiles, changelogs, and generated code will dominate the list otherwise.
## Who built this
```bash
git shortlog -sn --no-merges
```
Every contributor ranked by commit count.

___

