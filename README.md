# voice-humanizer

A Claude Code skill that checks your writing against *your own voice*, not generic AI-pattern rules.

The [humanizer by Siqi Chen](https://github.com/blader/humanizer) catches generic AI tells. This does something different: it calibrates to a specific author's voice using their published work as a corpus, then flags drift from that voice alongside the standard AI pattern check.

---

## What it does

**For drafts:**
- Voice drift flags (with rewrites in your register)
- Specificity audit (every unanchored claim, with required substitution)
- AI pattern check (24 Wikipedia patterns, weighted below voice drift)
- Comment stacking detection (attribution lists that aren't building toward a point)

**For incoming comments:**
- Authenticity score (0–3): specific citation + personal experience + real question
- Synthetic praise detection
- Response length recommendation

**For your own replies:**
- Three-step engagement check: locate what's new → extend it → redirect
- Voice drift flags
- Tic detection

---

## Install

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/dannwaneri/voice-humanizer.git ~/.claude/skills/voice-humanizer
```

Then replace `CORPUS.md` with your own writing. See `SETUP.md` for full instructions.

---

## The key idea

Generic humanizers check for patterns to avoid. This one checks for patterns to *match* — your specific cadences, the kinds of specificity you reach for, what good writing in your voice actually sounds like vs what Claude-flavored-you sounds like.

The corpus is private (`.gitignore`). The skill and structure are public.

---

Built with and for Claude Code. Inspired by [blader/humanizer](https://github.com/blader/humanizer).