## [Git Commands I Run Before Reading Any Code](https://piechowski.io/post/git-commands-before-reading-code/)

### What Changes the Most
```bash
git log --format=format: --name-only --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```

I run this from `app/` or `src/`, not the repo root. Lockfiles, changelogs, and generated code will dominate the list otherwise.
## Who built this
```bash
git shortlog -sn --no-merges
```
Every contributor ranked by commit count.

# Where do bugs cluster?
```bash
git log -i -E --grep="fix|bug|broken" --name-only --format='' | sort | uniq -c | sort -nr | head -20
```

# Is This Project Accelerating or Dying?
```bash
git log --format='%ad' --date=format:'%Y-%m' | sort | uniq -c
```

## How Often Is the Team Firefighting
```bash
git log --oneline --since="1 year ago" | grep -iE 'revert|hotfix|emergency|rollback'
```

## [What Good Requirements Look like](https://projan.ai/blog/what-good-requirements-look-like-and-how-to-write-them)

- **Unambiguous.** Two people reading it separately build the same thing.
- **Testable.** You can describe how you would demonstrate it is met.
- **Necessary.** Delete it and something a user or the business needs stops working.
- **Feasible.** It can be built inside the constraints you have, not the ones you wish you had.
- **Complete.** It does not rely on a fact that exists only in someone’s head.
- **Consistent.** It does not contradict another requirement in the same document.
- **Traceable.** Six months later you can say who asked for it and why.

### Examples
| <center>Weak version</center>                         | <center>What goes wrong </center>                                       | <center>Stronger version</center>                                                                                                                        |
| ----------------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Users can export and email reports.                   | Two obligations in one line, so half can fail while the line is ticked. | Split it. “A user can export a report as CSV.” and “A user can email an exported report to any address in their own organisation.”                       |
| Reports must be approved before publication.          | No actor, so at build time somebody picks one.                          | A finance manager must approve a report before it can be published.                                                                                      |
| The system supports relevant file types.              | Unbounded set, so the reader decides what relevant means.               | Uploads accept PDF, PNG and JPEG files up to 10 MB. Anything else is rejected with a message naming the accepted types.                                  |
| A confirmation email is sent when an order is placed. | Silent on failure, so the failure path gets invented under pressure.    | A confirmation email is sent within 60 seconds of an order being placed. If the send fails, the order remains valid and the failure is queued for retry. |
| Admins can manage users.                              | ”Manage” hides five behaviours with different permissions.              | An admin can create, deactivate and reset the password of any user in their own organisation. Admins cannot delete users.                                |
