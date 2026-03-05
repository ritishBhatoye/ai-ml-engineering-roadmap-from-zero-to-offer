# Contributing Guide

Thank you for your interest in improving this roadmap! This guide will help you contribute effectively.

---

## Table of Contents

1. [What We're Looking For](#1-what-were-looking-for)
2. [What We're NOT Looking For](#2-what-were-not-looking-for)
3. [How to Contribute](#3-how-to-contribute)
4. [Folder Conventions](#4-folder-conventions)
5. [Content Guidelines](#5-content-guidelines)
6. [Pull Request Process](#6-pull-request-process)
7. [Quality Standards](#7-quality-standards)

---

## 1. What We're Looking For

### High-Priority Contributions

| Type | Example | Why It Matters |
|------|---------|----------------|
| **Corrections** | Fix factual errors, broken links, typos | Keeps roadmap accurate |
| **Better Resources** | Higher-quality free course replacing existing | Improves learning |
| **New Interview Questions** | Real questions from ML interviews | Helps students prepare |
| **Project Improvements** | Better starter templates, clearer instructions | Makes projects more doable |

### Medium-Priority Contributions

| Type | Example |
|------|---------|
| New topic explanations | Adding content to existing topics |
| Additional exercises | More practice problems |
| Case studies | New real-world ML problems |

---

## 2. What We're NOT Looking For

- ❌ Research-level or PhD-focused content
- ❌ Promotional links to paid courses or products
- ❌ Content that doesn't directly help with interview preparation
- ❌ Surface-level "top 10 algorithms" additions
- ❌ Content without practical exercises
- ❌ Duplicate resources (check existing list first)

---

## 3. How to Contribute

### Step 1: Fork the Repository

```
1. Go to https://github.com/your-username/AI-ML-Engineering-Roadmap-From-Zero-To-Offer
2. Click "Fork" button
3. Clone your fork locally
```

### Step 2: Create a Feature Branch

```bash
git checkout -b fix/typo-in-linear-algebra
# or
git checkout -b add/new-interview-question
# or
git checkout -b improve/project-template
```

### Step 3: Make Your Changes

Follow the content guidelines below.

### Step 4: Submit a Pull Request

1. Push your branch: `git push origin fix/typo-in-linear-algebra`
2. Go to original repo
3. Click "New Pull Request"
4. Fill in the template with:
   - What you changed
   - Why it matters
   - How to test it

---

## 4. Folder Conventions

### Existing Structure

```
📦 AI-ML-Engineering-Roadmap-From-Zero-To-Offer/
│
├── 📂 01-mathematics/         # Topic: Math foundations
│   └── *.md                   # Each topic = one file
│
├── 📂 02-python-for-ml/       # Topic: Python for ML
│   └── *.md
│
├── 📂 03-ml-fundamentals/     # Topic: Core ML
│   └── *.md
│
├── 📂 04-deep-learning/       # Topic: Deep Learning
│   └── *.md
│
├── 📂 05-sql-for-ml/          # Topic: SQL
│   └── *.md
│
├── 📂 06-ml-coding/           # Topic: Coding practice
│   └── *.md
│
├── 📂 07-case-studies/        # Real-world examples
│   └── *.md
│
├── 📂 08-system-design/       # Production ML
│   └── *.md
│
├── 📂 09-deployment/          # MLOps
│   └── *.md
│
├── 📂 10-interview-strategy/  # Interview prep
│   └── *.md
│
├── 📂 projects/               # Project templates
│   └── [project-name]/
│       └── README.md
│
└── 📂 resources/              # Curated resources
    └── *.md
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Topic files | `kebab-case.md` | `linear-algebra.md` |
| Project folders | `kebab-case/` | `01-eda-project/` |
| Images | `kebab-case.png` | `confusion-matrix.png` |

---

## 5. Content Guidelines

### Topic Files (01-XX folders)

Each topic file should include:

```markdown
# Topic Name

> **Interview weight:** ⭐⭐⭐ (1-5 stars)
> **Time to study:** X hours
> **Goal:** What learner will achieve

---

## What Interviewers Actually Test

[What real questions they'll ask]

## Core Concepts

[Key concepts with code examples]

### Code Example

```python
# Minimal, runnable example
import numpy as np

# Clear, well-commented
def example():
    pass
```

## Common Interview Questions

1. **Q: Question?**
   > Answer with explanation

## Try It Yourself

1. Exercise 1
2. Exercise 2

## Resources

- [Resource name](link) — Why it's useful
```

### Project Templates (projects/ folder)

Each project should include:

```markdown
# Project Name

## Objective
[One sentence on what to build]

## Why This Matters
[Why interviewers care about this project]

## Suggested Datasets
| Dataset | Use Case |
|---------|----------|
| Name | Description |

## Deliverables Checklist
- [ ] Requirement 1
- [ ] Requirement 2

## Assessment Criteria
| Criterion | Weight |
|-----------|--------|
| Aspect | % |

## Suggested Structure
```
folder/
├── src/
├── config/
├── README.md
```

## Starter Code
[Minimal working code]
```

### Interview Questions (10-interview-strategy/)

Format:

```markdown
## Category Name

1. **Q: Question?**
   > Answer

2. **Q: Question?**
   > Answer
```

---

## 6. Pull Request Process

### PR Title Format

```
[type]: [short description]

Examples:
fix: Typo in linear-algebra.md
feat: Add new interview question about XGBoost
improve: Better starter code for Project 2
```

### PR Description Template

```markdown
## What Changed
[Brief description]

## Why It Matters
[How this helps learners]

## Testing
[How to verify the changes work]

## Screenshots (if applicable)
[Add images if relevant]
```

### Review Criteria

PRs will be reviewed for:
- ✅ Accuracy of content
- ✅ Relevance to interview prep
- ✅ Code correctness
- ✅ Formatting consistency
- ✅ Grammar and clarity

---

## 7. Quality Standards

### Code Examples

| ✅ Do | ❌ Don't |
|-------|----------|
| Minimal, runnable snippets | Full complex applications |
| Well-commented | Cryptic one-liners |
| Import statements included | Assumes context |
| Works with standard libraries | Requires obscure dependencies |

### Writing Style

| ✅ Do | ❌ Don't |
|-------|---------|
| Clear, professional language | Academic jargon without explanation |
| Practical, hands-on focus | Theoretical without application |
| Interview-focused content | Research-level depth |
| Consistent formatting | Random structure |

### Links

| ✅ Do | ❌ Don't |
|-------|----------|
| Verify links work | Dead links |
| Use official documentation | Unverified blogs |
| Prefer free resources | Paywalled content |

---

## Questions?

If you're unsure about anything, feel free to:
1. Open an issue to discuss
2. Ask in PR comments

We appreciate all contributions, big and small!

---

## Code of Conduct

Be respectful, constructive, and focused on helping students succeed. That's it.
