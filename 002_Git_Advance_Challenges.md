# Advanced Git Challenges - Questions and Answers

## 1. Rewrite Commit History

**Question:** Use git rebase -i to squash the last three commits into one with a custom commit message.

**Answer:**

```bash
touch file1.txt
echo "First commit content" >> file1.txt
git add file1.txt
git commit -m "First commit"

echo "Second commit content" >> file1.txt
git add file1.txt
git commit -m "Second commit"

echo "Third commit content" >> file1.txt
git add file1.txt
git commit -m "Third commit"

git rebase -i HEAD~3
# Write new commit message
```

## 2. Recover from a Detached HEAD

**Question:** Checkout an earlier commit, make a change, then create a new branch from that state to save the work.

**Answer:**

```bash
git checkout HEAD~2
touch detached-work.txt
echo "Work done in detached HEAD" >> detached-work.txt
git add detached-work.txt
git commit -m "Work in detached HEAD"
git checkout -b recovery-branch
```

## 3. Stash Changes and Switch Branches

**Question:** Modify files, stash the changes, switch to another branch, and reapply the stash. Bonus: Explain the difference between git stash apply and git stash pop.

**Answer:**

```bash
echo "Unfinished work" >> README.md
git stash push -m "Work in progress"
git checkout feature-x
git checkout main
git stash pop

# git stash pop - applies and removes from stash list
# git stash apply - applies but keeps in stash list
```

## 4. Resolve Merge Conflicts Manually

**Question:** Cause a conflict by editing the same line in two branches. Merge them and resolve the conflict in a text editor. Bonus: Commit with a message indicating the manual resolution.

**Answer:**

```bash
touch conflict-file.txt
echo "Original line" >> conflict-file.txt
git add conflict-file.txt
git commit -m "Add original file"

git checkout -b conflict-branch
echo "Modified in branch" > conflict-file.txt
git add conflict-file.txt
git commit -m "Modify in branch"

git checkout main
echo "Modified in main" > conflict-file.txt
git add conflict-file.txt
git commit -m "Modify in main"

git merge conflict-branch
echo "Resolved: Combined both changes" > conflict-file.txt
git add conflict-file.txt
git commit -m "Resolve merge conflict: manually combined changes"
```

## 5. Bisect a Bug

**Question:** Use git bisect to find the first commit that introduced a bug, assuming you know one commit that worked and one that didn't.

**Answer:**

```bash
git bisect start
git bisect bad
git bisect good HEAD~3
git bisect good
git bisect reset
```

## 6. Submodules

**Question:** Add another Git repository as a submodule, make a change in it, and commit updates in the main repository.

**Answer:**

```bash
git submodule add https://github.com/username/external-repo.git modules/external
cd modules/external
touch new-feature.txt
git add new-feature.txt
git commit -m "Add feature to submodule"
cd ../..
git add modules/external
git commit -m "Update submodule reference"
```

## 7. Clean Up with Reflog

**Question:** Accidentally delete a branch with unpushed commits, and use git reflog to recover it.

**Answer:**

```bash
git checkout -b important-work
touch important.txt
git add important.txt
git commit -m "Critical changes"
git checkout main
git branch -D important-work
git reflog
git checkout -b recovered-work <commit-hash>
```

## 8. Filter History to Remove Sensitive Data

**Question:** Use git filter-repo to completely remove a committed file (like .env) from the entire Git history.

**Answer:**

```bash
touch .env
echo "SECRET_KEY=sensitive_data" >> .env
git add .env
git commit -m "Add environment file"
git filter-repo --path .env --invert-paths
```

## 9. Cherry-pick a Commit

**Question:** Select and apply a specific commit from one branch to another using git cherry-pick.

**Answer:**

```bash
git checkout -b source-branch
touch cherry-feature.txt
echo "Specific feature" >> cherry-feature.txt
git add cherry-feature.txt
git commit -m "Feature to cherry-pick"
git checkout main
git cherry-pick <commit-hash>
```

## 10. Set Up a Git Hook

**Question:** Create a pre-commit hook that prevents committing .log files into the repository.

**Answer:**

```bash
touch .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
cat << 'EOF' > .git/hooks/pre-commit
#!/bin/bash
if git diff --cached --name-only | grep -q '\.log$'; then
    echo "Error: .log files cannot be committed"
    exit 1
fi
EOF
```

## 11. Merge with Custom Strategy

**Question:** Perform a merge using a custom strategy, such as --strategy=recursive -X theirs, to resolve automatic conflicts.

**Answer:**

```bash
touch strategy-file.txt
echo "original content" >> strategy-file.txt
git add strategy-file.txt
git commit -m "Original content"

git checkout -b their-branch
echo "their changes" > strategy-file.txt
git add strategy-file.txt
git commit -m "Their changes"

git checkout main
echo "our changes" > strategy-file.txt
git add strategy-file.txt
git commit -m "Our changes"

git merge their-branch --strategy=recursive -X theirs
```

## 12. Use Git Worktree for Multi-Branch Development

**Question:** Create a separate working directory using git worktree to work on another branch simultaneously without switching in the main directory.

**Answer:**

```bash
git worktree add ../feature-worktree feature-x
cd ../feature-worktree
touch worktree-feature.txt
echo "Worktree development" >> worktree-feature.txt
git add worktree-feature.txt
git commit -m "Work from worktree"
cd ../my-git-project
git worktree remove ../feature-worktree
```
