# Git Debugging Exercise – Fixed Repository

**Author:** Muhammad Naveed  
**Date:** 09/03/2026  

---

## ✅ What Was Fixed

1. **Mixed commit split**  
   - Commit `2ee27fa ("quick fix")` contained unrelated changes.  
   - Split into 3 logical commits:
     - `README.md` updates → `docs: update README with features`
     - `config.txt` added → `feat: add configuration file`
     - `todo.txt` corrected → `fix: correct todo items`

2. **Incorrect content in `todo.txt`**  
   - Commit `4a0530f` added an unwanted line.  
   - Reverted using: `git revert 4a0530f`

3. **Secrets removed**  
   - Commit `f6cd227` contained hardcoded API_KEY.  
   - Replaced with placeholder `API_KEY=YOUR_API_KEY` in `secrets.txt`.  
   - In production, secrets should be removed from history using `git filter-repo` or stored in environment variables.

4. **Merge conflicts resolved**  
   - Merge between `main` and `feature/login` caused conflict in `notes.txt`.  
   - Conflict manually resolved, preserving both branches’ content.

5. **Branch sync via rebase**  
   - `feature/login` rebased onto latest `main`.  
   - Linear commit history maintained.

---

## 🛠 Commands Used (High-Level)

```bash
# Inspect history
git log --oneline --all --graph
git show <commit-hash>

# Split mixed commit
git rebase -i <commit>^
git reset HEAD^
git add <file>
git commit -m "<message>"
git rebase --continue

# Revert incorrect commit
git revert <commit-hash>

# Merge conflict resolution
git checkout main
git merge feature/login
# edit notes.txt, then:
git add notes.txt
git commit -m "merge: resolved notes.txt conflict from feature/login"

# Rebase feature branch
git checkout feature/login
git rebase main
git add <file>  # if conflicts
git rebase --continue

# Remove secret (manual replacement)
nano secrets.txt
git add secrets.txt
git commit -m "security: remove hardcoded API key"

# Push to remote
git push -u origin main
git push -u origin feature/login
