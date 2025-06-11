# Git Workflow for ESG Financial Assistant

This guide provides all the basics for working with Git on our team, especially for beginners.

## Getting Started

### Cloning the Repository

To get the project on your computer:

```bash
git clone https://github.com/AI4ALL-ESG-Investing/esg-financial-assistant.git
cd esg-financial-assistant
```

## Our Team Workflow

We follow these steps for all changes:

1. **Create a branch** for your feature or bug fix
2. **Make changes** and commit them
3. **Push your branch** to GitHub
4. **Create a Pull Request** for team review
5. **Get approval** and merge your changes

## Step-by-Step Instructions

### 1. Create a New Branch

Always start by creating a branch for your work:

```bash
git checkout main       # Start from latest main branch
git pull                # Get latest changes
git checkout -b feature/your-feature-name
```

Name your branch to describe what you're working on (e.g., `feature/add-data-visualization` or `fix/login-error`).

### 2. Make and Commit Changes

As you work, regularly commit your changes:

Check status of your changes:

```bash
git status
```

Add your changes:

```bash
git add .              # Add all changes
# OR
git add path/to/file   # Add specific file
```

Commit with a descriptive message:

```bash
git commit -m "Add ESG score calculation function"
```

### 3. Push Your Branch

Send your changes to GitHub:

```bash
git push origin feature/your-feature-name
```

### 4. Create a Pull Request (PR)

When your feature is complete:

1. Go to our GitHub repository
2. Click "Pull Requests" → "New Pull Request"
3. Select your branch
4. Fill out the PR template with:
   - Description of your changes
   - Type of change
   - Checklist items

### 5. Review Process

- Another team member will review your code
- Address any feedback with new commits
- Once approved, your code can be merged

## When to Create Pull Requests

- When finishing a complete feature
- When your changes might affect others' work
- For any changes going into the main branch

## Common Git Commands

### Viewing History

```bash
git log
```

### Undoing Changes

For uncommitted changes:

```bash
git checkout -- path/to/your/file  # Discard changes to a file
```

For staged changes:

```bash
git reset HEAD path/to/your/file   # Unstage changes
```

### After Merging

Delete your branch (optional):

```bash
git branch -d feature/your-feature-name
```

## Tips for Beginners

- Commit often with clear messages
- Pull from main regularly to avoid conflicts
- When in doubt, ask a team member for help
- Don't commit data files larger than 30MB
- Remember to fill out the PR template completely