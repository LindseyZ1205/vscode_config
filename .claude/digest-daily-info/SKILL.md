---
name: digest-transcript
description: Process a Microsoft Teams meeting transcript. Cleans up the raw transcript in place to readable English dialogue, and creates a companion `-digest.md` file with bilingual (English + Chinese) topic summaries and a Chinese analysis section. Use whenever the user wants to digest, summarize, organize, or 整理 a Teams meeting transcript.
argument-hint: <transcript-path> [reference-1] [reference-2] ...
disable-model-invocation: true
allowed-tools: Read Write Edit
---

# Digest a Teams Meeting Transcript

Process the user's Microsoft Teams meeting transcript file into two outputs:

1. **Clean up the original transcript file in place** — readable English dialogue, no analysis.
2. **Create a new `-digest.md` companion file** — bilingual topic-by-topic summary + Chinese analysis section.

## Arguments

`$ARGUMENTS` is a whitespace-separated list of file paths:

- **First path** (required): the raw Teams transcript file to process.
- **Remaining paths** (optional): reference files (prior meeting notes, project docs, contact lists) that provide business background. Read them so the digest captures context the transcript itself does not explain.

If no transcript path is given, ask the user which file to process before doing anything else.

## Step 1 — Read everything first

Read the transcript file. Then read **every** reference file the user provided. Reference material is what lets the digest connect names, acronyms, and projects to the broader context — do not skip it.

If the user did not provide references but the transcript clearly belongs to a project folder, check sibling files in that folder (prior meeting notes, design docs, READMEs) for relevant background and read them too.

## Step 2 — Rewrite the original transcript file (clean English)

Overwrite the original transcript file with a cleaned-up version. The goal: a human can read it as a normal dialogue without wading through Teams artifacts.

**Format:**

```markdown
# <Meeting title — keep or improve the existing one>

> Date: <YYYY-MM-DD HH:MM>
> Participants: <Name 1>, <Name 2>
> Duration: <e.g. 26 minutes>

---

**<Speaker Name>:** <Cleaned-up speech...>

**<Speaker Name>:** <Cleaned-up speech...>
```

**Cleaning rules:**

- Strip Teams artifacts: timestamps, "started/stopped transcription" lines, duration markers per utterance.
- Remove filler words and false starts: `uh`, `uhh`, `mm-hmm`, `mhm`, `ohh`, `you know` (when used as filler), repeated words.
- Merge consecutive utterances from the same speaker into one block.
- Fix grammar and broken sentence fragments **without** changing meaning or substituting words. Keep the speaker's voice.
- Preserve verbatim: product names, person names, technical terms, acronyms, project names. Teams auto-captions frequently garble names and uncommon technical terms — when you spot something that looks like a phonetic mistranscription of a name or term that appears correctly in the reference files, correct it. If no reference disambiguates the spelling, leave the transcript's version as-is rather than guessing.
- Do **not** add analysis, commentary, or section headers — the cleaned file is just the dialogue.

## Step 3 — Determine the digest file path

Insert `-digest` before the `.md` extension of the original path.

- `foo/2026-05-15-meeting.md` → `foo/2026-05-15-meeting-digest.md`

## Step 4 — Write the `-digest.md` file

The digest file has a small header block, one bilingual section, and one Chinese analysis section.

### Header block

```markdown
# <Meeting title> — Digest

> Original transcript: `<basename of transcript file>`
> Participants: <names>
> Duration: <duration>
> Format: <e.g. 1:1 sync, team standup, architecture review>
```

### Section A — `## Bilingual Transcript Digest / 双语摘要`

Break the conversation into **6–10 logical topic segments**. Order them by topic flow, not strictly by chronology — group related back-and-forth together.

For each segment, write exactly this structure:

```markdown
---

**[<Topic label in English>]**

<One English paragraph: clean prose, corrected grammar, captures the substance of this segment. Not a transcription — a faithful summary.>

<One Chinese paragraph: natural business Chinese, captures the same meaning and nuance. Not a word-for-word translation — adjust phrasing for fluency. Describe what was discussed and any tension/decision.>
```

Rules:

- Use `---` dividers **before each segment** (and once at the top of the section).
- The English paragraph fixes grammar and tightens phrasing — it is not a literal copy of the speaker's words.
- The Chinese paragraph reads as if written natively in Chinese, not translated. Keep technical terms, product names, company names, and industry acronyms in their original English form even within Chinese sentences.
- Each segment is self-contained — a reader skimming one segment should not need the others to understand it.
- Preserve names and product names exactly. Cross-check against reference files.

### Section B — `## 中文解读`

A structured Chinese analysis at the bottom. Use these four sub-sections with these exact headers:

```markdown
### 会议主题

<2–3 sentences in Chinese: what the meeting was fundamentally about, what threads it weaves together.>

---

### 重要信息

<Numbered list of 4–6 key facts/updates. Each item: bold lead-in summarizing the point, then 1–2 sentences of detail.>

---

### 重要 Actionable Items

| 优先级 | 行动项 | 负责人 | 说明 |
|---|---|---|---|
| 🔴 高 | ... | ... | ... |
| 🟡 中 | ... | ... | ... |
| 🟢 低 | ... | ... | ... |

<5–8 rows. Prioritize concrete next steps with a clear owner.>

---

### 重要结论

<Numbered list of 4–6 conclusions or decisions reached. Each item bold lead-in, then 1–2 sentences of context.>
```

## Style guidelines

- **Faithful, not literal.** Both the cleaned transcript and the digest should preserve meaning, decisions, and nuance. They should not invent claims or sharpen positions the speakers did not actually take.
- **Business Chinese, not direct translation.** The Chinese paragraphs should read naturally to a native Chinese reader working in tech.
- **Use reference files for context.** If the transcript mentions a project, person, or acronym that is only meaningful with background, pull that context from the references — but do not pad the digest with reference material that did not come up in the meeting.
- **No emojis in the cleaned transcript.** Emojis only appear in the Actionable Items priority column (🔴🟡🟢).
- **Markdown discipline.** Headers nested correctly (`#` title, `##` major sections, `###` sub-sections). Dividers (`---`) used as specified.

## Final check before finishing

After writing both files:

1. Confirm the original transcript file is now the clean dialogue version (not the raw Teams output).
2. Confirm the `-digest.md` file exists at the right path with the bilingual section + Chinese analysis.
3. Reply to the user with one short sentence listing the two file paths produced. No long summary.
