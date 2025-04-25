# Git Basics for DevOps

## What is Git?

Git is a distributed version control system that tracks changes in source code. It enables multiple developers and automation systems to collaborate efficiently on infrastructure-as-code and other DevOps-related projects.

---

## Key Concepts

### Repository (Repo)

A Git repository is a directory that contains your project and the entire history of its changes.

### Init

Initializes a new Git repository in the current directory.

```bash
git init
```

You can also set a remote origin, including a local path:

```bash
git remote add origin /path/to/local/repo
```

### Clone

Creates a copy of a remote repository to your local machine.

```bash
git clone https://github.com/user/repo.git
```

### Commit

Records changes to the repository.

```bash
git add .
git commit -m "Your message"
```

### Push

Sends your commits to a remote repository.

```bash
git push origin main
```

### Pull

Fetches and merges changes from the remote repository to your local branch.

```bash
git pull origin main
```

### Branch

Allows parallel development by creating isolated lines of development.

```bash
git branch feature-branch
git checkout feature-branch
```

### Merge

Combines changes from one branch into another.

```bash
git checkout main
git merge feature-branch
```

### Rebase (optional)

Reapplies commits on top of another base tip, often used to keep history clean.

```bash
git checkout feature-branch
git rebase main
```

### Status

Shows the state of the working directory and staging area.

```bash
git status
```

### Log

Displays commit history.

```bash
git log --oneline
```

---

## Common Workflows in DevOps

### Infrastructure-as-Code (IaC)

Use Git to version Terraform, Ansible, Kubernetes manifests, etc.

### CI/CD Integration

Use Git webhooks to trigger builds/deployments in CI/CD pipelines.

### GitOps

Declarative infrastructure management using Git as a single source of truth.

---

## Tips

- Use `.gitignore` to exclude files from version control.
    
- Use meaningful commit messages.
    
- Use Pull Requests (PRs) for code reviews and automated testing.
    
- Tag releases using `git tag`.
    

---

## Git Config Example

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## Resources

- [Pro Git Book](https://git-scm.com/book/)
    
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
    
- [GitHub Docs](https://docs.github.com/en/get-started/quickstart)