# Experiment 04 — Merge conflict resolution and rebase

**Student:** [Your name]  
**Register number:** [Your register number]  
**Course:** Collaborative Development and DevOps

## Aim

Create a merge conflict by editing the same line on two branches, resolve it, and compare merge and rebase history.

## Part A — Resolve a merge conflict

1. Create the baseline:
   ```sh
   mkdir conflict-rebase-lab
   cd conflict-rebase-lab
   git init
   git branch -M main
   printf "environment=development\n" > settings.txt
   git add settings.txt
   git commit -m "Add default environment"
   ```
2. Change the same line on a feature branch:
   ```sh
   git switch -c feature/production
   printf "environment=production\n" > settings.txt
   git commit -am "Set production environment"
   ```
3. Make a different change to that line on `main`, then attempt the merge:
   ```sh
   git switch main
   printf "environment=staging\n" > settings.txt
   git commit -am "Set staging environment"
   git merge feature/production
   ```
4. Open `settings.txt`. Choose the intended final value and remove every conflict marker (`<<<<<<<`, `=======`, `>>>>>>>`). Then complete the merge:
   ```sh
   git add settings.txt
   git commit -m "Resolve environment conflict"
   git status
   git log --oneline --graph --all
   ```

## Part B — Rebase a non-conflicting feature

1. Add a separate feature commit:
   ```sh
   git switch -c feature/logging
   printf "logging=enabled\n" > logging.txt
   git add logging.txt
   git commit -m "Add logging setting"
   ```
2. Advance `main`, then replay the feature commit on top of it:
   ```sh
   git switch main
   printf "timeout=30\n" > timeout.txt
   git add timeout.txt
   git commit -m "Add timeout setting"
   git switch feature/logging
   git rebase main
   git log --oneline --graph --all
   ```

## What to record

Show the conflict markers before resolution, the resolved file, and the final graph. Explain how rebase changes commit ancestry. Do not rebase a branch that other collaborators are already using.

## Result

Complete this section after performing the commands. Do not report output you did not observe.

## Reference and attribution

The topic follows the conflict-resolution and rebasing theme in [Smirk1308/DevOps_LAB_04](https://github.com/Smirk1308/DevOps_LAB_04). The sample files and procedure here are independently written.