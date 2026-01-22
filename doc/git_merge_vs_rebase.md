# Git Superpowers - Understanding Merge Vs Rebase
## Nick Zavlagkas | Agile Actors

---

## THE FUNDAMENTAL QUESTION

**"Should I merge or rebase?"**

This is one of the most common questions in Git workflows. Both commands integrate changes from one branch into another, but they do it in fundamentally different ways.

**The short answer:**
- **Merge** preserves history exactly as it happened
- **Rebase** rewrites history to create a linear timeline

**The long answer:** It depends on your context, team, and goals.

---

## WHAT IS MERGE?

### The Concept

**Merge** combines two branches by creating a new commit that has two parents. It preserves the exact history of how development happened.

```bash
# Basic merge
git checkout main
git merge feature-branch

# This creates a "merge commit" that combines both branches
```

### Visual Representation

**Before merge:**
```
main:     A---B---C
                \
feature:         D---E
```

**After merge:**
```
main:     A---B---C-------M
                \         /
feature:         D---E---/
```

The `M` is a merge commit that has two parents: `C` and `E`.

### What Merge Does

1. **Finds the common ancestor** (the point where branches diverged)
2. **Combines changes** from both branches
3. **Creates a merge commit** that ties both histories together
4. **Preserves all history** exactly as it happened

### Merge Characteristics

✅ **Preserves history** - Shows exactly when branches diverged and merged  
✅ **Non-destructive** - Never rewrites existing commits  
✅ **Safe for shared branches** - Others can see the full development story  
✅ **Shows branch context** - Clear indication of feature work  
⚠️ **Creates merge commits** - Can clutter history with many merge commits  
⚠️ **Non-linear history** - Graph can become complex with many branches  

---

## WHAT IS REBASE?

### The Concept

**Rebase** takes commits from one branch and replays them on top of another branch, creating a linear history as if the work was done sequentially.

```bash
# Basic rebase
git checkout feature-branch
git rebase main

# This replays feature-branch commits on top of main
```

### Visual Representation

**Before rebase:**
```
main:     A---B---C
                \
feature:         D---E
```

**After rebase:**
```
main:     A---B---C
                      \
feature:               D'---E'
```

Notice: `D'` and `E'` are **new commits** with different hashes. The original `D` and `E` are gone (but recoverable via reflog).

### What Rebase Does

1. **Finds the common ancestor** (where branches diverged)
2. **Temporarily removes** commits from feature branch
3. **Replays them** one by one on top of the target branch
4. **Creates new commits** with new hashes
5. **Results in linear history** - looks like work was done sequentially

### Rebase Characteristics

✅ **Linear history** - Clean, easy-to-read timeline  
✅ **No merge commits** - History stays focused on actual work  
✅ **Easier to review** - Changes appear in logical sequence  
⚠️ **Rewrites history** - Creates new commits, old ones are "lost"  
⚠️ **Requires force push** - If already pushed, need `git push --force`  
⚠️ **Can break shared work** - If others are using the branch, rebase causes problems  

---

## SIDE-BY-SIDE COMPARISON

### Scenario: Feature Branch Integration

**Starting State:**
```
main:     A---B---C
                \
feature:         D---E---F
```

### Using Merge

```bash
git checkout main
git merge feature
```

**Result:**
```
main:     A---B---C-------M
                \         /
feature:         D---E---F
```

**History shows:**
- Feature branch existed
- It was merged at point M
- All original commits preserved

### Using Rebase

```bash
git checkout feature
git rebase main
git checkout main
git merge feature  # Fast-forward merge
```

**Result:**
```
main:     A---B---C---D'---E'---F'
```

**History shows:**
- Linear sequence
- No indication a branch existed
- Looks like work was done directly on main

---

## WHEN TO USE MERGE

### Use Merge When:

1. **Working on shared/public branches**
   - Others might be using the branch
   - Rebasing would force them to rewrite their work
   - Example: `main`, `develop`, or any branch others depend on

2. **You want to preserve branch context**
   - Show that work happened in a feature branch
   - Document when features were integrated
   - Example: "This merge shows when authentication feature was added"

3. **Team prefers merge workflow**
   - Some teams standardize on merge
   - Easier for less experienced developers
   - No risk of history rewriting

4. **You want to see the full development story**
   - Understand when branches diverged
   - See parallel development clearly
   - Example: Multiple features developed simultaneously

### Merge Best Practices

```bash
# Use --no-ff to always create merge commit (even if fast-forward possible)
git merge --no-ff feature-branch

# Add meaningful merge commit message
git merge -m "Merge feature: User authentication" feature-branch

# Review before merging
git log main..feature-branch  # See what will be merged
```

---

## WHEN TO USE REBASE

### Use Rebase When:

1. **Working on local/private branches**
   - Only you are using the branch
   - No one else has pulled it
   - Example: Your personal feature branch

2. **You want clean, linear history**
   - Easier to read and understand
   - Better for code reviews
   - Example: Open source projects often prefer linear history

3. **Before merging to main**
   - Clean up your feature branch
   - Make it easier to review
   - Example: Rebase feature branch, then merge to main

4. **Interactive rebase for cleanup**
   - Combine multiple small commits
   - Reword commit messages
   - Remove or reorder commits
   - Example: `git rebase -i HEAD~5` to clean up last 5 commits

### Rebase Best Practices

```bash
# Always rebase onto the latest main
git checkout feature-branch
git fetch origin
git rebase origin/main

# Use interactive rebase to clean up commits
git rebase -i HEAD~3  # Clean up last 3 commits

# After rebase, force push (only if branch is private!)
git push --force-with-lease origin feature-branch
```

**⚠️ CRITICAL:** Never rebase branches that others are using!

---

## THE GOLDEN RULE

### Local vs. Shared Branches

```
LOCAL BRANCHES (yours only):
✅ Merge: Safe
✅ Rebase: Safe
✅ Reset: Safe
✅ Any operation: Safe

SHARED BRANCHES (others use them):
✅ Merge: Safe
❌ Rebase: DANGEROUS (rewrites history others depend on)
❌ Reset: DANGEROUS (loses commits others have)
✅ Revert: Safe (adds new commit, doesn't rewrite)
```

**The Rule:**
- **Local branches:** Do whatever you want (merge, rebase, reset)
- **Shared branches:** Only use non-destructive operations (merge, revert)

---

## PRACTICAL EXAMPLES

### Example 1: Feature Branch Workflow (Merge)

```bash
# Start feature
git checkout -b feature/user-login
# ... make commits D, E, F ...

# Meanwhile, main gets updates
git checkout main
git pull origin main  # Gets commits B, C

# Merge feature into main
git merge feature/user-login
# Creates merge commit M

# Result: History shows feature branch clearly
```

**When to use:** Team workflow, shared branches, preserving context

---

### Example 2: Feature Branch Workflow (Rebase)

```bash
# Start feature
git checkout -b feature/user-login
# ... make commits D, E, F ...

# Update feature branch with latest main
git fetch origin
git rebase origin/main
# Replays D, E, F on top of latest main

# Merge to main (fast-forward)
git checkout main
git merge feature/user-login
# Fast-forward merge (no merge commit needed)

# Result: Linear history, no merge commits
```

**When to use:** Personal branches, clean history preference, before final merge

---

### Example 3: Interactive Rebase for Cleanup

```bash
# You made 5 messy commits
git log --oneline
# abc123 Fix typo
# def456 Another fix
# ghi789 Actually fix it properly
# jkl012 Add feature
# mno345 Initial work

# Clean them up
git rebase -i HEAD~5

# In editor, you can:
# - pick: keep commit as-is
# - squash: combine with previous commit
# - reword: change commit message
# - drop: remove commit

# Example: Squash first 3 into one
pick mno345 Initial work
squash jkl012 Add feature
squash ghi789 Actually fix it properly
squash def456 Another fix
pick abc123 Fix typo

# Result: 2 clean commits instead of 5 messy ones
```

**When to use:** Before pushing, cleaning up work-in-progress commits

---

## MERGE CONFLICTS VS REBASE CONFLICTS

### Merge Conflicts

```bash
git checkout main
git merge feature-branch

# If conflicts occur:
# CONFLICT (content): Merge conflict in file.txt
# Automatic merge failed; fix conflicts and then commit the result.

# Resolve conflicts, then:
git add file.txt
git commit  # Completes the merge
```

**Characteristics:**
- One conflict resolution point
- Resolve all conflicts, then commit once
- Merge commit contains the resolution

### Rebase Conflicts

```bash
git checkout feature-branch
git rebase main

# If conflicts occur:
# CONFLICT (content): Rebase conflict in file.txt

# Resolve conflicts, then:
git add file.txt
git rebase --continue

# May need to resolve conflicts MULTIPLE times
# (once for each commit being replayed)
```

**Characteristics:**
- May have multiple conflict resolution points
- Resolve conflicts for EACH commit being replayed
- Each commit gets replayed individually

**Tip:** Rebase conflicts can be more tedious, but result in cleaner history.

---

## COMMON SCENARIOS & RECOMMENDATIONS

### Scenario 1: Personal Feature Branch

**Situation:** You're working on a feature, branch is only yours.

**Recommendation:** **Rebase** before merging
```bash
git checkout feature-branch
git fetch origin
git rebase origin/main
git checkout main
git merge feature-branch  # Fast-forward
```

**Why:** Clean history, no unnecessary merge commits.

---

### Scenario 2: Team Feature Branch

**Situation:** Multiple people working on same feature branch.

**Recommendation:** **Merge** only
```bash
git checkout main
git merge feature-branch
```

**Why:** Rebasing would force teammates to rewrite their work.

---

### Scenario 3: Updating Feature Branch with Main

**Situation:** Main has new commits, you want them in your feature.

**Option A - Merge:**
```bash
git checkout feature-branch
git merge main
# Creates merge commit in feature branch
```

**Option B - Rebase:**
```bash
git checkout feature-branch
git rebase main
# Replays your commits on top of main
```

**Recommendation:** 
- If branch is private: **Rebase** (cleaner)
- If branch is shared: **Merge** (safer)

---

### Scenario 4: Cleaning Up Before Code Review

**Situation:** You have 10 messy commits, want to clean up before PR.

**Recommendation:** **Interactive Rebase**
```bash
git rebase -i HEAD~10
# Combine related commits
# Reword messages
# Remove unnecessary commits
```

**Why:** Cleaner history makes code review easier.

---

## ADVANCED: REBASE STRATEGIES

### Strategy 1: Rebase and Merge (Best of Both)

```bash
# Step 1: Rebase feature branch (local cleanup)
git checkout feature-branch
git rebase main

# Step 2: Merge with --no-ff (preserve context)
git checkout main
git merge --no-ff feature-branch
```

**Result:** Clean commits in feature branch, but merge commit shows when it was integrated.

---

### Strategy 2: Squash and Merge

```bash
# Merge all feature commits into one
git checkout main
git merge --squash feature-branch
git commit -m "Add user authentication feature"
```

**Result:** All feature work becomes one commit on main.

**When to use:** Feature branch has many small commits, want single commit on main.

---

### Strategy 3: Rebase Onto (Selective Rebase)

```bash
# Rebase only part of branch
git rebase --onto new-base old-base feature-branch
```

**Example:**
```bash
# Rebase commits after commit abc123 onto main
git rebase --onto main abc123 feature-branch
```

**When to use:** Want to rebase only some commits, not all.

---

## TROUBLESHOOTING

### Problem: Rebase Conflict - How to Abort

```bash
# If rebase gets too complicated
git rebase --abort
# Returns to state before rebase started
```

---

### Problem: Accidentally Rebased Shared Branch

```bash
# If you already pushed the rebase
# Option 1: Ask team to reset (if possible)
# Option 2: Revert the rebase
git revert <merge-commit>

# Option 3: Recover from reflog
git reflog
git reset --hard <commit-before-rebase>
git push --force  # Only if team agrees!
```

**Prevention:** Always check if branch is shared before rebasing.

---

### Problem: Merge Created Unwanted Merge Commit

```bash
# If you want linear history instead
git reset --hard HEAD~1  # Remove merge commit
git rebase feature-branch  # Rebase instead
```

**Note:** Only if merge commit hasn't been pushed yet!

---

## DECISION MATRIX

| Situation | Recommended Approach | Why |
|-----------|---------------------|-----|
| Personal feature branch | Rebase then merge | Clean history |
| Shared feature branch | Merge only | Safe for team |
| Updating with main (private) | Rebase | Linear history |
| Updating with main (shared) | Merge | Preserves team work |
| Before code review | Interactive rebase | Clean up commits |
| Main/master branch | Merge only | Never rebase main! |
| Cleaning up commits | Interactive rebase | Combine/fix commits |
| Preserving branch context | Merge | Shows development story |

---

## KEY TAKEAWAYS

### The Core Principles

1. **Merge preserves history, rebase rewrites it**
   - Merge: "This is how it happened"
   - Rebase: "This is how it should have happened"

2. **Local vs. shared is the key distinction**
   - Local branches: Rebase freely
   - Shared branches: Merge only

3. **Both are valid, context matters**
   - No "right" answer for all situations
   - Choose based on team, project, and goals

4. **History is a tool, not a burden**
   - Use merge to preserve context
   - Use rebase to clean up
   - Both serve different purposes

5. **Safety first**
   - When in doubt, use merge
   - Rebase only when you're certain it's safe
   - Check if branch is shared before rebasing

---

## PRACTICAL WORKFLOW RECOMMENDATIONS

### For Individual Developers

```bash
# Daily workflow
1. Work on feature branch (local)
2. Regularly rebase onto main: git rebase main
3. Clean up commits: git rebase -i HEAD~n
4. When ready: Merge to main (or create PR)
```

### For Teams

```bash
# Team workflow
1. Work on feature branch (may be shared)
2. Update with main: git merge main (or rebase if private)
3. When ready: Create PR, team reviews
4. Merge to main: git merge --no-ff feature-branch
```

### For Open Source Projects

```bash
# Open source workflow (often prefers rebase)
1. Fork and create feature branch
2. Make commits, keep branch clean
3. Rebase onto upstream main regularly
4. Submit PR with clean, linear history
5. Maintainers may squash-merge
```

---

## COMMON MYTHS DEBUNKED

### Myth 1: "Rebase is always better"

**Reality:** Rebase is better for clean history, but merge is safer for shared work. Context matters.

### Myth 2: "Merge commits are bad"

**Reality:** Merge commits preserve valuable context about when and how features were integrated.

### Myth 3: "You can't rebase after pushing"

**Reality:** You can, but you need `--force-with-lease` and should only do it on private branches.

### Myth 4: "Rebase loses commits"

**Reality:** Original commits are in reflog. They're recoverable, just not in the main history.

### Myth 5: "One approach fits all projects"

**Reality:** Different projects have different needs. Some prefer merge, some prefer rebase.

---

## VISUAL SUMMARY

### Merge Workflow
```
Feature Development:
main:     A---B---C
                \
feature:         D---E---F

After Merge:
main:     A---B---C-------M
                \         /
feature:         D---E---F
```

### Rebase Workflow
```
Feature Development:
main:     A---B---C
                \
feature:         D---E---F

After Rebase:
main:     A---B---C
                      \
feature:               D'---E'---F'

After Merge (Fast-forward):
main:     A---B---C---D'---E'---F'
```

---

## FINAL THOUGHTS

**Merge and rebase are both powerful tools.** Neither is inherently better or worse. The choice depends on:

- **Your team's preferences**
- **Project requirements**
- **Whether branches are shared**
- **History clarity goals**

**The most important rule:** 
> **Never rebase shared branches. Always merge shared branches.**

**For everything else:** Choose based on what makes sense for your context.

**Remember:** Git is flexible. You can always recover from mistakes (thanks to reflog!). Experiment on local branches to understand both approaches.

---

## QUICK REFERENCE

### Merge Commands
```bash
# Basic merge
git merge <branch>

# Merge with no fast-forward (always create merge commit)
git merge --no-ff <branch>

# Merge with custom message
git merge -m "Message" <branch>

# Abort merge in progress
git merge --abort
```

### Rebase Commands
```bash
# Basic rebase
git rebase <branch>

# Interactive rebase (last n commits)
git rebase -i HEAD~n

# Rebase onto specific base
git rebase --onto <new-base> <old-base> <branch>

# Continue rebase after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort

# Skip current commit during rebase
git rebase --skip
```

### Safety Checks
```bash
# Check if branch is shared (has remote tracking)
git branch -vv

# See what commits would be affected
git log <branch>..main

# Check reflog before destructive operations
git reflog
```

---

*Git Superpowers Workshop*  
*Presented by Nick Zavlagkas | Agile Actors*  
*Understanding Merge vs Rebase: Choose the Right Tool for the Job*

