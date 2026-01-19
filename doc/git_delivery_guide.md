# Git Superpowers Workshop - Complete Guide
## Nick Zavlagkas | Agile Actors | Friday Presentation

---

## QUICK START (Before Friday)

### 1. Download & Open Presentation
```bash
# The presentation file: git_superpowers.html
# Open in browser: Chrome, Firefox, Safari, Edge
# Controls: Arrow keys or buttons for navigation
# Speaker notes appear at bottom of each slide
```

### 2. Test Your Environment
```bash
# Check Git
git --version
# Expected: git version 2.x.x or higher

# Check Java
javac -version
# Expected: javac 11.0.x or higher (any modern version works)
```

### 3. Create the POJO Project (Now, before Friday)
```bash
# Full setup from scratch
cd ~/Desktop  # or preferred location
mkdir git-superpowers
cd git-superpowers
git init

# Configure Git
git config user.name "Your Name"
git config user.email "your@email.com"

# Create project structure
mkdir src
touch README.md

# Create Main.java
cat > src/Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
    }
}
EOF

# Initial commit
git add .
git commit -m "Initial commit: Basic Java project setup"

# Verify
git log
```

**Expected output after git log:**
```
commit abc1234567890... (HEAD -> main)
Author: Your Name <your@email.com>
Date:   [timestamp]

    Initial commit: Basic Java project setup
```

---

## PRESENTATION STRUCTURE (17 Slides)

### Slide Breakdown & Speaker Notes

#### SLIDE 1: Title & Welcoming
- **Your Role:** Set tone. Smile. Make eye contact.
- **Key Message:** "This is not a lecture. This is a confidence journey."
- **Action:** Ask "Who feels nervous about Git?" Normalize the fear.
- **Transition:** "By the end, you won't feel that way."

#### SLIDES 2-3: Mental Model
- **Focus:** Reframe Git as TIME MACHINE, not SCARY TOOL
- **Key Concept:** Snapshots (immutable), Branches (cheap pointers), HEAD (your location)
- **Action:** Show your git log from initial commit. Explain: "This snapshot is immutable. It will always exist."
- **Transition:** "Now let's see how this works in practice."

#### SLIDES 4-5: Project Init & Myth Debunking
- **Action:** Initialize project LIVE. Go slowly. Explain each step.
- **After setup:** Show git log. Ask: "Where is this commit?" Answer: "In the .git folder, safely stored."
- **Myths:** Address each one: "Reset doesn't delete. Rebase doesn't destroy. Detached HEAD is safe."
- **Transition:** "Now I'll prove every myth is false."

#### SLIDES 6-7: Superpower #1 - Reflog (THE KEY MOMENT)
- **This is where fear dies.** Show reflog. Make intentional mistake. Recover it.
- **Script:** 
  1. "Make a commit"
  2. "Reset hard—it's 'gone'"
  3. "But it's in reflog"
  4. "Recover it"
  5. "It's back. Nothing is ever lost."
- **Audience moment:** They'll see fear was unjustified.

#### SLIDES 8-9: Superpower #2 - Detached HEAD
- **Message:** "This is a playground. You can break everything safely."
- **Demo:** Checkout old commit → modify code → create branch or discard
- **Key insight:** "If you want to keep work, branch it. If you don't, discard it. Zero risk."

#### SLIDES 10-11: Superpower #3 - Reset vs Revert vs Checkout
- **THIS IS CRITICAL DECISION FRAMEWORK**
- **Reset:** Local history rewriting (safe on local only)
- **Revert:** Create undo commit (safe on shared branches)
- **Checkout:** Discard uncommitted changes (file level)
- **Demo same mistake three ways** so they see when to use each

#### SLIDE 12: Superpower #4 - Branches Are Cheap
- **Key:** "A branch is just a pointer. Cost = nothing. Delete without guilt."
- **Demo:** Create many branches → break code → delete branches → check reflog (still there)
- **Message:** "Branches enable fearless experimentation."

#### SLIDE 13: Superpower #5 - Stash
- **Context:** "Halfway through code. Emergency happens."
- **Solution:** Stash → context switch → come back → unstash
- **Message:** "Stash is psychological relief. Your work is safe."

#### SLIDE 14: Superpower #6 - Cherry-pick
- **Use case:** "One good commit is on the wrong branch"
- **Solution:** "Cherry-pick it to current branch"
- **Message:** "Cherry-pick is selective, surgical recovery."

#### SLIDE 15: Professional Safety Rules
- **RULE 1:** Rewrite history on LOCAL branches (reset, rebase, force push = OK)
- **RULE 2:** NEVER rewrite on SHARED branches (use revert instead)
- **Message:** "You can break your house. You cannot break your teammate's house."

#### SLIDE 16: Emotional Closure
- **Message:** "Git doesn't punish mistakes. It records them so you can undo them."
- **Proof:** List all superpowers and what each enables
- **Final statement:** "Nothing is ever truly lost. You control Git now."
- **Close with:** "Questions?"

#### SLIDE 17: Q&A Open Floor
- **Your role:** Take real questions. Use git to demonstrate live.
- **Message:** "Real-time problem-solving reinforces learning."

---

## LIVE DEMO SCRIPT

### Demo 1: Project Initialization (5 minutes)
```bash
# Show step-by-step setup
mkdir git-superpowers
cd git-superpowers
git init
mkdir src
cat > src/Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
    }
}
EOF
git config user.name "Nick Zavlagkas"
git config user.email "nick@agileactors.com"
git add .
git commit -m "Initial commit: Basic Java project"
git log
```
**Explanation:** "Every step creates a snapshot. git init creates the database (.git). Files get staged. Commit saves the snapshot."

---

### Demo 2: Reflog Recovery (7 minutes) - THE KEY DEMO
```bash
# Step 1: Make a real commit
echo "Feature: User login" > src/Main.java
git add src/Main.java
git commit -m "Add user authentication"
git log --oneline

# Step 2: "Accidentally" reset hard
echo "Watch carefully..."
git reset --hard HEAD~1
echo "I just deleted the commit."
git log --oneline
echo "It's gone from the log. You see?"

# Step 3: The magic
echo "But here's the magic..."
git reflog
echo "See that commit in reflog? It's still there."

# Step 4: Recover
git reset --hard <commit_hash_from_reflog>
echo "Check the log..."
git log --oneline
echo "It's back! Nothing is ever lost."
```
**Audience Psychology:** This is where fear leaves the room. They see the "impossible" recovery.

---

### Demo 3: Detached HEAD Exploration (6 minutes)
```bash
# Step 1: Show current history
git log --oneline

# Step 2: Checkout an old commit
git checkout <first_commit_hash>
git status
echo "We're in detached HEAD. This is a playground."

# Step 3: Break code intentionally
echo "BREAKING CODE INTENTIONALLY" > src/Main.java
git add .
git commit -m "Experimental chaos"

# Step 4: Create a branch to save this
git checkout -b experiment-branch
echo "Saved on experiment-branch"

# Step 5: Or discard and go back to main
git checkout main
git status
echo "We're back on main. The experiment is isolated."
```
**Message:** "Detached HEAD is not dangerous. It's liberation."

---

### Demo 4: Reset vs Revert vs Checkout (8 minutes)
```bash
# Create a bad commit
echo "BAD CODE" > src/Main.java
git add .
git commit -m "This is a mistake"
git log --oneline

# --- STRATEGY 1: Reset ---
echo "Strategy 1: Reset (local history rewrite)"
git reset --hard HEAD~1
git log --oneline
echo "Commit is gone from log. But check reflog..."
git reflog

# Recreate the bad commit for strategy 2
echo "BAD CODE" > src/Main.java
git add .
git commit -m "This is a mistake"

# --- STRATEGY 2: Revert ---
echo "Strategy 2: Revert (safe for shared branches)"
git revert HEAD
echo "Check the log now..."
git log --oneline
echo "Two commits: the mistake AND the undo."

# Reset for strategy 3 demo
git reset --hard HEAD~2

# --- STRATEGY 3: Checkout (unstaged files) ---
echo "Strategy 3: Checkout (discard unstaged changes)"
echo "UNCOMMITTED MISTAKE" > src/Main.java
git status
git checkout src/Main.java
git status
echo "File is clean. Unstaged changes are gone."
```
**Message:** "Same problem. Three solutions. Choose based on context."

---

### Demo 5: Branches Are Cheap (5 minutes)
```bash
# Create many experimental branches
git checkout -b feature-experiment-1
git checkout -b feature-experiment-2
git checkout -b crazy-refactor

# Break code on crazy-refactor
echo "CHAOS!!!" > src/Main.java
git add .
git commit -m "Testing extreme changes"

# Go back to main
git checkout main
git log --oneline

# Delete the crazy branch
git branch -D crazy-refactor

# Check reflog (commits still exist)
git reflog
echo "The commits are still in reflog. Nothing lost."
```
**Message:** "Branches are free. Delete without guilt."

---

### Demo 6: Stash & Cherry-pick (4 minutes)
```bash
# --- STASH DEMO ---
echo "HALFWAY THROUGH" > src/Main.java
git status
git stash
git status
echo "Work is stashed. Context is clean."

# Come back later
git stash pop
git status
echo "Work is restored."

# --- CHERRY-PICK DEMO ---
git log --oneline
echo "Let's say this commit is on the wrong branch"
git checkout main
git cherry-pick <commit_hash>
git log --oneline
echo "That specific commit is now on main too."
```
**Message:** "Stash is the panic button. Cherry-pick is surgical precision."

---

## TIPS FOR DELIVERY

### Before Presenting
- [ ] Test all demos with the exact commands (don't improvise)
- [ ] Have terminal font at size 18+ for visibility
- [ ] Use dark terminal theme for high contrast
- [ ] Open presentation in fullscreen
- [ ] Have speaker notes visible or printed

### During Presenting
- [ ] Speak slowly. Pause often. Let concepts sink in.
- [ ] After each demo, ask: "Questions?" Don't rush.
- [ ] Always show git status or git log after commands
- [ ] Repeat the safety message: "Nothing is ever lost."
- [ ] Watch audience faces. Adjust pace if confused.

### Confidence Statements (Use Often)
- "This is version control. Control is the keyword."
- "Git is forgiving. I'm about to prove it."
- "If it's in your Git history, you can get it back. Every. Single. Time."
- "Mistakes are not problems. They're learning opportunities."
- "You can't break anything that matters. Git is your insurance policy."

### If Something Goes Wrong (Perfect Teaching Moment)
1. **Don't panic.** Say: "Perfect. Let me show you how to recover from this."
2. **Use git reflog** to recover.
3. **Explain:** "See? Even accidents are recoverable."
4. **Continue:** "This is exactly why Git is safe."

---

## AGILE ACTORS BRANDING

### Color Palette (Used in Presentation)
- **Deep Teal:** #0F9A8C (Primary)
- **Bright Cyan:** #00D4D4 (Accent)
- **Dark Charcoal:** #1A1A1A (Background)
- **Professional Gray:** #F5F5F5 (Light Background)

### Tone
- Professional, mentor-like
- Calm and reassuring
- Confident without being arrogant
- Approachable and clear

### Visual Theme
- Clean, modern gradients
- High contrast for readability
- Code blocks clearly formatted
- Speaker notes for presenter guidance

---

## HANDLING QUESTIONS

### Common Questions (Prepared Answers)

**Q: "Can I really never lose work?"**
A: "If you've committed it to Git, yes. Uncommitted work is different—that's what stash is for. Once committed, it's in reflog forever."

**Q: "What if I force pushed to main by accident?"**
A: "Reflog only lives on your computer. But if others have the old commits, they can push them back. This is why we don't force push shared branches."

**Q: "Is rebase as dangerous as people say?"**
A: "On local branches? No. On shared branches? Yes—your teammates will have inconsistent history. Use revert on shared, rebase on local."

**Q: "How long does reflog keep commits?"**
A: "Usually 90 days by default, but you can extend it. The point: it's a safety net for reasonable time periods."

**Q: "What's the difference between git reset and git revert?"**
A: "Reset moves HEAD and rewrites history (local only). Revert creates a new commit that undoes changes (safe for shared). Different tools for different contexts."

---

## PRACTICE CHECKLIST

Before Friday, run through:
- [ ] All 6 demo scripts (in order, no shortcuts)
- [ ] git reflog recovery twice (the key skill)
- [ ] Each superpower demonstration once
- [ ] Professional rules explanation (local vs. shared)
- [ ] One recovery-from-mistake scenario (good fallback)

**Time estimate:** 1 hour practice = smooth 1-hour presentation

---

## PRESENTATION TIMING (Updated for 28 Slides)

**Total: ~75 minutes including Q&A** (Extended due to enhanced content)

- Slide 1: Title & Welcome (3 min)
- Slide 2: Project Setup Demo (4 min live demo) ← MOVED EARLIER
- Slide 3: Git Is Not Dangerous (3 min)
- Slide 4: How Git Really Works (3 min)
- Slide 5: Visual Git State Diagram (3 min) ← NEW
- Slide 6: Debunk Myths (2 min)
- Slide 7: Real-World Scenario - Reflog (2 min) ← NEW
- Slides 8-9: Reflog Superpower + Demo (7 min live demo) ← KEY MOMENT
- Slide 10: Check Your Understanding - Reflog (3 min) ← NEW
- Slide 11: Real-World Scenario - Detached HEAD (2 min) ← NEW
- Slides 12-13: Detached HEAD + Demo (6 min live demo)
- Slide 14: Real-World Scenario - Three Ways (2 min) ← NEW
- Slides 15-18: Reset/Revert/Checkout + Decision Matrix (10 min) ← BROKEN DOWN
- Slide 19: Demo - Three Undo Strategies (5 min) ← ENHANCED
- Slide 20: Real-World Scenario - Branches (2 min) ← NEW
- Slide 21: Branches Are Cheap (5 min live demo)
- Slide 22: Real-World Scenario - Stash (2 min) ← NEW
- Slide 23: Stash (4 min live demo)
- Slide 24: Real-World Scenario - Cherry-pick (2 min) ← NEW
- Slide 25: Cherry-pick (4 min live demo)
- Slide 26: Common Mistakes & Recoveries (4 min) ← NEW
- Slide 27: Professional Safety Rules (3 min discussion)
- Slide 28: Emotional Closure (2 min)
- Slide 29: Q&A (15 min open discussion)

---

## SUCCESS METRICS

By the end of Friday, attendees should:

✅ Understand Git as a time machine (snapshots, not diffs)
✅ Know what reflog does and how to use it
✅ Feel confident experimenting with branches
✅ Know when to use reset vs. revert vs. checkout
✅ Understand "safe on local, careful on shared"
✅ Have zero fear about Git mistakes
✅ Leave thinking: "I can't break anything anymore"

---

## FILES INCLUDED

1. **git_superpowers.html** - The full presentation (17 slides, all speaker notes)
2. **git_superpowers_setup.md** - Preparation checklist and reference guide
3. **This file** - Complete delivery guide with demo scripts

---

## READY TO PRESENT?

**Friday Checklist (Day Of):**
- [ ] Terminal ready, 10 projects created in fresh folder
- [ ] Presentation open in browser, fullscreen capable
- [ ] Speaker notes visible or printed
- [ ] Internet working (if showing anything external)
- [ ] Projector/screen working
- [ ] Audience seated 5 min before start
- [ ] Your confidence level: HIGH ✅

**Final Note:**
You're going to remove Git anxiety from this room. That's powerful. Own it.

**Let's go make Git fearless. — Nick**

---

*Agile Actors | Git Superpowers Workshop*
*Presented by Nick Zavlagkas*
*Friday, [Date]*
