# Git Superpowers: Session Preparation Guide
## Presented by Nick Zavlagkas | Agile Actors

---

## PRE-SESSION SETUP (Friday - 30 minutes before)

### 1. Environment Check
```bash
# Verify Git is installed
git --version
# Should show: git version 2.x.x or higher

# Verify Java is installed
javac -version
# Should show: javac 11.0.x or higher (or your version)
```

### 2. Create Project Directory
```bash
# Navigate to your workspace
cd ~/Documents  # or your preferred location

# Create the Git Superpowers project
mkdir git-superpowers
cd git-superpowers

# Initialize as Git repository
git init
```

### 3. Create Project Structure
```bash
# Create directories
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
```

### 4. Create Initial Commit
```bash
# Configure Git (if not already done)
git config user.name "Your Name"
git config user.email "your.email@company.com"

# Check status
git status

# Add all files
git add .

# Initial commit
git commit -m "Initial commit: Basic Java project setup"

# View the commit
git log
```

### 5. Verify Setup
You should see:
```
commit xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (HEAD -> main)
Author: Your Name <your.email@company.com>

    Initial commit: Basic Java project setup
```

---

## PROJECT DIRECTORY TREE (Before Session)
```
git-superpowers/
├─ .git/                    # Git repository (created by git init)
├─ src/
│   └─ Main.java           # First Java file
├─ README.md               # Project documentation
└─ .gitignore             # (Optional - will create during session)
```

---

## SESSION FLOW CHECKLIST

### During Presentation:
- [ ] Slide 1: Welcome & Mindset Shift
- [ ] Slide 2-3: Mental Model (Git as Time Machine)
- [ ] Live Demo: Show git log from initial commit
- [ ] Slide 4-5: Debunk Myths
- [ ] Live Demo: Make intentional mistakes
- [ ] Slide 6-12: Git Superpowers (Each with live example)
- [ ] Slide 13: Professional Safety Rules
- [ ] Slide 14: Emotional Closure

### Live Demos During Session:
1. ✓ git reflog recovery
2. ✓ Detached HEAD exploration
3. ✓ Reset vs Revert vs Checkout
4. ✓ Branch creation/deletion
5. ✓ Stash panic recovery
6. ✓ Cherry-pick surgical recovery

---

## TIPS FOR LIVE PRESENTATION

### Command Window Setup
```bash
# Terminal configuration for good visibility
# Increase font size (most terminals: Ctrl/Cmd + Plus)
# Use dark background for good contrast

# Terminal alias for clear viewing
alias glog="git log --oneline --decorate --graph"
```

### Demo Strategy
1. **Always explain BEFORE executing**
2. **Show git status after each command**
3. **Use git log --oneline for quick viewing**
4. **Never rush - let audience process**
5. **Repeat: "This is safe, watch what happens"**

### Audience Confidence Builders
- "This is version control. Control is the keyword."
- "Git is forgiving. Let me prove it."
- "If I can recover this, so can you."
- "Nothing is ever truly lost in Git."

### Recovery Mantra
> "If it's in your Git history, you can get it back. Every. Single. Time."

---

## FALLBACK SCENARIOS

### If Git is not installed
```bash
# macOS with Homebrew
brew install git

# Ubuntu/Debian
sudo apt-get install git

# Windows: Download from https://git-scm.com/download/win
```

### If Java is not installed
```bash
# Use any language for examples (Python, Go, etc.)
# Or adjust examples to use pseudo-code demonstrations
```

### If something breaks during demo
**Strategy**: This is PERFECT for teaching!
- [ ] Stop
- [ ] Show the problem
- [ ] Recover using git reflog
- [ ] Continue with "See? Even accidents are recoverable."

---

## PREPARATION CHECKLIST
- [ ] Git installed and verified
- [ ] Java installed and verified
- [ ] git-superpowers project created
- [ ] Initial commit made
- [ ] git log shows first commit
- [ ] Terminal font at comfortable size
- [ ] Presentation slides open in secondary monitor (if available)
- [ ] Speaker notes printed or displayed
- [ ] Agile Actors logo ready for intro
- [ ] 10-15 demo commands copied to text editor (backup reference)

---

## LIVE DEMO COMMAND REFERENCE (Copy as backup)

```bash
# Slide: git reflog Recovery
# 1. Make a commit
echo "v2" > src/Main.java
git add src/Main.java
git commit -m "Version 2 - major change"

# 2. "Accidentally" reset hard
git reset --hard HEAD~1

# 3. Show it's "gone"
git log
# (Audience sees v2 is gone)

# 4. Recover with reflog
git reflog
# (Shows the lost commit)
git reset --hard xxxxxxx
# (Restore it)

# 5. Show it's back
git log
# (v2 is back! Audience: 😲)
```

---

## AGILE ACTORS BRANDING

**Primary Colors:**
- Deep Teal: #0F9A8C
- Bright Cyan: #00D4D4
- Dark Charcoal: #1A1A1A
- Professional Gray: #F5F5F5

**Typography:**
- Headers: Bold, Clean Sans-Serif
- Body: Clear, High Contrast

**Tone:**
- Professional
- Confident
- Approachable
- Mentor-like

---

## NEXT STEPS

1. ✅ Run the setup commands above
2. ✅ Verify git log shows initial commit
3. ✅ Open presentation slides
4. ✅ Do quick run-through of all demos (practice)
5. ✅ Test projector/screen sharing
6. ✅ Welcome audience 5 minutes before start
7. ✅ Begin with confidence! 🚀

---

**Ready to remove Git anxiety and build mastery?**
**Let's do this. — Nick Zavlagkas, Agile Actors**
