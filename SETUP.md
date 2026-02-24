# SETUP.md — Installing and Configuring voice-humanizer

A voice-calibrated writing editor for Claude Code. Two things the generic humanizer doesn't do:

1. Checks writing against *your specific voice*, not generic AI-pattern rules
2. Evaluates incoming comments for authenticity before you waste time on synthetic praise

---

## Install

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/dannwaneri/voice-humanizer.git ~/.claude/skills/voice-humanizer
```

Or manually:
```bash
mkdir -p ~/.claude/skills/voice-humanizer
cp SKILL.md ~/.claude/skills/voice-humanizer/
```

---

## Configure (Required)

The skill ships with someone else's writing corpus. You need to replace it with yours.

**Option A: Edit CORPUS.md directly**
```bash
cp CORPUS.example.md CORPUS.md
# Edit CORPUS.md — paste your writing, answer the five questions
```

**Option B: Start fresh**
```bash
echo "" > CORPUS.md
# Add your pieces manually
```

CORPUS.md is in `.gitignore` — it won't be pushed to GitHub if you fork this repo. Your writing stays private.

---

## Use

**Review a draft before publishing:**
```
/voice-humanizer

[paste your draft here]
```

**Evaluate a comment you received:**
```
/voice-humanizer comment

[paste the comment here]
```

**Check a reply you wrote before posting:**
```
/voice-humanizer check

[paste your reply here]
```

---

## What It Does

**For drafts:**
- Voice drift flags: sentences where you sound like Claude instead of yourself, with rewrites in your register
- Specificity audit: every unanchored claim flagged with required substitution
- AI pattern check: the standard 24 Wikipedia patterns, weighted below voice drift
- Comment stacking check: attribution lists that aren't building toward a point

**For incoming comments:**
- Authenticity score (0–3) based on: specific citation, personal experience, real question
- Synthetic praise detection: closing endorsement language, forward-looking corporate phrases
- Response length recommendation: full reply / one paragraph / one sentence / skip

**For your replies:**
- Three-step check: did you locate what's new, extend it, redirect?
- Voice drift flags: does this reply sound like you or like a helpful assistant?
- Tic detection: "appreciate the clarity," generic affirmations, attribution stacking

---

## How It's Different From the Generic Humanizer

The [humanizer by Siqi Chen](https://github.com/blader/humanizer) is excellent at catching generic AI tells. This skill does something different: it calibrates to *your* voice, not Wikipedia's list of AI patterns.

Generic humanizer: "Don't use 'testament to' or em dashes for emphasis"
This skill: "Here's where you sound like Claude instead of [you], and here's what [you] would do instead"

The 24 AI patterns are still checked — but as a second pass, weighted below voice-specific feedback. A pattern hit that appears in your corpus is fine. That's your voice. A pattern hit that doesn't appear in your corpus is Claude bleeding through.

---

## For People Who Clone This

This repo ships with CORPUS.md containing one author's writing. To use it for yourself:

1. Replace CORPUS.md with your own writing (see CORPUS.example.md for the format)
2. Answer the five calibration questions in CORPUS.example.md
3. The skill will derive your voice fingerprint from your corpus

Your CORPUS.md won't be pushed to GitHub (it's in `.gitignore`). The skill and structure are public. The corpus is private.

---

## Caveats

**The skill is only as good as the corpus.** If you give it 200 words of writing, the voice fingerprint will be weak. Three full articles is the minimum. Five is better.

**It won't catch everything.** Voice is harder to fingerprint than AI patterns. Use the output as a starting point, not a verdict.

**It's a draft tool, not a publishing gate.** Run it before you finalize, not after you're committed to the text.