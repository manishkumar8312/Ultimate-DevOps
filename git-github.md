# Git & GitHub Command Reference Guide

Git is a **distributed version control system** that enables developers to track changes in code, collaborate with teams, and manage project history efficiently.

Git is widely used in modern **software development, DevOps workflows, CI/CD pipelines, and open-source collaboration**.

This guide provides a **comprehensive reference of essential Git and GitHub commands**, organized by common workflows such as repository setup, file tracking, commits, branching, rebasing, and collaboration.

---

# Table of Contents

1. Initialization & Configuration
2. Working with Files
3. Commit Operations
4. Branching
5. Pushing & Pulling
6. Reset & Revert
7. Cleanup
8. GitHub CLI Commands
9. Rebase
10. Stash Commands
11. Tagging (Release Management)
12. Cherry Pick
13. Submodules
14. Inspect & Search
15. Additional Useful Commands
16. Best Practices
17. Additional Learning Resources

---

# 1. Initialization & Configuration

These commands help you **initialize repositories and configure Git identity**.

| Command                                    | Description                     |
| ------------------------------------------ | ------------------------------- |
| `git init`                                 | Initialize a new Git repository |
| `git clone <repo-url>`                     | Clone an existing repository    |
| `git config --global user.name "<name>"`   | Set global username             |
| `git config --global user.email "<email>"` | Set global email                |
| `git config --list`                        | View all configuration settings |

Example

```bash
git config --global user.name "Manish Kumar Sah"
git config --global user.email "your-email@example.com"
```

---

# 2. Working With Files

These commands manage **file tracking and staging area operations**.

| Command                       | Description                    |
| ----------------------------- | ------------------------------ |
| `git status`                  | Show file status               |
| `git add <file>`              | Add specific file to staging   |
| `git add .`                   | Add all files to staging       |
| `git reset <file>`            | Unstage a file                 |
| `git rm <file>`               | Remove file and stage deletion |
| `git restore <file>`          | Restore file from last commit  |
| `git restore --staged <file>` | Unstage changes                |
| `git mv <old> <new>`          | Rename or move file            |

---

# 3. Commit Operations

Commits capture a **snapshot of the project history**.

| Command                      | Description                    |
| ---------------------------- | ------------------------------ |
| `git commit -m "<message>"`  | Commit staged changes          |
| `git commit -am "<message>"` | Stage and commit tracked files |
| `git log`                    | View commit history            |
| `git log --oneline`          | Compact commit log             |
| `git show <commit>`          | Show detailed commit changes   |

Example

```bash
git add .
git commit -m "Add authentication module"
```

---

# 4. Branching

Branches allow **parallel development without affecting the main codebase**.

| Command                  | Description                    |
| ------------------------ | ------------------------------ |
| `git branch`             | List branches                  |
| `git branch <name>`      | Create a new branch            |
| `git checkout <branch>`  | Switch branch                  |
| `git checkout -b <name>` | Create and switch              |
| `git switch <branch>`    | Switch branch (modern command) |
| `git merge <branch>`     | Merge branch into current      |
| `git branch -d <branch>` | Delete branch                  |

Example

```bash
git checkout -b feature-login
```

---

# 5. Pushing & Pulling

These commands **synchronize local repositories with remote repositories**.

| Command                       | Description                   |
| ----------------------------- | ----------------------------- |
| `git remote -v`               | Show remote repository URLs   |
| `git remote add origin <url>` | Add remote repository         |
| `git push -u origin <branch>` | Push branch and set upstream  |
| `git push`                    | Push local commits            |
| `git pull`                    | Pull latest changes           |
| `git fetch`                   | Fetch updates without merging |
| `git push --force-with-lease` | Safe force push               |
| `git pull --ff-only`          | Fast-forward only pull        |

---

# 6. Reset & Revert

These commands help **undo changes or modify commit history**.

| Command                     | Description                          |
| --------------------------- | ------------------------------------ |
| `git reset --soft <commit>` | Reset HEAD but keep staged changes   |
| `git reset --hard <commit>` | Reset completely and discard changes |
| `git revert <commit>`       | Undo commit by creating a new commit |
| `git checkout <commit>`     | Checkout a specific commit           |
| `git checkout HEAD~1`       | Move to previous commit              |

---

# 7. Cleanup

Used to **remove untracked files and clean workspace**.

| Command            | Description                  |
| ------------------ | ---------------------------- |
| `git clean -n`     | Preview files to delete      |
| `git clean -f`     | Delete untracked files       |
| `git clean -fd`    | Delete files and directories |
| `git reset --hard` | Discard all local changes    |

---

# 8. GitHub CLI Commands

GitHub CLI allows interaction with GitHub **directly from the terminal**.

| Command            | Description                 |
| ------------------ | --------------------------- |
| `gh auth login`    | Authenticate GitHub account |
| `gh repo create`   | Create repository           |
| `gh issue list`    | View issues                 |
| `gh pr create`     | Create pull request         |
| `gh pr merge <id>` | Merge pull request          |

---

# 9. Rebase

Rebase rewrites commit history to create a **cleaner linear history**.

| Command                                           | Description                        |
| ------------------------------------------------- | ---------------------------------- |
| `git rebase <branch>`                             | Rebase onto another branch         |
| `git rebase --continue`                           | Continue after resolving conflicts |
| `git rebase --abort`                              | Abort rebase                       |
| `git rebase --skip`                               | Skip patch                         |
| `git rebase -i <commit>`                          | Interactive rebase                 |
| `git pull --rebase`                               | Pull using rebase                  |
| `git rebase --onto <newbase> <upstream> <branch>` | Advanced rebase                    |
| `git reflog`                                      | View reference history             |

---

# 10. Stash Commands

Used to **temporarily save uncommitted changes**.

| Command           | Description            |
| ----------------- | ---------------------- |
| `git stash`       | Save current changes   |
| `git stash list`  | Show stashes           |
| `git stash apply` | Apply stash            |
| `git stash pop`   | Apply and remove stash |
| `git stash drop`  | Delete stash           |

---

# 11. Tagging (Release Management)

Tags mark **release versions of the project**.

| Command                          | Description            |
| -------------------------------- | ---------------------- |
| `git tag`                        | List tags              |
| `git tag <tag>`                  | Create lightweight tag |
| `git tag -a <tag> -m "<msg>"`    | Annotated tag          |
| `git push origin <tag>`          | Push tag               |
| `git push --tags`                | Push all tags          |
| `git tag -d <tag>`               | Delete local tag       |
| `git push origin --delete <tag>` | Delete remote tag      |

---

# 12. Cherry Pick

Cherry-pick allows applying **specific commits from another branch**.

| Command                      | Description             |
| ---------------------------- | ----------------------- |
| `git cherry-pick <commit>`   | Apply specific commit   |
| `git cherry-pick --abort`    | Abort operation         |
| `git cherry-pick --continue` | Continue after conflict |

---

# 13. Submodules

Submodules allow including **external repositories inside your project**.

| Command                           | Description           |
| --------------------------------- | --------------------- |
| `git submodule add <repo> <path>` | Add submodule         |
| `git submodule update --init`     | Initialize submodules |
| `git submodule sync`              | Sync URLs             |

---

# 14. Inspect & Search

Useful for **analyzing repository history and code changes**.

| Command             | Description                    |
| ------------------- | ------------------------------ |
| `git blame <file>`  | Show line modification history |
| `git grep "<text>"` | Search text in repository      |
| `git shortlog -sn`  | Contributor commit count       |

---

# 15. Additional Useful Commands

```bash
git add -p           # Interactive staging
git diff             # Show unstaged changes
git diff --staged    # Show staged changes
git reflog           # View reference logs
git stash branch     # Create branch from stash
git bisect           # Find commit causing bug
```

---

# 16. Best Practices
```
✔ Write meaningful commit messages 
✔ Use feature branches for development
✔ Avoid force pushing to shared branches
✔ Use `.gitignore` for unnecessary files
✔ Pull frequently to avoid merge conflicts
✔ Prefer `git pull --rebase` for cleaner history
```
---

# 17. Additional Learning Resources

Official Documentation

* [https://git-scm.com/docs](https://git-scm.com/docs)
* [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

Interactive Learning

* [https://learngitbranching.js.org](https://learngitbranching.js.org)
* [https://ohmygit.org](https://ohmygit.org)

GitHub Learning Resources

* [https://docs.github.com](https://docs.github.com)
* [https://skills.github.com](https://skills.github.com)

Practice Platforms

* [https://www.codecademy.com/learn/learn-git](https://www.codecademy.com/learn/learn-git)
* [https://www.atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)
