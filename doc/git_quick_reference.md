# Git Superpowers - Quick Reference Card
## Nick Zavlagkas | Agile Actors | Friday Workshop

---

## THE 6 GIT SUPERPOWERS (At a Glance)

### 1. Git Reflog — Absolute Recovery
```bash
git reflog                    # See all HEAD movements
git reset --hard <commit>    # Recover "lost" commits
# WHEN: You deleted a commit or reset hard
# SAFETY: Always recovers anything committed
```

### 2. Detached HEAD — Safe Exploration
```bash
git checkout <old_commit>    # Enter detached HEAD
git checkout -b new-branch   # Save work as branch
git checkout main            # Or discard and return
# WHEN: Want to explore old code without risk
# SAFETY: Can always go back to main
```

### 3. Reset vs Revert vs Checkout — The Decision Matrix

| Tool | Use Case | Safety | History |
|------|----------|--------|---------|
| **reset** | Undo commits locally | Local only | Rewrites history |
| **revert** | Undo commits on shared branch | Shared safe | Adds new commit |
| **checkout** | Discard uncommitted changes | File level | No history |

### 4. Branches Are Cheap — Fearless Experimentation
```bash
git checkout -b experiment         # Create branch
git branch -D experiment           # Delete (commits in reflog)
# WHEN: Any new idea, any experiment
# SAFETY: Delete guilt-free, commits persist
```

### 5. Stash — The Panic Button
```bash
git stash                    # Save uncommitted work
git stash pop               # Restore it later
# WHEN: Emergency context switch mid-work
# SAFETY: Work is preserved, can restore anytime
```

### 6. Cherry-pick — Surgical Recovery
```bash
git cherry-pick <commit>    # Take one commit and apply here
# WHEN: One good commit is on the wrong branch
# SAFETY: Precise, intentional, non-destructive
```

---

## COMMANDS USED IN LIVE DEMOS

### Demo 1: Project Setup
```bash
mkdir git-superpowers && cd git-superpowers
git init
mkdir src && touch README.md
cat > src/Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
    }
}
EOF
git config user.name "Your Name"
git config user.email "your@email.com"
git add . && git commit -m "Initial commit"
```

### Demo 2: Reflog Recovery
```bash
echo "New feature" > src/Main.java && git add . && git commit -m "Feature"
git log --oneline                    # See the commit
git reset --hard HEAD~1              # "Delete" it
git reflog                           # Find it
git reset --hard abc1234             # Recover it
git log --oneline                    # It's back!
```

### Demo 3: Detached HEAD
```bash
git checkout abc1234                 # Enter detached HEAD
echo "BREAK" > src/Main.java
git add . && git commit -m "Experiment"
git checkout -b experiment-branch    # Save as branch
git checkout main                    # Or return clean
```

### Demo 4: Reset/Revert/Checkout
```bash
# Reset approach
git reset --hard HEAD~1

# Revert approach
git revert HEAD

# Checkout approach (unstaged files only)
git checkout src/Main.java
```

### Demo 5: Branches
```bash
git checkout -b branch1 && git checkout -b branch2 && git checkout -b branch3
echo "CHAOS" > src/Main.java && git add . && git commit -m "Chaos"
git checkout main
git branch -D branch3
git reflog                # Commits still there!
```

### Demo 6: Stash & Cherry-pick
```bash
# Stash
echo "WIP" > src/Main.java && git stash
git stash pop

# Cherry-pick
git cherry-pick abc1234
```

---

## TERMINAL TIPS FOR PRESENTING

### Before You Start
```bash
# Test font size (should see clearly from 20 feet away)
# Cmd+Plus or Ctrl+Plus to increase

# Use professional color scheme
# Recommended: Dracula, Solarized Dark, or Nord

# Clear before each demo
clear

# Useful aliases to add
alias glog="git log --oneline --graph --all --decorate"
alias gstatus="git status --short"
```

### During Demos
```bash
# Always show output after commands
git status                    # Show what changed
git log --oneline            # Show current history
git reflog                    # Show all HEAD movements

# Use these for clarity
git show <commit>            # Show commit details
git diff HEAD~1              # Show changes
git branch -v                # Show branches
```

---

## KEY MESSAGES TO REPEAT

**Slide 1-3:**
> "Git is a time machine, not a scary tool. Snapshots are immutable. Nothing is ever lost."

**Slide 6-7 (Reflog Demo - CRITICAL):**
> "Even when you think you deleted it... it's in reflog. Always. Nothing is ever truly lost."

**Slide 8-9:**
> "Detached HEAD is not dangerous. It's a playground. You can break everything safely."

**Slide 12:**
> "Branches are free. Cost is nothing. Delete without guilt. Commits persist in reflog."

**Slide 15:**
> "You can break your own house. You cannot break your teammate's house. Local branches: yours. Shared branches: careful."

**Slide 16 (Emotional Closing):**
> "Git doesn't punish mistakes. It records them so you can undo them. You control Git now."

---

## AUDIENCE PSYCHOLOGY

### The Fear Journey
1. **Entry:** "I might break things forever"
2. **Mental Model:** "Actually, Git is a safety net"
3. **Reflog Demo:** "Wait... I really can't lose anything?"
4. **Superpowers:** "I have 6 tools to fix problems"
5. **Exit:** "I'm leaving confident. I can experiment fearlessly"

### Confidence Statements (Use Often)
- "This is version control. Control is the keyword."
- "Git is forgiving. I'm about to prove it."
- "If it's committed, it's recoverable. Period."
- "Mistakes are learning opportunities, not failures."
- "You cannot break anything that matters."

---

## TROUBLESHOOTING IN 30 SECONDS

| Problem | Solution |
|---------|----------|
| Git not installed | `brew install git` (macOS) or `sudo apt-get install git` (Linux) |
| Java not installed | Not required for Git demos |
| Terminal text too small | Cmd/Ctrl + Plus multiple times |
| Reflog shows nothing | Make a few commits first, then check |
| Command didn't work | Check you're in the right directory: `pwd` |
| Audience can't see text | Move terminal to center, increase font size |
| "What about X?" | "Great question. That's advanced. Today we focus on core safety." |
| You make a mistake | "Perfect teaching moment!" Use git reflog to recover |

---

## TIMING GUIDE

- **5 min:** Title + Mental Model (Slides 1-3)
- **2 min:** Project Setup (Slide 4)
- **2 min:** Debunk Myths (Slide 5)
- **7 min:** Reflog Demo (Slides 6-7) ← KEY
- **6 min:** Detached HEAD (Slides 8-9)
- **8 min:** Reset/Revert/Checkout (Slides 10-11)
- **5 min:** Branches (Slide 12)
- **4 min:** Stash & Cherry-pick (Slides 13-14)
- **3 min:** Professional Rules (Slide 15)
- **2 min:** Emotional Closure (Slide 16)
- **15 min:** Q&A (Slide 17)

**Total: ~60 minutes**

---

## PRESENTATION CHECKLIST

### Before You Present
- [ ] Presentation HTML file ready in browser (fullscreen capable)
- [ ] Terminal font size tested (visible from back of room)
- [ ] All 6 demo projects created and tested
- [ ] git-superpowers project initialized
- [ ] Speaker notes reviewed or printed
- [ ] Agile Actors logo/branding ready
- [ ] You've run through all demos once
- [ ] Confidence level: HIGH

### During Presentation
- [ ] Smile and make eye contact
- [ ] Speak slowly
- [ ] Pause after key concepts
- [ ] Show git output after every command
- [ ] Use confidence statements
- [ ] Repeat safety message
- [ ] Stay calm if something breaks
- [ ] Ask "Questions?" frequently

---

## ONE-PAGE MENTAL MODEL

```
Git is a TIME MACHINE with REFLOG safety net

Snapshots:   Each commit = complete project state (immutable)
Branches:    Cheap pointers to commits (free to create/delete)
HEAD:        Your current location (moves freely)
Reflog:      Record of every HEAD movement (your backup)

The Safety Guarantee:
If you committed it → It's in reflog forever → You can always recover it

The Professional Rule:
Local branches = Yours (reset, rebase OK)
Shared branches = Everyone's (use revert, not reset)

The Confidence Payoff:
You can experiment fearlessly because Git always lets you undo.
Nothing is ever truly lost.
You control Git. Not the other way around.
```

---

## SUCCESS INDICATORS

You'll know the workshop worked when attendees say:
- "I can't break anything anymore"
- "I was way more afraid than I needed to be"
- "I'm leaving feeling confident about Git"
- "That reflog demo changed how I think about Git"
- "Can we do more advanced Git next?"

---

## QUICK LINKS

**File References:**
1. `git_superpowers.html` — Full presentation (open in browser)
2. `git_superpowers_setup.md` — Pre-workshop preparation
3. `git_delivery_guide.md` — Complete delivery script
4. `git_advanced_tips.md` — Troubleshooting & advanced tips
5. `THIS FILE` — Quick reference card

---

**You've got everything you need.**

**Trust your preparation. Trust your expertise. Trust that removing fear from a room is powerful work.**

**Let's make Git fearless. — Nick Zavlagkas, Agile Actors**

---

*Print this card. Keep it handy. Reference during Q&A if needed.*
*But mostly? You don't need it. You've got this.*
