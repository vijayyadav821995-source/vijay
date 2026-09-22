# Git cheat sheet

Print this, or keep it open in a tab. These are ~95% of what you'll ever type.

## Every single day

```bash
git status                  # What's changed? Run this constantly.
git add <file>              # Stage one file for the next commit
git add .                   # Stage everything changed
git commit -m "message"     # Save a snapshot with a description
git push                    # Send commits up to GitHub
git pull                    # Bring GitHub's commits down
```

## Starting out

```bash
git clone <url>             # Copy a GitHub repo to your computer
git init                    # Turn an existing folder into a Git repo
git remote -v               # Show which GitHub repo this is linked to
```

## Branches

```bash
git branch                  # List branches (* = current)
git switch -c <name>        # Create a new branch and switch to it
git switch main             # Switch to an existing branch
git merge <name>            # Merge a branch into the current one
git branch -d <name>        # Delete a branch you're done with
git push -u origin <name>   # Push a new branch to GitHub the first time
```

## Looking around

```bash
git log --oneline           # Compact history
git log --oneline --graph --all   # History with branch structure
git diff                    # Changes you haven't staged
git diff --staged           # Changes you HAVE staged
git show <commit>           # What a specific commit changed
```

## Undoing things

```bash
git restore <file>              # Throw away uncommitted edits to a file
git restore --staged <file>     # Unstage a file (keeps your edits)
git commit --amend -m "msg"     # Reword / add to your last commit
git revert <commit>             # Make a NEW commit that undoes an old one (safe)
git reset --hard <commit>       # Rewind to a commit, DESTROYING later work (careful!)
```

> `revert` is safe and shareable. `reset --hard` deletes work permanently.
> When in doubt, use `revert`.

## Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list                        # See all current settings
```

## Two habits worth building

1. **`git status` before anything else.** It tells you where you are and usually
   suggests the exact command you need next.
2. **Commit small and often.** Ten small commits are far easier to understand —
   and to undo — than one enormous one.
