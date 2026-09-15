# skill-presentation-build

A Claude Code skill that builds the **structure** of a talk before it builds a single slide.

**English** · [Tiếng Việt](README.vi.md)

---

## The problem it fixes

Ask an assistant for "a deck about X" and you get slides in thirty seconds — slides that
are a written document in disguise, that the speaker ends up reading aloud, and that the
audience has already finished reading before the speaker reaches line three.

The failure is not visual. It is structural, and it happens before any slide exists.

A structure exists to do two jobs at once: let the **audience** follow the argument and
remember the message, and let the **speaker** stay calm, on point, and able to move
between sections without groping for the link.

So this skill fixes the order:

```
brief  →  section map  →  speaker script  →  slides
```

No slide tool opens until the section map is written down and corrected.

---

## What it does

### 1. The brief — three questions, asked one at a time

| | |
|---|---|
| **Goal** | Not the topic. Inform, persuade, sell, teach, get a decision, get budget. |
| **Audience** | Who is in the room and **what they already know** — this sets how much context to build and which jargon is free. |
| **The one message** | What must they remember afterwards? One sentence. If it takes three, the talk has no message yet. |

Plus five constraints that change the shape of the structure: duration, interaction level,
context (stage / boardroom / Zoom / classroom), whether there is a demo, and what visual
material exists.

Everything downstream is judged against the one-sentence message.

### 2. The structure

Defaults to the classic five parts — greeting, opening, body, conclusion, thanks & Q&A —
and switches to an alternative when the situation calls for it:

| Pattern | Use when | Sequence |
|---|---|---|
| **Basic** | Most talks, updates, teaching | Greeting → opening → body → conclusion → Q&A |
| **Demo** | Introducing a product or system | Value → need → problem → demo → how it scales |
| **Problem–solution** | Persuading someone to change | Problem → impact → solution → call to action |
| **Story** | Building emotion, holding attention | Context → challenge → journey → outcome → lesson |
| **Elimination** | Contested topic, several camps | Problem → options → limits of each → recommendation |

Every body section must carry **all four** of: one main point, evidence, what it means for
*this* audience, and a summary sentence said out loud before moving on. A section missing
one is not ready.

### 3. The section map — the actual work product

A table you correct in one pass, before anything is built:

| # | Section | Main point | Evidence | So what, for them | Transition into next | Min |
|---|---|---|---|---|---|---|

Two rules that do most of the work:

- **Time is budgeted first, content fits into it.** Opening ≈ 10%, conclusion + Q&A ≈ 20%,
  body gets the rest. A 20-minute talk supports **three** body sections. Not six.
- **Every transition is written out as a sentence.** Summarise what finished → why it
  mattered → what comes next → the link between them. Transitions are where speakers lose
  the room *and* lose their own thread, so they are not left to improvisation. Group
  handovers are written the same way.

Sections that can be cut if time runs short are marked **now**, calmly, not on stage.

### 4. The speaker script

Not bullets. Per section: the opening line, the point, the evidence with its numbers, the
so-what, the summary line, the written transition, and a target minute mark. The **first 60
seconds and last 60 seconds are scripted word-for-word** — they decide how the talk is
received and what survives it.

Plus a Q&A prep block: five likely questions, one of which must be the hostile one.

### 5. The slides

Only then. One slide, one idea. An image or diagram instead of a paragraph. Minimum 30pt
type. An agenda slide and a summary slide, because they are the audience's map. Kawasaki's
10–20–30 as a calibration point, not a law — a three-hour workshop obviously breaks it, but
the type size never bends.

Built into whichever channel the deck needs to live in:

| Channel | Pick it when |
|---|---|
| **Gamma** | Fastest path to a good-looking deck; will keep being edited online |
| **.pptx** | Must open in PowerPoint or Keynote, be emailed, handed to an organiser |
| **HTML Artifact** | Layout control matters, or it should live at a shareable URL |
| **Canva / Adobe Express** | A designer will take it further in their own tool |

### 6. A pre-delivery checklist

Twelve items, including the one that matters most: **is the one-sentence message
recoverable from the conclusion alone?**

---

## Install

```bash
/plugin marketplace add vicky-tiq/skill-presentation-build
/plugin install presentation-build
```

Or drop `skills/presentation-build/` into `~/.claude/skills/`.

---

## Use

It triggers on its own for anything deck-shaped. Or call it directly:

```
/presentation-build
```

Trigger phrases include *presentation, slides, deck, pitch deck, talk, workshop, webinar,
keynote, speaker notes, outline my talk*, and in Vietnamese *làm slide, bài thuyết trình,
chuẩn bị bài nói, dàn ý bài trình bày, kịch bản thuyết trình, bài giảng*.

---

## What's in the box

```
skills/presentation-build/
├── SKILL.md                          the six-step procedure
└── references/
    ├── structures.md                 five patterns in full, ordering schemes,
    │                                 transition phrasing, group handovers,
    │                                 a fully worked workshop example
    ├── script-template.md            speaker script format, timing, Q&A prep
    └── slide-channels.md             producing the deck in each of the four channels
```

---

## Source

The structural principles come from VirtualSpeech's
[How to Structure your Presentation](https://virtualspeech.com/blog/how-to-structure-your-presentation),
turned into an enforceable procedure: fixed order of work, a time budget that caps section
count, transitions written rather than improvised, and a checklist that has to pass before
delivery.

MIT licensed.

---

## Contributing / editing

```bash
git clone https://github.com/vicky-tiq/skill-presentation-build.git
ln -s "$PWD/skill-presentation-build/skills/presentation-build" ~/.claude/skills/presentation-build
```

Claude Code reads the skill through the symlink, so an edit in the repo is live
immediately — no copy step, nothing to forget to sync.
