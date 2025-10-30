
# 🧠 GIT COMPLETE STUDY GUIDE (Interview + Practical Reference)

This README is a **comprehensive Git crash course** that covers **every concept, interview topic, and command** you need to **answer 90%+ Git questions confidently** — with short theory, examples, and tips.

---

## 🟩 1. Git Overview

### 🔹 What is Git?
Git is a **distributed version control system (DVCS)** used to track code changes and collaborate efficiently.

**Key Points:**
- Distributed (each clone has full history)
- Version history and rollback
- Branching and merging for collaboration

---

## 🟨 2. Git vs GitHub

| Feature | Git | GitHub |
|----------|-----|--------|
| Type | Version Control System | Hosting Service |
| Location | Local machine | Cloud |
| Example | `git commit` | Pull Request |

---

## 🟦 3. Git Core Commands

### Initialize a repo
```bash
git init
```

### Add & Commit
```bash
git add <file>        # Stage file
git commit -m "msg"   # Save snapshot
```

### Check Status & Logs
```bash
git status
git log --oneline
```

### Configure User Info
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

## 🟪 4. Branching & Merging

### Create and Switch Branch
```bash
git branch feature1
git switch feature1
```

### Merge Branch
```bash
git checkout main
git merge feature1
```

### Delete Branch
```bash
git branch -d feature1
```

### Visual Log
```bash
git log --oneline --graph --decorate
```

---

## 🟧 5. Undoing Changes

### Undo Last Commit (keep changes)
```bash
git reset --soft HEAD~1
```

### Undo Last Commit (discard changes)
```bash
git reset --hard HEAD~1
```

### Revert Specific Commit
```bash
git revert <commit_id>
```

### Remove a file but keep locally
```bash
git rm --cached filename
```

---

## 🟥 6. Remote Repositories

### Add Remote
```bash
git remote add origin <repo_url>
```

### Push / Pull Changes
```bash
git push -u origin main
git pull origin main
```

### View Remote URLs
```bash
git remote -v
```

---

## 🟩 7. Stashing Changes

### Temporarily Save Changes
```bash
git stash
git stash list
git stash pop
```

### Use Case:
When you want to switch branches without committing current work.

---

## 🟨 8. Cherry Pick & Rebase

### Cherry-pick a Commit
```bash
git cherry-pick <commit_hash>
```

### Rebase for Clean History
```bash
git checkout feature
git rebase main
```

### Merge vs Rebase
| Merge | Rebase |
|--------|--------|
| Preserves history | Linear history |
| Easier for teams | Cleaner for solo work |

---

## 🟦 9. Tags & Releases

### Create and Push a Tag
```bash
git tag v1.0
git push origin v1.0
```

### List Tags
```bash
git tag
```

---

## 🟪 10. Logs & Reflog

### View Commit History
```bash
git log --oneline --graph
```

### View All Operations (even deleted commits)
```bash
git reflog
```

**Use Case:** Recover lost commits after `reset --hard`.

---

## 🟧 11. Git Ignore

### Create `.gitignore`
```
*.log
__pycache__/
.env
```
Used to exclude unwanted files.

---

## 🟫 12. Collaboration (Pull Requests & Workflows)

### Pull & Fetch
```bash
git fetch origin
git merge origin/main
git pull origin main
```

### Common Branch Types (GitFlow)
- **main** – stable code
- **develop** – current dev work
- **feature/** – new features
- **release/** – pre-production
- **hotfix/** – urgent fixes

---

## 🟥 13. Conflicts & Resolution

### When Conflict Occurs:
Git marks conflict areas in files like:
```
<<<<<<< HEAD
Changes from current branch
=======
Changes from merging branch
>>>>>>> feature
```

### Resolve by:
1. Manually edit the file
2. Stage it: `git add file`
3. Commit it: `git commit`

---

## 🟩 14. Detached HEAD

Occurs when you checkout a commit instead of a branch.

**Fix:**
```bash
git checkout main
```

---

## 🟦 15. Common Daily Commands

```bash
git status
git add .
git commit -m "message"
git push
git pull
git branch
git checkout
git merge
```

---

## 🟧 16. Best Practices

✅ Commit small and meaningful changes  
✅ Pull before push  
✅ Use branches for features  
✅ Avoid committing secrets or `.env` files  
✅ Write descriptive commit messages  
✅ Rebase only on private branches  

---

## 🧩 17. Quick Recovery Commands

| Issue | Solution |
|-------|-----------|
| Lost commit | `git reflog` |
| Undo last commit | `git reset --soft HEAD~1` |
| Unstage file | `git restore --staged <file>` |
| Restore deleted file | `git checkout HEAD <file>` |

---

## 🧠 18. Top Interview Questions Summary

- What is Git? Difference between Git and GitHub?  
- Explain 3 areas in Git (Working Directory, Staging, Repo).  
- Difference between merge and rebase?  
- What is Git stash? Git cherry-pick?  
- What happens during `git reset --hard`?  
- How do you resolve merge conflicts?  
- Explain Git workflow with commands.  
- How do you tag a release?  
- How do you recover deleted commits?  
- Difference between `git fetch` and `git pull`?  

If you understand this document end-to-end and **practice a few commands** locally — you’ll be **interview-ready** for any Git-related question in DevOps, SRE, or developer interviews.

---

✅ **Tip for Interview Day:**
When asked about Git, **always explain your answers with small command examples** — it shows practical knowledge.

Example:
> _“To undo the last commit but keep changes, I’d use `git reset --soft HEAD~1`, which moves the HEAD pointer without discarding changes.”_

---

**Author:** Sohel Mohammed  
**Goal:** Master Git for DevOps interviews  
**Confidence:** 90%+ coverage of all Git core and advanced questions

---
