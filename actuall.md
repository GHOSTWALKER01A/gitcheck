# Git and GitHub Practice README

This file is a beginner-friendly practice guide for learning Git and GitHub step by step.

You can use it like a workbook:

* Read one command at a time
* Try it in your terminal
* Compare your output with the sample result
* Repeat until it feels natural

---

## 1. What Git and GitHub are

**Git** is a tool that tracks changes in your project.

**GitHub** is a website where you store Git projects online and collaborate with others.

Simple idea:

* Git = saves your work locally
* GitHub = shares your work online

---

## 2. Important Git terms

### Repository

A repository, or repo, is your project folder tracked by Git.

### Working directory

This is the normal folder where you edit files.

### Staging area

This is the place where you prepare changes before commit.

### Commit

A commit is a saved snapshot of your project.

### Branch

A branch is a separate line of work.

### Remote

A remote is a Git repository stored on another machine, usually GitHub.

### HEAD

HEAD points to the branch or commit you are currently on.

---

## 3. Before you start

Check whether Git is installed:

```bash
git --version
```

Sample result:

```bash
git version 2.45.1
```

Check your name and email setup:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

See current config:

```bash
git config --global --list
```

Sample result:

```bash
user.name=Your Name
user.email=your.email@example.com
```

---

## 4. Create a new practice repository

Make a folder and go inside it:

```bash
mkdir git-practice
cd git-practice
```

Initialize Git:

```bash
git init
```

Sample result:

```bash
Initialized empty Git repository in C:/.../git-practice/.git/
```

Check status:

```bash
git status
```

Sample result:

```bash
On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

---

## 5. Your first file, add, commit

Create a file called `README.md` with this content:

```md
# My Practice Repo
This is my first Git practice repository.
```

Check status again:

```bash
git status
```

Sample result:

```bash
Untracked files:
  README.md
```

Stage the file:

```bash
git add README.md
```

Check status:

```bash
git status
```

Sample result:

```bash
Changes to be committed:
  new file: README.md
```

Commit the file:

```bash
git commit -m "Add first README"
```

Sample result:

```bash
[main (root-commit) abc1234] Add first README
 1 file changed, 2 insertions(+)
 create mode 100644 README.md
```

See commit history:

```bash
git log --oneline
```

Sample result:

```bash
abc1234 Add first README
```

---

## 6. Edit a file and commit again

Edit `README.md` and add:

```md
## About
This repo is for Git practice.
```

Check changes:

```bash
git status
```

Sample result:

```bash
modified: README.md
```

See exactly what changed:

```bash
git diff
```

Sample result:

```diff
+## About
+This repo is for Git practice.
```

Stage and commit:

```bash
git add README.md
git commit -m "Update README"
```

Sample result:

```bash
[main def4567] Update README
 1 file changed, 2 insertions(+)
```

---

## 7. Useful status and history commands

### `git status`

Shows the current state of your repo.

```bash
git status
```

### `git log`

Shows full commit history.

```bash
git log
```

Sample result:

```bash
commit def4567
Author: Your Name <your.email@example.com>
Date:   ...

    Update README
```

### `git log --oneline`

Short commit history.

```bash
git log --oneline
```

Sample result:

```bash
def4567 Update README
abc1234 Add first README
```

### `git log --graph --oneline --decorate --all`

Shows branch structure visually in text.

```bash
git log --graph --oneline --decorate --all
```

Sample result:

```bash
* def4567 (HEAD -> main) Update README
* abc1234 Add first README
```

---

## 8. Branching practice

Create a new branch:

```bash
git branch feature-1
```

List branches:

```bash
git branch
```

Sample result:

```bash
* main
  feature-1
```

Switch to the branch:

```bash
git checkout feature-1
```

Sample result:

```bash
Switched to branch 'feature-1'
```

You can also use:

```bash
git switch feature-1
```

Create and switch in one command:

```bash
git checkout -b feature-2
```

Sample result:

```bash
Switched to a new branch 'feature-2'
```

Modern version:

```bash
git switch -c feature-2
```

---

## 9. Branch workflow practice

Suppose you are on `feature-2` and make a change to `README.md`.

Then:

```bash
git add README.md
git commit -m "Work on feature 2"
```

Sample result:

```bash
[feature-2 778899a] Work on feature 2
 1 file changed, 1 insertion(+)
```

Now go back to `main`:

```bash
git switch main
```

Your `main` branch will not contain the feature commit yet.

Merge the feature branch into main:

```bash
git merge feature-2
```

Sample result for a fast-forward merge:

```bash
Updating def4567..778899a
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

If Git cannot fast-forward, it may create a merge commit.

Sample merge commit result:

```bash
Merge made by the 'ort' strategy.
 README.md | 1 +
```

---

## 10. Merge conflict practice

A merge conflict happens when both branches change the same lines in the same file.

Example conflict markers:

```text
<<<<<<< HEAD
My change from main
=======
Their change from feature
>>>>>>> feature-branch
```

### How to solve it

1. Open the file
2. Decide which text to keep
3. Remove the conflict markers
4. Save the file
5. Stage it
6. Commit it

Commands:

```bash
git status
git add README.md
git commit -m "Resolve merge conflict"
```

Sample result:

```bash
[main 99aa11b] Resolve merge conflict
```

---

## 11. Pull from GitHub

First connect a remote repository.

Add remote:

```bash
git remote add origin https://github.com/your-username/git-practice.git
```

Check remotes:

```bash
git remote -v
```

Sample result:

```bash
origin  https://github.com/your-username/git-practice.git (fetch)
origin  https://github.com/your-username/git-practice.git (push)
```

Push your branch:

```bash
git push -u origin main
```

Sample result:

```bash
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

Get remote changes:

```bash
git pull origin main
```

This is the same as:

* fetch remote changes
* merge them into your current branch

If you are behind and have local changes, Git may stop and say the files would be overwritten.

---

## 12. Fetch only

Fetch gets changes from remote but does not merge them.

```bash
git fetch origin
```

Sample result:

```bash
From https://github.com/your-username/git-practice.git
 * [new branch]      main -> origin/main
```

Use this when you want to inspect remote updates first.

---

## 13. Rebase practice

Rebase moves your commits on top of another branch.

Example:

```bash
git switch feature-branch
git rebase main
```

Sample result:

```bash
Successfully rebased and updated refs/heads/feature-branch.
```

### Important rule

Do not rebase a branch that many people already use, because it rewrites history.

---

## 14. Interactive rebase practice

Interactive rebase lets you clean up commits.

```bash
git rebase -i HEAD~3
```

This opens an editor where you may see:

```bash
pick a1b2c3d Add login page
pick b2c3d4e Fix typo
pick c3d4e5f Update style
```

You can change one of them to:

```bash
squash b2c3d4e Fix typo
```

This combines commits into one.

After saving, Git may ask you to edit the commit message.

Sample result:

```bash
Successfully rebased and updated refs/heads/feature-branch.
```

---

## 15. Stash practice

Stash saves unfinished work temporarily.

```bash
git stash
```

Sample result:

```bash
Saved working directory and index state WIP on main: abc1234 Add first README
```

See saved stashes:

```bash
git stash list
```

Sample result:

```bash
stash@{0}: WIP on main: abc1234 Add first README
```

Apply back the latest stash:

```bash
git stash pop
```

Sample result:

```bash
Dropped refs/stash@{0}
```

Use `git stash apply` if you want to keep the stash after applying.

---

## 16. Undo practice

### Undo staged files but keep file changes

```bash
git restore --staged README.md
```

Sample result:

```bash
(no output)
```

### Undo changes in working directory

```bash
git restore README.md
```

Sample result:

```bash
(no output)
```

### Undo the last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

### Undo the last commit and unstage changes

```bash
git reset --mixed HEAD~1
```

### Delete the last commit and discard changes

```bash
git reset --hard HEAD~1
```

Be careful with `--hard` because it can remove work permanently from your branch view.

---

## 17. Cherry-pick practice

Cherry-pick copies one commit from another branch.

```bash
git cherry-pick abc1234
```

Sample result:

```bash
[main 55dd66e] Add first README
```

Use this when only one commit is needed from another branch.

---

## 18. Revert practice

Revert makes a new commit that cancels an old commit.

```bash
git revert abc1234
```

Sample result:

```bash
[main 77ee88f] Revert "Add first README"
```

This is safer than reset on shared branches because it keeps history.

---

## 19. Detach HEAD practice

Checkout a commit directly:

```bash
git checkout abc1234
```

Sample result:

```bash
HEAD is now at abc1234 Add first README
```

This is called detached HEAD.

To continue working from there, create a branch:

```bash
git switch -c fix-from-old-commit
```

---

## 20. Useful inspection commands

Show changed files:

```bash
git diff --name-only
```

Show staged changes only:

```bash
git diff --staged
```

Show last commit details:

```bash
git show
```

Show a compact summary of branches:

```bash
git branch -vv
```

Sample result:

```bash
* main       def4567 [origin/main] Update README
  feature-1  778899a Work on feature 2
```

---

## 21. Common problems and what they mean

### Problem: "Your local changes would be overwritten by merge"

You changed a file locally, and Git refuses to overwrite it.

Fix:

* commit your work
* or stash it
* or restore it if you do not need it

### Problem: "Merge conflict"

Both branches changed the same part of a file.

Fix:

* edit the file manually
* remove conflict markers
* add and commit

### Problem: "non-fast-forward"

Your branch is behind the remote branch.

Fix:

* pull first
* or rebase first
* then push again

### Problem: "detached HEAD"

You checked out a commit instead of a branch.

Fix:

* create a branch from that commit

---

## 22. Beginner practice flow

Use this exact order for practice:

```bash
git init
git status
git add .
git commit -m "first commit"
git branch feature-1
git switch feature-1
git add .
git commit -m "work on feature-1"
git switch main
git merge feature-1
git log --oneline --graph --decorate --all
```

Expected learning result:

* you understand repo creation
* you understand staging and commit
* you understand branching
* you understand merging
* you understand history visualization

---

## 23. Practice with GitHub

After creating a repo on GitHub:

```bash
git remote add origin https://github.com/your-username/your-repo.git
git push -u origin main
```

Then use feature branches:

```bash
git switch -c feature/login
git add .
git commit -m "Add login feature"
git push -u origin feature/login
```

On GitHub:

* open a Pull Request
* review changes
* merge when approved

---

## 24. Rule for professional work

Always try to keep your work organized like this:

* one branch = one task
* one PR = one logical change
* small commits are better than huge commits
qwsfigsiuius8fuyaufsf yuwgugsy bytd cygalknposi-9


---

## 25. Command cheat sheet

```bash
git init
git status
git add .
git commit -m "message"
git log --oneline
git branch
git switch branch-name
git checkout -b new-branch
git merge branch-name
git rebase main
git stash
git stash pop
git fetch origin
git pull origin main
git push origin main
git diff
git restore file.txt
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git cherry-pick <commit-hash>
git revert <commit-hash>
```

---

## 26. Final note for practice

Do not try to memorize everything at once.

Learn in this order:

1. status
2. add
3. commit
4. branch
5. merge
6. pull and push
7. stash
8. rebase
9. conflict resolution
10. revert, reset, cherry-pick

That order will make Git much easier to understand.

---

## 27. Mini exercises

### Exercise 1

Create a file, stage it, commit it.

### Exercise 2

Create a branch, make one change, merge it back.

### Exercise 3

Make a change, stash it, pull new changes, then pop the stash.

### Exercise 4

Make two branches change the same line and resolve the conflict.

### Exercise 5

Create three commits and practice `git rebase -i`.

---

## 28. Words to remember

* Git tracks history
* branch = pointer
* commit = snapshot
* staging = preparing changes
* merge = combine histories
* rebase = rewrite on top
* stash = temporary save
* revert = safe undo
* reset = move branch pointer

---

## 29. Sample learning goal

After practicing this file, you should be able to:

* create and edit repositories
* work with branches
* push and pull from GitHub
* solve simple merge conflicts
* use rebase safely
* understand when to stash, revert, or reset

---

## 30. Your next best practice

Practice in a separate test repository first, never directly inside an important project.
