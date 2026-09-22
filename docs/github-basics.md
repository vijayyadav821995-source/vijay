# Git & GitHub for complete beginners

If you've never used these before, the single most confusing thing is that
**Git** and **GitHub** are two different things with similar names.

---

## 1. Git vs GitHub

**Git** is a program that runs on your computer. It takes snapshots of your
files as you work, so you can look at old versions, undo mistakes, and see
exactly what changed and when. Git works fine with no internet at all.

**GitHub** is a website that stores copies of Git projects online. It's where
you back up your work, share it with other people, and collaborate.

> Analogy: Git is like the "save history" feature. GitHub is like Google Drive
> where you keep a copy of that history so it's safe and shareable.

You use Git on your machine. You push to GitHub when you want the world (or a
backup) to have it.

---

## 2. The words you'll keep seeing

| Word | What it actually means |
|------|------------------------|
| **repository** ("repo") | A project folder that Git is tracking. This repo is called `vijay`. |
| **clone** | Download a copy of a GitHub repo onto your computer. |
| **commit** | A saved snapshot of your changes, with a message describing them. |
| **staging** | Choosing *which* changes go into the next commit (`git add`). |
| **push** | Upload your commits from your computer to GitHub. |
| **pull** | Download commits from GitHub onto your computer. |
| **branch** | A parallel line of work. Lets you try things without breaking the main version. |
| **main** | The name of the default/primary branch in most modern repos. |
| **merge** | Combine one branch's work into another. |
| **pull request** ("PR") | On GitHub: "please review my branch and merge it in." |
| **remote** | A nickname for a repo's online location. Yours is called `origin`. |
| **origin** | The default name for "the GitHub copy of this repo." |

---

## 3. The mental model: three places your work lives

```
   Working directory  ──git add──▶  Staging area  ──git commit──▶  Local history
   (the files you're                (the changes                   (snapshots on
    actually editing)                you've picked)                 your computer)
                                                                          │
                                                                     git push
                                                                          │
                                                                          ▼
                                                                    GitHub (origin)
```

And in reverse: `git pull` brings GitHub's commits down to your computer.

Almost every confusing Git moment comes down to: *which of these four places is
my change sitting in right now?* The answer is always `git status`.

---

## 4. Your first change, step by step

### One-time setup on your computer

Install Git (https://git-scm.com/downloads), then tell it who you are. This name
and email get stamped on every commit you make:

```bash
git config --global user.name "Vijay Yadav"
git config --global user.email "vijayyadav821995@gmail.com"
```

### Get the project onto your computer

```bash
git clone https://github.com/vijayyadav821995-source/vijay.git
cd vijay
```

`clone` downloads the whole project *and* its entire history, and remembers
where it came from.

### Make a change

Open any file in an editor, change something, save it. Then ask Git what it
noticed:

```bash
git status
```

It'll list your modified files in red — meaning "changed, but not staged yet."

### Stage, commit, push

```bash
git add README.md        # stage one file  (or: git add .  to stage everything)
git commit -m "Update the intro in the README"
git push
```

Refresh the repo page on GitHub. Your change is there. That's the whole loop —
you'll do `status → add → commit → push` thousands of times.

---

## 5. Writing good commit messages

A commit message explains *why* the change exists. Future-you will thank you.

```
Good:  Fix crash when the username field is empty
Good:  Add contact page with email form
Bad:   update
Bad:   asdf
Bad:   fixed stuff
```

Rule of thumb: finish the sentence "If applied, this commit will ___".

---

## 6. Branches — and why you want them

By default you're on `main`. If you edit `main` directly and break something,
the broken version is the official version.

Instead, make a branch. It's a free, instant, private copy of the project where
you can experiment:

```bash
git switch -c add-contact-page   # create a branch and move onto it
# ...make your changes, commit them...
git push -u origin add-contact-page
```

Then on GitHub you'll see a banner offering to open a **pull request**. A pull
request is a page where the change can be reviewed and discussed before it
becomes part of `main`. When you're happy, click **Merge**.

Moving between branches:

```bash
git branch          # list branches; * marks the one you're on
git switch main     # go back to main
git pull            # get main up to date after merging
```

---

## 7. `.gitignore` — the file that keeps you out of trouble

Some files should never go into Git:

- **Secrets** — passwords, API keys, `.env` files. Once pushed to a public repo,
  assume they're compromised forever. This is the #1 beginner mistake.
- **Generated files** — `node_modules/`, build output, compiled binaries. They're
  huge and can be recreated anytime.
- **OS junk** — `.DS_Store`, `Thumbs.db`.

The `.gitignore` file in this repo lists patterns for all of these. Anything
matching is invisible to Git.

---

## 8. When things go wrong

| Problem | Fix |
|---------|-----|
| "I have no idea what state I'm in" | `git status` — always safe, always first. |
| Undo changes to a file you haven't committed | `git restore <file>` |
| Unstage a file you `git add`ed by mistake | `git restore --staged <file>` |
| Fix the message on your last commit | `git commit --amend -m "Better message"` |
| See your history | `git log --oneline --graph --all` |
| See exactly what you changed | `git diff` |
| Push rejected — "updates were rejected" | Someone pushed first. Run `git pull`, resolve anything conflicting, then push again. |

**A merge conflict** means Git found two different edits to the same lines and
won't guess which you want. It marks the spot in the file like this:

```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> main
```

Delete the markers, leave the text you want, save, then `git add` the file and
`git commit`. That's all a conflict ever is.

---

## 9. What to do next

1. Clone this repo to your computer (section 4).
2. Edit `README.md` — add a line about yourself.
3. Commit and push it. Watch it appear on GitHub.
4. Then do it again on a branch, and open your first pull request.

Nothing here is permanent or breakable. Git's entire purpose is that you can
always get the old version back.
