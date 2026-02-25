# voice-humanizer

A Claude Code skill that checks your writing against *your own voice*, not generic AI-pattern rules.

The [humanizer by Siqi Chen](https://github.com/blader/humanizer) catches generic AI tells. This does something different: it calibrates to a specific author's voice using their published work as a corpus, then flags drift from that voice alongside the standard AI pattern check.

---

## What it does

**For drafts:**
- Voice drift flags (with rewrites in your register)
- Specificity audit (every unanchored claim, with required substitution)
- AI pattern check (weighted below voice drift)
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

### Example

Here's voice-humanizer catching drift that a generic humanizer would miss.

**Before (draft):**

> The fingerprint tracks rhythm patterns, paragraph opening style,
> specificity signals, what you reach for when you need a concrete
> detail, and — just as important — what you don't do.

**Flag:**

> Voice drift — list of five items where your corpus shows you compress
> to two. Em dash doing emotional emphasis work your corpus handles
> structurally.

**After:**

> The fingerprint tracks what you reach for and — just as important —
> what you don't. Rhythm, specificity, the patterns absent from your
> corpus that signal drift.

No AI pattern was triggered. A generic humanizer would have passed this.
Voice-humanizer caught it because the corpus knew this author compresses
lists. That's the difference.

---

Built for Claude Code. Claude desktop users see SETUP.md for manual usage. Inspired by [blader/humanizer](https://github.com/blader/humanizer).