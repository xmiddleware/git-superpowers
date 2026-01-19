# Git Superpowers Workshop - Visual Guide & Flow
## Nick Zavlagkas | Agile Actors

---

## PRESENTATION FLOW (Visual Overview)

```
┌─────────────────────────────────────────────────────────────┐
│  SLIDE 1: TITLE & WELCOME                                  │
│  🎯 Set tone: Calm, confident, mentor-like                │
│  Message: "This is a confidence journey"                   │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  SLIDES 2-3: MENTAL MODEL (5 min)                          │
│  🎯 Reframe Git as time machine                            │
│  ✓ Snapshots (immutable)                                   │
│  ✓ Branches (cheap pointers)                               │
│  ✓ HEAD (your location)                                    │
│  ✓ Reflog (your safety net)                                │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  DEMO 1: PROJECT SETUP (2 min)                             │
│  🎯 Create POJO project live                               │
│  ✓ mkdir, git init, Main.java                              │
│  ✓ git config, git add, git commit                         │
│  ✓ Show git log → snapshot exists forever                  │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  SLIDE 5: DEBUNK MYTHS (2 min)                             │
│  🎯 Prove fear is unjustified                              │
│  ✗ Reset deletes work? NO—git reflog recovers it          │
│  ✗ Rebase destroys history? NO—old commits in reflog      │
│  ✗ Detached HEAD is unsafe? NO—it's a playground          │
│  ✗ Force push is evil? NO—just not on shared branches     │
└─────────────────────────────────────────────────────────────┘
                            ↓
     ╔═════════════════════════════════════════════════════╗
     ║  ⭐ DEMO 2: REFLOG RECOVERY (7 min) ⭐              ║
     ║  🎯 THE KEY MOMENT - Fear dies here               ║
     ║  ✓ Make a commit                                   ║
     ║  ✓ Reset --hard (seems to delete it)              ║
     ║  ✓ Check git log (it's "gone")                    ║
     ║  ✓ Check git reflog (it's still there!)          ║
     ║  ✓ Recover with reset --hard (it's back!)         ║
     ║  MESSAGE: "Nothing is ever truly lost"            ║
     ╚═════════════════════════════════════════════════════╝
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  DEMO 3: DETACHED HEAD (6 min)                             │
│  🎯 Safe exploration playground                           │
│  ✓ Checkout old commit                                    │
│  ✓ Modify code (break it intentionally)                   │
│  ✓ Create branch to save (or discard)                     │
│  ✓ Return to main—zero damage                            │
│  MESSAGE: "This is where you experiment fearlessly"       │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  DEMO 4: RESET vs REVERT vs CHECKOUT (8 min)              │
│  🎯 Decision matrix for recovery                          │
│  ✓ RESET: Local history rewriting (local only)           │
│  ✓ REVERT: Create undo commit (shared safe)              │
│  ✓ CHECKOUT: Discard file changes (unstaged)             │
│  MESSAGE: "Three tools, three contexts"                  │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  DEMO 5: BRANCHES ARE CHEAP (5 min)                       │
│  🎯 Free to create, free to delete                        │
│  ✓ Create many branches                                   │
│  ✓ Break code intentionally                               │
│  ✓ Delete branches guilt-free                             │
│  ✓ Commits still in reflog                                │
│  MESSAGE: "Branches enable fearless experimentation"      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  DEMO 6: STASH & CHERRY-PICK (4 min)                      │
│  🎯 Flexibility and precision tools                        │
│  ✓ Stash: Save uncommitted work temporarily              │
│  ✓ Cherry-pick: Take specific commit elsewhere            │
│  MESSAGE: "Stash = panic button. Cherry-pick = surgeon"   │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  SLIDE 15: PROFESSIONAL RULES (3 min)                     │
│  🎯 When to be bold, when to be careful                   │
│  ✓ LOCAL branches: reset, rebase, force push OK          │
│  ✓ SHARED branches: use revert, NOT reset                │
│  MESSAGE: "You can break your house. Not teammate's."    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  SLIDE 16: EMOTIONAL CLOSURE (2 min)                      │
│  🎯 Leave with confidence and mastery                     │
│  ✓ List all superpowers and what each enables            │
│  ✓ Final message: "You control Git now"                  │
│  CLOSE: "Nothing is ever truly lost"                      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  SLIDE 17: Q&A (15 min)                                    │
│  🎯 Open discussion, real-time problem solving            │
│  ✓ Answer questions with git demonstrations               │
│  ✓ Reinforce learning through real scenarios              │
└─────────────────────────────────────────────────────────────┘

TOTAL TIME: ~60 minutes (including breathing room)
```

---

## EMOTIONAL ARC (The Psychology)

```
      CONFIDENCE
      MASTERY        ╱─────────────────────╲
                    ╱                       ╲
                   ╱                         ╲  SLIDE 16-17
                  ╱    DEMOS 2-6             ╲  Emotional
                 ╱  (Superpowers)            ╲ Closure
                ╱                             ╲
    REALIZATION ╱                              ╲
               ╱  DEMO 2: REFLOG               ╲
              ╱  (Fear dies here)                ╲
             ╱  ⭐ KEY MOMENT ⭐
            ╱
           ╱
          ╱
        ╱     SLIDE 1-3
       ╱     Mental Model    SLIDE 5
      ╱      Introduction    Myths
     FEAR ←─────────────────────
    ANXIETY     RECOGNITION

Entry: Scared of Git
|
Turns: "Maybe Git isn't that scary"
|
Breaks: REFLOG DEMO - "Oh. I can't break anything?"
|
Grows: Six tools, each empowering
|
Leaves: "I control Git. I'm confident."

```

---

## COMMAND FLOW DIAGRAM

```
┌──────────────────────────────────────────────────────────────┐
│                    GIT SUPERPOWERS JOURNEY                   │
└──────────────────────────────────────────────────────────────┘

DEMO 1: Setup
├── git init
├── git config
├── git add .
├── git commit
└── git log ─→ "Snapshot exists forever"

DEMO 2: Reflog ⭐
├── Modify + commit "feature"
├── git log ─→ "See the commit"
├── git reset --hard HEAD~1 ─→ "Delete it"
├── git log ─→ "It's gone"
├── git reflog ─→ "It's still there!"
└── git reset --hard <hash> ─→ "RECOVERED!"

DEMO 3: Detached HEAD
├── git checkout <old_hash>
├── [Modify code]
├── git add . && git commit
├── git checkout -b branch ─→ "Save work"
└── git checkout main ─→ "Or discard"

DEMO 4: Recovery Strategies
├── Approach A: git reset --hard
├── Approach B: git revert
└── Approach C: git checkout [file]

DEMO 5: Branches
├── git checkout -b exp1
├── git checkout -b exp2
├── git checkout -b exp3
├── [Break code] → git add . && git commit
├── git checkout main
├── git branch -D exp3
└── git reflog ─→ "Commits preserved"

DEMO 6: Advanced Tools
├── git stash ─→ "Save work"
├── [Context switch]
├── git stash pop ─→ "Restore work"
├── git cherry-pick <hash> ─→ "Selective recovery"
└── git log ─→ "Commit now here"

```

---

## SLIDES BY COLOR (Agile Actors Branding)

```
TITLE SLIDES (Dark Teal Gradient)
├── Slide 1: Welcome
├── Slide 6-7: Reflog (CRITICAL)
├── Slide 16: Emotional Closure

CONTENT SLIDES (Bright Cyan Gradient)
├── Slide 2-3: Mental Model
├── Slide 8-9: Detached HEAD
├── Slide 13-14: Stash & Cherry-pick

MIXED SLIDES (Light Gray)
├── Slide 4: Project Setup
├── Slide 10-11: Reset/Revert/Checkout
├── Slide 15: Professional Rules

DARK CHARCOAL (Professional)
├── Slide 5: Myth Debunking
├── Slide 12: Branches

Q&A SLIDE (Closing)
└── Slide 17: Open Discussion

```

---

## SPEAKER ENERGY LEVELS

```
MINUTES  │ CONTENT              │ YOUR ENERGY LEVEL
─────────┼──────────────────────┼──────────────────
0-2      │ Welcome              │ HIGH - Set tone
2-5      │ Mental Model         │ MEDIUM - Explain
5-7      │ Project Setup Demo   │ HIGH - Show live
7-9      │ Myth Debunking       │ MEDIUM - Assert
─────────┼──────────────────────┼──────────────────
9-16 ⭐  │ REFLOG DEMO (KEY!)   │ VERY HIGH - Drama
16-22    │ Detached HEAD        │ HIGH - Prove safety
22-30    │ Reset/Revert/Chk     │ MEDIUM - Explain
30-35    │ Branches             │ HIGH - Demonstrate
35-39    │ Stash/Cherry-pick    │ MEDIUM - Show
─────────┼──────────────────────┼──────────────────
39-42    │ Professional Rules   │ CALM - Teach rules
42-44    │ Emotional Closure    │ VERY HIGH - Inspire
44-60    │ Q&A Discussion       │ HIGH - Engage

KEY: High energy for demos, medium for explanation,
     Very high for emotional moments
```

---

## SLIDE TEMPLATE (Visual Layout)

```
┌─────────────────────────────────────────────────────────────┐
│  AGILE ACTORS LOGO (top right)                             │
│                                                             │
│                        Slide Title                          │
│                    ═════════════════════                     │
│                                                             │
│                    Main Content Here                        │
│                  (Bullet points or demo)                    │
│                                                             │
│                                                             │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ SPEAKER NOTE (at bottom):                             │ │
│  │ What to say, when to say it, key points              │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                             │
│  [Slide Counter: X/17]  [Navigation Buttons]               │
└─────────────────────────────────────────────────────────────┘
```

---

## DEMO SETUP CHECKLIST

```
Before Each Demo:

REFLOG DEMO (Demo 2)
├── [ ] Terminal visible to audience
├── [ ] git log clear for before/after
├── [ ] git reflog ready to show
├── [ ] Speak slowly through each step
└── [ ] Watch audience faces

DETACHED HEAD DEMO (Demo 3)
├── [ ] Explain what's happening BEFORE executing
├── [ ] Show branch creation
├── [ ] Return to main successfully
└── [ ] Clarify: "Not dangerous, it's a playground"

RESET/REVERT/CHECKOUT DEMO (Demo 4)
├── [ ] Three separate approaches for SAME problem
├── [ ] Show output after each
├── [ ] Explain when each is appropriate
└── [ ] Emphasize: "Local vs. Shared"

BRANCHES DEMO (Demo 5)
├── [ ] Create multiple branches visibly
├── [ ] Break code on one branch
├── [ ] Show deletion
├── [ ] Check reflog for persistence
└── [ ] Message: "Cost = nothing, value = freedom"

STASH & CHERRY-PICK DEMO (Demo 6)
├── [ ] Stash mid-work scenario (realistic)
├── [ ] Pop it back
├── [ ] Cherry-pick another commit
└── [ ] Show final state with both tools used

```

---

## AUDIENCE RESPONSE INDICATORS

```
✅ YOU'RE DOING GREAT WHEN:

SILENCE → Audience is absorbing (don't interrupt)
HEADS NODDING → Concepts are landing
EYES WIDE DURING REFLOG → Fear is leaving
QUESTIONS ASKED → They're engaging
SMILES → They're connecting
NOTE-TAKING → They value the content
HANDS UP → Confidence to ask questions

⚠️  ADJUST IF YOU SEE:

CONFUSION → Pause, repeat with different words
CHECKING PHONES → Slow down, vary pace
BLANK STARES → Too fast or not clear
NO ONE TAKING NOTES → Not emphasizing key points
NERVOUS QUESTIONS → Need more reassurance
SKEPTICAL LOOKS → Need more proof (show more demos)

```

---

## RECOVERY PROTOCOLS

```
If Demo Breaks:

1. STOP
2. Say: "Perfect teaching moment"
3. Use git reflog to fix it
4. Say: "See? Even mistakes recover instantly"
5. CONTINUE

If Audience Seems Lost:

1. PAUSE
2. Ask: "Questions so far?"
3. Repeat key concept with NEW WORDS
4. Show git log as visual proof
5. MOVE FORWARD (don't get stuck)

If You Forget What's Next:

1. Look at git_quick_reference.md (on your phone)
2. Check presentation slide (it tells you)
3. Take a sip of water
4. Continue with confidence

If Wrong Demo Order:

1. Nothing breaks—demos are modular
2. Just finish the current one
3. Move to next slide
4. Recovery: "We can do these in any order"

```

---

## SUCCESS INDICATORS (Audience Knowledge)

```
THEY KNOW IT WORKED WHEN THEY CAN:

✓ Explain why git reflog is their safety net
✓ Use git reset --hard to recover commits
✓ Checkout an old commit without fear
✓ Choose between reset, revert, and checkout
✓ Create branches without hesitation
✓ Stash work mid-stream
✓ Cherry-pick specific commits
✓ Understand "safe on local, careful on shared"
✓ Leave confident, not scared

POST-WORKSHOP STATEMENTS YOU WANT TO HEAR:

"I can't break anything anymore"
"I was way more scared than I needed to be"
"Git makes so much more sense now"
"That reflog demo changed everything"
"I'm going to experiment with branching now"
"I feel actually confident about Git"
"Can we do advanced Git next?"

```

---

## FINAL VISUAL SUMMARY

```
╔════════════════════════════════════════════════════════════╗
║  GIT SUPERPOWERS: FEAR REMOVAL IN 60 MINUTES              ║
╠════════════════════════════════════════════════════════════╣
║                                                            ║
║  ENTRY MINDSET:        CORE MESSAGE:                       ║
║  "I might break Git"   "Nothing is ever lost"              ║
║  "I'm scared"          "You control Git"                   ║
║  "Mistakes are bad"    "Mistakes are learning"             ║
║                                                            ║
║  THE JOURNEY:                                              ║
║                                                            ║
║  Slides 1-5:   REFRAME (Git is not scary)                 ║
║  Demos 2-6:    PROVE (Watch me recover lost commits)      ║
║  Slides 15-17: EMPOWER (You know when to be bold)         ║
║                                                            ║
║  EXIT MINDSET:                                             ║
║  ✓ "I understand Git better"                              ║
║  ✓ "I can experiment fearlessly"                          ║
║  ✓ "I know how to recover anything"                       ║
║  ✓ "I'm confident about Git"                              ║
║                                                            ║
║  TRANSFORMATION: FEAR → MASTERY                           ║
║                                                            ║
╚════════════════════════════════════════════════════════════╝
```

---

**You are about to guide people from fear to confidence.**

**That's powerful. That matters.**

**You've got this. ✅**

---

*Git Superpowers Workshop*
*Nick Zavlagkas | Agile Actors*
*Friday Workshop — Remove Fear, Build Mastery*
