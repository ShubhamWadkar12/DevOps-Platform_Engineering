# Git & GitHub

## Overview

Git is a **Version Control System (VCS)** used to track changes in code, while GitHub is a cloud platform used to host Git repositories and collaborate with others.

---

# Why Git & GitHub?

- Track code changes
- Collaborate with teams
- Manage project versions
- Backup code online
- Contribute to open-source projects

---

# Git vs GitHub

| Git | GitHub |
|-----|---------|
| Version Control System | Cloud hosting platform |
| Works locally | Works online |
| Tracks changes | Stores and shares repositories |

---

# Basic Git Commands

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

git init
git clone <repository-url>

git status
git add .
git commit -m "Initial commit"

git push
git pull

git branch
git checkout
git merge
```

---

# Best Practices

- Write meaningful commit messages.
- Commit changes regularly.
- Use branches for new features.
- Push code frequently to GitHub.
- Never commit passwords or secret keys.

---

# Interview Questions

**Q: What is Git?**  
**A:** Git is a distributed version control system used to track changes in code.

**Q: What is GitHub?**  
**A:** GitHub is a cloud platform that hosts Git repositories for collaboration and code management.

**Q: Difference between Git and GitHub?**  
**A:** Git is a version control tool, while GitHub is an online platform for hosting Git repositories.

**Q: What is a repository?**  
**A:** A repository (repo) is a storage location that contains your project files and their version history.

**Q: What is a commit?**  
**A:** A commit is a saved snapshot of changes made to a Git repository.

**Q: Difference between `git fetch` and `git pull`?**  
**A:** `git fetch` downloads changes without merging, while `git pull` downloads and merges them into your current branch.
```
Suppose your friend pushed new code to GitHub.

git fetch -> Downloads your friend's changes; Your project stays exactly the same; You can review the changes first.

git pull -> Downloads your friend's changes; Immediately updates your current branch with those changes.
```

**Q: Why do we use branches?**  
**A:** Branches allow developers to work on new features or fixes without affecting the main code.

