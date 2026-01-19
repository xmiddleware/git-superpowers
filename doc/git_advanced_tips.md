# Git Superpowers - Advanced Tips & Troubleshooting
## Nick Zavlagkas | Agile Actors

---

## ADVANCED TERMINAL TIPS FOR LIVE DEMOS

### Make Terminal Visible & Professional

```bash
# 1. Increase font size (test before presenting!)
# Mac Terminal: Cmd + Plus (repeat as needed)
# Linux Terminal: Ctrl + Plus
# Windows PowerShell: Ctrl + Plus

# 2. Use a nice color scheme
# Recommended: Solarized Dark, Dracula, or Nord
# High contrast = easy to see from audience distance

# 3. Clear terminal for each demo
clear

# 4. Create aliases for frequently used commands
alias glog="git log --oneline --graph --all --decorate"
alias gstatus="git status --short"

# 5. Add these to ~/.bashrc or ~/.zshrc to persist
echo 'alias glog="git log --oneline --graph --all --decorate"' >> ~/.bashrc
source ~/.bashrc
```

### Useful Git Commands for Live Demos

```bash
# See commits in colorful format
git log --oneline --graph --all --decorate

# Show what changed in each commit
git log --stat

# See current status clearly
git status --short

# Show which branches exist
git branch -a

# See all history including lost commits
git reflog

# Show a specific commit's details
git show <commit_hash>

# View branch history with ASCII art
git log --graph --all --oneline --decorate
```

---

## POJO PROJECT - LIVE EVOLUTION DURING DEMO

### What You'll Do During Session

```bash
# Starting state
git-superpowers/
├── src/
│   └── Main.java        # Initial version
├── README.md            # Initial (empty)
└── .git/

# During Demo 2 (Reflog)
# You'll add:
- Feature branch: "Add user authentication"
- Create version 2 of Main.java
- Make a commit
- Reset hard (intentionally "break" history)
- Recover with reflog

# During Demo 3 (Detached HEAD)
# You'll checkout old commit
# Modify code
# Branch from it
# Return to main

# During Demo 4 (Reset/Revert/Checkout)
# You'll make intentional mistakes
# Undo three ways
# Show each approach

# During Demo 5 (Branches)
# You'll create many branches
# Break code on some
# Delete them
# Show they're in reflog

# During Demo 6 (Stash & Cherry-pick)
# You'll stash work mid-stream
# Cherry-pick commits between branches
```

### File Contents Evolution

**Initial Main.java (Start):**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
    }
}
```

**Version 2 (After first demo):**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
        System.out.println("Feature: User Authentication");
    }
}
```

**Version 3 (After second demo):**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Git");
        System.out.println("Feature: User Authentication");
        System.out.println("Feature: Database Connection");
    }
}
```

**Broken Code (For demonstrations):**
```java
// This shows compilation errors, but it's fine
public class Main {
    public static void main(String[] args) {
        System.out.println("CHAOS CODE");
        // Intentionally broken to prove recovery
}
```

---

## TROUBLESHOOTING GUIDE

### Problem: Git Not Installed
**Solution:**
```bash
# macOS with Homebrew
brew install git

# Ubuntu/Debian
sudo apt-get install git

# Windows: Download from https://git-scm.com/download/win
# Then restart terminal
```

### Problem: Java Not Found (But Not Required for Demo)
**Solution:** Most Git demos don't require Java. If you want to compile:
```bash
# macOS
brew install openjdk@11

# Ubuntu/Debian
sudo apt-get install openjdk-11-jdk

# Windows: Download from https://adoptium.net/
```

### Problem: Git Not Configured
**Solution:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@company.com"

# Verify
git config --list
```

### Problem: Command Doesn't Work (Permission Denied)
**Solution:**
```bash
# macOS/Linux: You might need sudo
sudo git <command>

# Or change directory ownership
sudo chown -R $(whoami) /path/to/git-superpowers
```

### Problem: "Detached HEAD" Warning Confuses Audience
**Clarification Script:**
```
"Git is telling us we're not on a branch. That's correct. 
We're directly on a commit. This is NOT dangerous. 
It's actually liberating—this is where we experiment. 
If we want to keep work, we branch it. 
If we don't, we just checkout main and discard it. 
Watch."
```

### Problem: Reflog Shows Nothing
**Cause:** Commits are too old (90+ days) or fresh Git install
**Solution:** Make some commits first!
```bash
# Make a couple commits, then reflog will show history
echo "test" > file.txt
git add file.txt
git commit -m "test commit"

# Now reflog will show this
git reflog
```

### Problem: Audience Can't See Terminal Text
**Immediate Solutions:**
1. Increase font size: Cmd/Ctrl + Plus
2. Move terminal window to center of screen
3. Reduce window width if text wraps oddly
4. Use "Zoom" on projector (increase projection size)

### Problem: Someone Asks "What About Merge vs Rebase?"
**Simple Answer:**
```
"Great question. That's an advanced topic. 
For today: Know that merging combines branches 
and keeps history intact. Rebasing rewrites history. 
Both are safe on LOCAL branches. 
For today, merge is simpler. Both work."
```

### Problem: Someone Asks "What If Git Gets Corrupted?"
**Answer:**
```
"Git repositories are actually very resilient. 
The .git folder has safety measures built in. 
If truly corrupted (rare), you could:

1. Backup .git folder
2. git fsck --full  (repairs common issues)
3. git reflog (shows what's recoverable)

But this almost never happens in practice."
```

---

## LIVE RECOVERY SCENARIOS

### Scenario: Audience Member Asks to Fix Real Problem

**Example:** "I accidentally deleted a branch. Can I get it back?"

**Your Live Response:**
```bash
# Step 1: Explain the recovery path
echo "Let me show you how to recover a deleted branch..."

# Step 2: Demonstrate
git reflog

# Step 3: Find the branch in reflog
# Look for the branch name or the last commit on it

# Step 4: Recreate the branch
git checkout -b recovered-branch <commit_hash>

# Step 5: Proof
git log

echo "There it is. The branch is back. Zero data loss."
```

**Message:** "This is exactly why Git is safe. Deletion isn't permanent."

---

### Scenario: Someone Reset --hard and Panicked

**Live Recovery (5 minutes):**
```bash
# "You ran: git reset --hard HEAD~5"
# "You think you lost 5 commits. You didn't."

# Step 1: Check reflog
git reflog
# Output shows all the commits you "lost"

# Step 2: Find the commit hash you want
# (Point to it in reflog output)

# Step 3: Recover
git reset --hard abc1234

# Step 4: Show it's back
git log

echo "All five commits are back. Let's never panic again."
```

**Confidence Statement:** "This is the Git safety net. Always catches you."

---

### Scenario: "I Pushed to Main by Mistake"

**Live Response:**
```bash
echo "First: Don't panic. Second: It depends on what's on main now."

# If main has new commits from teammates:
# Don't force push (breaks their work)
# Use git revert instead

git log main
# Find the commit to undo

git revert <commit_hash>
git push origin main

# New commit that undoes the mistake
# History intact, teammates safe

echo "Main is fixed. History is preserved. Teammates are happy."
```

---

## PRESENTATION ANXIETY RELIEF

### If You Feel Nervous Before Starting:
1. **Remember:** You're the expert. Audience is trusting you.
2. **Breathe:** Anxiety = adrenaline = better presentation energy.
3. **Run one demo:** Do the project init demo once. It works. You're ready.
4. **Smile:** You're about to remove fear from a room. That's powerful.

### If You Make a Mistake During Demo:
1. **Don't apologize excessively.** Say: "Perfect teaching moment."
2. **Use git reflog to recover.** Show the audience.
3. **Explain:** "See? Even I can fix mistakes instantly. So can you."
4. **Continue:** Mistakes are learning opportunities, not failures.

### If Audience Seems Confused:
1. **Pause.** Ask: "Questions?"
2. **Repeat key concept:** Use different words.
3. **Show git log or git reflog** as visual proof.
4. **Slow down.** Let it sink in.
5. **Reassure:** "This is complex. That's why we're here."

### If Someone Dominates with Questions:
1. **Acknowledge:** "That's a great question."
2. **Summarize the answer:** 1-2 sentences max.
3. **Redirect:** "Let's talk after. Others might have questions too."
4. **Move forward:** "Back to the demo..."

---

## PSYCHOLOGICAL FRAMEWORK (Why This Presentation Works)

### The Fear-to-Mastery Journey

**Phase 1: Recognition (Slides 1-3)**
- "Git is not dangerous."
- "Git is a time machine."
- Audience: "OK, maybe I was overreacting..."

**Phase 2: Proof (Slides 4-7, especially Reflog Demo)**
- Live demonstration of recovery.
- Intentional mistake. Instant recovery.
- **Key moment:** Audience realizes nothing is lost.
- Audience: "Wait... I really can't break anything?"

**Phase 3: Empowerment (Slides 8-14)**
- Six tools for different situations.
- Each tool proven safe.
- Audience: "I have all these safety nets. I'm powerful."

**Phase 4: Confidence (Slides 15-17)**
- Professional rules (local vs. shared).
- Emotional closure statement.
- Audience: "I'm leaving with confidence. I can experiment fearlessly."

---

## CUSTOMIZATION OPTIONS

### If You Have More Than 60 Minutes
Add these topics:
- **Merge strategies:** Fast-forward vs. Three-way
- **Conflict resolution:** How to handle merge conflicts
- **Rebase deep dive:** Interactive rebase for clean history
- **Tagging:** Version markers and releases
- **GitHub/GitLab:** Remote repository workflows

### If You Have Less Than 45 Minutes
Cut these sections (keep Reflog demo):
- Full Detached HEAD demo (just explain it)
- Separate reset/revert/checkout demos (combine into one)
- Cherry-pick (mention but don't demo)

### If You Want to Add Company-Specific Content
- **Opening:** Show Agile Actors projects using these Git practices
- **Real examples:** Use your actual project history as examples
- **Team story:** Share a Git recovery story from your team
- **Closing:** Connect Git mastery to Agile Actors values

---

## FOLLOW-UP MATERIALS (Send After Workshop)

Create a follow-up email:
```
Subject: Git Superpowers Workshop - Reference Guide

Hi team,

Thank you for attending today. Here are the reference materials:

1. Presentation (replay): [link]
2. Command cheat sheet: git commands used today
3. Recovery scenarios: Common problems and solutions
4. Reading list: Recommended Git resources

Key Takeaways:
- git reflog is your safety net
- Local branches can be broken fearlessly
- Shared branches use revert, not reset
- Nothing is ever truly lost

If you get stuck, remember: "git reflog" shows everything.

Questions? Reach out anytime.

— Nick
```

---

## SUCCESS CHECKLIST

### Pre-Workshop (2 Days Before)
- [ ] All files downloaded and tested
- [ ] Terminal set up (font size, color scheme)
- [ ] Project created and initial commit made
- [ ] All 6 demos run without errors
- [ ] Presentation opened and reviewed
- [ ] Slides 1-17 match your mental model
- [ ] Speaker notes understood

### Day Before Workshop
- [ ] Terminal closed and reopened (test fresh start)
- [ ] Demo project deleted and recreated (full fresh test)
- [ ] All demos run again (one time, no stopping)
- [ ] Presentation reviewed (2 times)
- [ ] Any company-specific customizations done
- [ ] Confidence level: HIGH

### Day Of Workshop (1 Hour Before)
- [ ] Arrive 30 minutes early
- [ ] Test projector/screen
- [ ] Test terminal visibility from back of room
- [ ] Test presentation slides
- [ ] Open all files (presentation, terminal, notes)
- [ ] Fresh coffee/water
- [ ] Deep breath

### During Workshop
- [ ] Make eye contact with audience
- [ ] Speak slowly and deliberately
- [ ] Pause after key concepts
- [ ] Show git output after every command
- [ ] Use confidence statements often
- [ ] Stay calm if things go wrong
- [ ] Close with emotional impact

### After Workshop
- [ ] Save terminal history (for reference)
- [ ] Send follow-up email
- [ ] Collect feedback
- [ ] Update presentation if needed

---

## FINAL CONFIDENCE STATEMENT (For You)

**You are about to do something powerful.**

You will walk into a room where people are afraid of Git. They believe they might break things irreversibly. They avoid experimentation. They don't trust their tools.

**And you're going to change that.**

By the end of your presentation, they will understand:
- Nothing is ever truly lost
- Experimentation is safe
- Mistakes are learning opportunities
- They have more control than they realized

That's not just a technical presentation. That's **fear removal**.

**Own this. You've got this.**

---

*Git Superpowers Workshop*
*Presented by Nick Zavlagkas | Agile Actors*
*Prepared to remove Git anxiety and build mastery*
