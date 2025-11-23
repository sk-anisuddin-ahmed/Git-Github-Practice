# Git Exercises - Questions and Answers

## 1. Initialize and Track a Project

**Question:** Create a new directory, initialize a Git repository, and track a new file (README.md). Bonus: Commit the file with the message "Add project description".

**Answer:**

```bash
mkdir my-git-project
cd my-git-project
git init
touch README.md
echo "# My Git Project" >> README.md
git add README.md
git commit -m "Add project description"
```

## 2. Check Status and Log

**Question:** Modify a tracked file and use Git commands to check: What is staged, What is modified, The commit history with hashes and messages.

**Answer:**

```bash
echo "This project demonstrates Git basics." >> README.md
git status
git add README.md
git status
git log --oneline
```

## 3. Undo Mistakes

**Question:** Add a file and commit it. Then modify its content and use Git to undo the last commit while preserving changes in the working directory.

**Answer:**

```bash
touch mistake.txt
echo "Initial content" >> mistake.txt
git add mistake.txt
git commit -m "Add mistake file"
echo "Modified content" >> mistake.txt
git reset --soft HEAD~1
```

## 4. Branch and Merge

**Question:** Create a new branch feature-x, make a change, commit it, and merge it into main. Bonus: Visualize the branch history using git log --graph.

**Answer:**

```bash
git checkout -b feature-x
touch feature.txt
echo "Feature X implementation" >> feature.txt
git add feature.txt
git commit -m "Implement feature X"
git checkout main
git merge feature-x
git log --graph --oneline --all
```

## 5. Push to GitHub

**Question:** Connect your local repo to a GitHub remote and push your branch. Bonus: Clone the repository from another machine or folder to verify.

**Answer:**

```bash
git remote add origin https://github.com/username/repository-name.git
git push -u origin main
cd ..
git clone https://github.com/username/repository-name.git
```

## 6. Ignore Files

**Question:** Create a .gitignore file that ignores *.log files and the node_modules/ directory. Bonus: Confirm the ignored files don't appear in git status.

**Answer:**

```bash
touch .gitignore
echo "*.log" >> .gitignore
echo ".vscode/" >> .gitignore
git add .gitignore
git commit -m "Add .gitignore file"
mkdir .vscode
touch app.log
git status
```

## 7. View and Revert Changes

**Question:** Make a change, use git diff to view it, and then revert it back to the last committed state.

**Answer:**

```bash
echo "Unwanted change" >> README.md
git diff
git checkout -- README.md
```

## 8. Tag a Release

**Question:** Tag a specific commit as v1.0. Bonus: Push the tag to the remote repository.

**Answer:**

```bash
git tag -a v1.0 -m "Release version 1.0"
git push origin v1.0
git tag -l
```
