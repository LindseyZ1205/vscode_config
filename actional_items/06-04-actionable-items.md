# Day 2 Actionable Items, June 2 2026

> Source: my own voice memo at the end of Day 2, focused on what I want to accomplish on Day 3 (June 3).
> Companion files: `06-02_1on1_with_mentor_transcript-digest.md`, `06-02_standup_Kertik_transcript-digest.md`.

---

## 1. The Single Priority for Tomorrow

Tomorrow's load-bearing task is to **walk the full Amazon internal code review workflow end-to-end, on my own**, so that by end of day I can clone a repo, branch, commit, raise a CR, answer review comments, and merge — without having to ask Jonathan or Kartik how each step works.

The system is Amazon's internal GitHub equivalent. Jonathan called it `code.amazon.com` in our 1:1 (it lives under the Brazil / Builder Hub tooling family). The mechanics map onto regular GitHub — pull, branch, CR (which is what Amazon calls a pull request), reviewer assignment, comment threads, merge — but the access model, the toolchain, and the conventions are Amazon-specific.

I am picking this as the day's anchor for three reasons:

1. **It unblocks everything else.** Reading CRs is one of the four things Jonathan explicitly asked me to do in the first few days, and I cannot review a CR meaningfully without first feeling the workflow from the author side.
2. **It is the prerequisite for the project work that starts next week.** Once the summer project is scoped (Jonathan has a meeting on June 3 to define scope), I want to be able to write code on day one without burning that day on Brazil setup or CR mechanics.
3. **The first CR is always the slowest.** I would rather pay that cost on a deliberately trivial change tomorrow than on real project code next week.

---

## 2. The Four Steps I Will Run Through

I am going to treat this as a small structured experiment rather than improvising. Four steps, in order.

### Step 1 — Confirm my access

Before I do anything else, I need to know exactly what I have permission to do.

- Can I log into `code.amazon.com` with my Amazon credentials right now? If yes, what level of access do I have? If no, what is the request flow to get it?
- Where on Amazon's internal tooling can I see my own permission set? I want a single page or command that tells me what I can and cannot touch, not an inference from trial and error.
- If access is missing or partial, file the request today rather than tomorrow morning, so it does not block Step 2.

### Step 2 — Map the repos that matter

Once I am in the system, I want a short, written list of repos that are relevant to my world.

- Which repos does the team own? Kartik named `AWSQuickWork` and `UniversalAICapabilities` in standup — those are the two I have heard most often. There are almost certainly more.
- Out of those, which ones am I expected to **read** (to understand how the system works) versus which ones am I expected to **touch** (write code in) versus which ones am I explicitly **not** supposed to touch?
- Separately: for practice, can I create my own personal repo to use as a sandbox? If yes, what is the convention (naming, visibility, ownership)? If no, what is the recommended sandbox path — a feature branch on an existing repo? A scratch package?

I want answers to these in writing by lunch, even if the answers are short.

### Step 3 — Run one full CR cycle on a deliberately trivial change

Once Step 2 tells me where I can safely practice, I will do exactly one end-to-end CR cycle. The change itself has to be small and meaningless on purpose — large enough to exercise the toolchain, small enough that no reviewer has to think about correctness.

My plan is to add a single `chore.txt` housekeeping file (or similar) with one-line content like `1` (or change an existing throwaway value from `1` to `2`). It is unambiguously a no-op for the codebase. It is not documentation, so it cannot mislead anyone. It exists only to give me a payload to push through the workflow.

The full cycle I want to walk:

1. Clone the target repo to my local machine via Brazil (`brazil ws create` or equivalent — I will confirm the exact command).
2. Create a new branch with a sensible name.
3. Add the chore file. Commit. Push to the remote.
4. Open a CR. Assign a reviewer — I will check with Jonathan in the morning who the right courtesy reviewer is for a no-op practice CR.
5. Walk through the review interface, even if there are no real comments. Add a comment, resolve a comment, mark the CR ready, etc.
6. Merge. Verify the merge landed on the target branch.
7. Clean up the local branch.

If anything in this sequence breaks or surprises me, I capture the surprise immediately rather than work around it silently — surprises are exactly what the documentation in Step 4 is for.

### Step 4 — Document every command into a reusable agent skill

Once the cycle is done, I write down every single command I used, in order, with the IDE / tool / CLI context for each one. The goal is a runnable document that turns "I have done this once" into "I can teach someone else (including future me) to do this without thinking."

Concretely:

- Which command clones a Brazil workspace, and how do I pick the right version set?
- Which CLI vs IDE workflow do I use to branch and commit? Where does Kiro fit in, where does Claude Code fit in, where do I drop to plain `git`?
- What is the canonical `push` flow? Is there a custom Amazon wrapper, or is it stock `git push`?
- How is a CR opened — through the web UI on `code.amazon.com`, or via a CLI command? What metadata do I need to attach?
- How are reviewers assigned, and what is the etiquette for picking one?
- What does the merge button actually do — squash, rebase, merge commit?

I want this written up in `02-projects/` (or wherever fits best) as a markdown file, and then promoted into a reusable Claude Code agent skill — likely at `.claude/skills/amazon-cr-workflow/SKILL.md`. The skill should let me (or any future Claude session) re-run this workflow without re-discovering the mechanics each time.

This converts a one-off learning exercise into a permanent tooling asset, which is the kind of compounding investment Mac has been pushing me to make from Day 1.

---

## 3. What This Day Looks Like in Practice

Rough shape of the day:

- **Morning (before standup):** Step 1. Confirm access and map permissions. If a request needs to be filed, file it now.
- **Standup at 12:30 PM:** Use the 30 seconds I have to mention that today's focus is the CR workflow walkthrough on a no-op chore CR, and ask Jonathan (or whoever) for a courtesy reviewer.
- **Afternoon (post-standup):** Steps 2 and 3. Map the repos and run the full cycle.
- **End of day:** Step 4. Write up the documentation while the commands are still fresh in working memory. Promote into an agent skill if the writeup is clean.

If any one of these blocks gets blocked (e.g. I cannot get access until tomorrow), I do not waste the day — I shift to reading existing CRs in `AWSQuickWork` to build pattern recognition for the review interface, and continue desktop-app product exploration in parallel.

---

## 4. Why I Am Not Doing More Than This Tomorrow

I deliberately kept tomorrow's plan to one main thread. Two reasons.

First, the project itself is not yet scoped — Jonathan has a defining meeting on June 3 and the scope conversation only really starts after that. Pushing on speculative project work before scope lands would burn cycles in the wrong direction.

Second, the CR workflow is exactly the kind of foundational mechanic that is invisible when it works and a constant tax when it does not. Spending one full day on it now buys back a week of friction during the execution phase. That is a trade I am willing to make.

Everything else — embark tasks, Quick desktop app exploration, reading sample CRs — continues in the background, but the day's "done / not done" verdict hangs on whether I can run one full CR cycle by EOD and ship a documented agent skill out the other side.
