# Git Branch Workflow Workout

Welcome to the Git Branch Workflow Workout! This guide will help you understand and practice working with main and development branches.

## Table of Contents
- [Understanding Branches](#understanding-branches)
- [Main vs Development Branches](#main-vs-development-branches)
- [Branch Workflow](#branch-workflow)
- [Hands-on Exercises](#hands-on-exercises)
- [Best Practices](#best-practices)

## Understanding Branches

### What are Git Branches?

Branches in Git are like parallel universes for your code. They allow you to:
- Work on new features without affecting the main codebase
- Experiment with ideas safely
- Collaborate with others without conflicts
- Maintain different versions of your code

### Visualizing Branches

```
main:     A---B---C---D
                   \
development:        E---F---G
                         \
feature:                  H---I
```

## Main vs Development Branches

### Main Branch (formerly master)

The **main** branch is typically:
- The **stable** production-ready code
- The source for deployments to production
- Protected from direct commits
- Updated through pull requests and reviews
- Always in a working state

**Key Points:**
- 🛡️ Protected and stable
- 🚀 Ready for deployment
- ✅ Thoroughly tested
- 📝 Documented changes

### Development Branch

The **development** branch is typically:
- The **integration** branch for features
- More active than main
- Where feature branches are merged first
- Used for testing before merging to main
- May contain work-in-progress code

**Key Points:**
- 🔄 Active development
- 🧪 Testing ground
- 🔗 Integration point
- 🚧 May be unstable

## Branch Workflow

### Basic Gitflow Model

```
main (production)
  ↑
  | merge when stable
  |
development (integration)
  ↑
  | merge when complete
  |
feature branches (individual work)
```

### Step-by-Step Workflow

#### 1. Start with an Updated Repository

```bash
# Clone the repository
git clone <repository-url>
cd <repository-name>

# Check current branch
git branch

# See all branches (including remote)
git branch -a
```

#### 2. Create a Feature Branch from Development

```bash
# Switch to development branch
git checkout development

# Pull latest changes
git pull origin development

# Create and switch to a new feature branch
git checkout -b feature/my-new-feature
```

#### 3. Make Changes and Commit

```bash
# Make your changes to files

# Check status
git status

# Stage changes
git add .

# Commit with a descriptive message
git commit -m "Add new feature: description"
```

#### 4. Push Your Feature Branch

```bash
# Push feature branch to remote
git push origin feature/my-new-feature
```

#### 5. Create a Pull Request

- Go to your repository on GitHub
- Click "Compare & pull request"
- Set base branch to `development`
- Write a clear description
- Request reviews if needed
- Submit the pull request

#### 6. Merge to Development

After review and approval:
- Merge the pull request to development
- Delete the feature branch (optional but recommended)

#### 7. Test in Development

```bash
# Switch to development
git checkout development

# Pull the merged changes
git pull origin development

# Run tests
# Deploy to staging environment (if applicable)
```

#### 8. Merge to Main (Release)

When development is stable and ready:
- Create a pull request from `development` to `main`
- Get thorough review
- Run all tests
- Merge to main
- Tag the release (optional)

```bash
git checkout main
git pull origin main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

## Hands-on Exercises

### Exercise 1: Branch Exploration

Practice checking branches in this repository:

```bash
# List all local branches
git branch

# List all branches (local and remote)
git branch -a

# View current branch
git status

# View branch history
git log --oneline --graph --all
```

**Questions to Answer:**
1. What is your current branch?
2. How many branches exist in this repository?
3. What's the latest commit on the main branch?

---

### Exercise 2: Create a Personal Feature Branch

```bash
# Make sure you're on development
git checkout development
git pull origin development

# Create your feature branch
git checkout -b feature/your-name-practice

# Make a change (create a file with your name)
echo "# My Practice File - [Your Name]" > my-practice.md

# Add and commit
git add my-practice.md
git commit -m "Add practice file"

# Push your branch
git push origin feature/your-name-practice
```

---

### Exercise 3: Understanding Branch Differences

```bash
# Compare branches
git diff main development

# See commits in development not in main
git log main..development

# Show branches merged into development
git branch --merged development
```

**Questions to Answer:**
1. What differences exist between main and development?
2. How many commits ahead is development from main?

---

### Exercise 4: Simulate a Pull Request Workflow

```bash
# Create a feature branch
git checkout development
git checkout -b feature/add-documentation

# Make changes
echo "## Project Documentation" >> README.md

# Commit changes
git add README.md
git commit -m "Update README with documentation section"

# Push branch
git push origin feature/add-documentation

# Now go to GitHub and create a Pull Request!
```

**Steps to Complete:**
1. Push your feature branch
2. Go to GitHub repository
3. Click "Compare & pull request"
4. Set base: development, compare: feature/add-documentation
5. Write description
6. Create pull request

---

### Exercise 5: Clean Up Old Branches

```bash
# List all branches
git branch -a

# Delete a local branch (after it's merged)
git branch -d feature/old-feature

# Delete a remote branch
git push origin --delete feature/old-feature

# Prune deleted remote branches
git fetch --prune
```

---

## Best Practices

### 1. Branch Naming Conventions

Use clear, descriptive names:

```
✅ Good:
- feature/user-authentication
- bugfix/login-error
- hotfix/security-patch
- docs/api-documentation

❌ Bad:
- test
- temp
- my-branch
- branch1
```

### 2. Commit Messages

Write meaningful commit messages:

```
✅ Good:
- "Add user authentication with JWT tokens"
- "Fix: Resolve login error on Safari browsers"
- "Refactor: Improve database query performance"

❌ Bad:
- "update"
- "fix stuff"
- "changes"
- "asdf"
```

### 3. Keep Branches Small and Focused

- One feature or fix per branch
- Easier to review
- Faster to merge
- Fewer merge conflicts

### 4. Regularly Sync with Development

```bash
# While working on your feature
git checkout development
git pull origin development
git checkout feature/my-feature
git merge development
```

### 5. Never Commit Directly to Main

- Always use pull requests
- Get code review
- Run automated tests
- Maintain stability

### 6. Delete Merged Branches

```bash
# After merging, delete the feature branch
git branch -d feature/merged-feature
git push origin --delete feature/merged-feature
```

## Common Commands Reference

### Branch Operations

```bash
# Create a new branch
git branch <branch-name>

# Switch to a branch
git checkout <branch-name>

# Create and switch to a new branch
git checkout -b <branch-name>

# List all branches
git branch -a

# Delete a branch
git branch -d <branch-name>

# Rename current branch
git branch -m <new-name>
```

### Merging and Updating

```bash
# Merge a branch into current branch
git merge <branch-name>

# Update current branch from remote
git pull origin <branch-name>

# Push current branch to remote
git push origin <branch-name>

# Fetch all remote branches
git fetch --all
```

### Viewing History

```bash
# View commit history
git log --oneline --graph --all

# View branch differences
git diff <branch1> <branch2>

# View commits in one branch but not another
git log <branch1>..<branch2>
```

## Workflow Diagram

```
1. Start: main branch
   ↓
2. Create: development branch
   ↓
3. Branch: feature/my-feature from development
   ↓
4. Work: Make changes and commit
   ↓
5. Push: Push feature branch
   ↓
6. PR: Create pull request to development
   ↓
7. Review: Get code review
   ↓
8. Merge: Merge to development
   ↓
9. Test: Test in development
   ↓
10. Release: Merge development to main
    ↓
11. Tag: Tag the release (optional)
```

## Troubleshooting

### Problem: Merge Conflicts

```bash
# When you get a merge conflict
git status  # See conflicting files

# Open and edit the files to resolve conflicts
# Look for <<<<<<, ======, >>>>>> markers

# After resolving
git add <resolved-files>
git commit -m "Resolve merge conflicts"
```

### Problem: Wrong Branch

```bash
# If you committed to the wrong branch
git log  # Find the commit hash
git checkout <correct-branch>
git cherry-pick <commit-hash>
git checkout <wrong-branch>
git reset --hard HEAD~1  # Remove the commit
```

### Problem: Need to Update Feature Branch

```bash
# Update your feature branch with latest development
git checkout feature/my-feature
git merge development

# Or use rebase for a cleaner history
git rebase development
```

## Quiz Questions

Test your understanding:

1. What is the main purpose of the development branch?
2. When should you merge to the main branch?
3. Why is it important to use pull requests?
4. What is a feature branch?
5. How do you keep your feature branch up to date with development?

## Additional Resources

- [Git Branching Documentation](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Atlassian Git Workflow Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

## Congratulations!

You've completed the Git Branch Workflow Workout! You now understand the difference between main and development branches and how to work with them effectively. Keep practicing! 🎉

---

**Remember:** Practice makes perfect. The more you work with branches, the more comfortable you'll become!
