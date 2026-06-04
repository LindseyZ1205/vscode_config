# Day 1 Actionable Items, June 1 2026

> Source meetings: 1on1 with manager, 1on1 with Jonathan (mentor), team weekly (on-call review + Workstreams vision + canvas demos).

---

## 1. What I Learned from Day 1

These are the facts I pulled out of the three meetings. They are not opinions yet, just what I observed.

1. The product is almost certainly **Amazon Q** (the "Quick" rendering in the transcripts is Teams auto caption drift from the single letter Q). It is pitched as "an IDE for business" — one surface that replaces switching across email, Slack, docs, code.
2. Around April the team launched a path to let regular users log in with Gmail or a personal email, so the product is no longer enterprise SSO only. It is now consciously chasing consumer plus mid market in addition to enterprise.
3. The product is evolving from a chat first interface to an outcome first agent. Step one is "user talks to a bot that talks to systems." Step two is "user defines an outcome and the system runs it on schedule, generates reports, fires actions."
4. The biggest current engineering push is **unifying the web app and the desktop app into a single architecture**, with the desktop app as the primary load bearing surface going forward. Jonathan said explicitly: "just explore the desktop app more since that is where we are headed."
5. The differentiating feature Jonathan named is **"My Contacts"**, a knowledge graph that learns over time. The moat is durable cross system personalized context (tone preferences, who you collaborate with, shared resources), not project management features.
6. Arvind, the product lead, framed the strategic direction as **Workstreams**, which he wants to be the next form of "agent spaces." It is outcome first, with a proactive generative canvas as the primary surface and chat or knowledge or artifacts as secondary surfaces.
7. The team intentionally favors a **single shared canvas** over per user views, because once you let two viewers see different things the shared source of truth dies. Arvind framed this as a trust decision, not a feature decision.
8. The connector stack named on day 1 is **Slack, Outlook, Microsoft Teams, MCP servers**. External tools are treated as ingress points for context, not as targets to replicate.
9. Senior leadership from Seattle (Sid at L7 and Suharsh at L8) flew in for one or two days, which made the day 1 schedule denser than a normal first day.
10. I heard **two different sets of names for the chain of command** across the day. The manager 1on1 named Pankhuri (direct), Siddharth (skip), and Sid Uppal. Jonathan named Prateek (Seattle, official) and Kartik (local point of contact). The two sets do not overlap, which most likely points to a matrix structure where one line is administrative and the other is project facing. I want to confirm which is which.
11. The team has gone through a few direction shifts in the past several quarters, so I should expect prior internal documents and prior plans to age quickly and treat them as snapshots rather than current truth.
12. Sync cadence is two tiered: weekly 1on1 with the manager (day not yet picked), daily 15 minute standup with Jonathan, Slack as the always on async channel.
13. The project is mine to own. The manager framed it as "you own the design and the vision, identify the approach, build a prototype, deliver an end to end prototype for the company." Jonathan mentors, the manager joins selected calls, Sairam and others help as needed.
14. The specific summer project will be scoped two days from now. Jonathan said "we will get to that later in the week once we sort things out on our end, probably not for another two days." Day 1 priority is onboarding plus product exploration, not project work.
15. The team is heavily LLM assisted in everyday coding. Jonathan said: "we heavily use LLMs for coding, and you should leverage that too." The specific approved tool was not named in the meetings.
16. Amazon specific stack basics: build system is **Bazel** (analogous to Maven or Gradle), main languages on the team are **Scala and Python**, pull requests are called **CRs** (code reviews), and onboarding is driven by a task list system called **embark**.
17. The team is heavy on operational discipline. On call work is captured in a structured markdown report (`weekly_report_2026-06-01.md`) under the `UniversalAICapabilities` package, with sections for new and worked Sev 2, resolved Sev 2, open Sev 2 carried into next week, and notable lower severity tickets.
18. The same fault often produces both an SNCS orchestrator fault ticket and a chat QBS activity ticket. The team agreed to make ticket deduplication a next week action item.
19. The two Workstreams demos showed concrete shapes for the new direction. Sahil's demo had a tab based canvas with agent and human co edit, a Watchman agent that mutates the canvas based on comments, and Slack as an input source for new context. Ibrahim's demo focused on shareable markdown documents backed by a Quip replacement called **Chorus**, with real time cursors and selection based agent edits.
20. The work culture is explicitly results oriented. Jonathan: "you do not have to stay for a certain number of hours, we value outputs and getting work done."

---

## 2. What I Should Do Now

These are the actions I will take this week. I split them into two categories: hands on product exploration that I can do on my own, and onboarding and relationship steps that depend on others.

### 2.1 Hands on product exploration

The strongest single instruction I received on day 1 was Jonathan's: explore the desktop app more, because that is where the architecture is heading. I will treat this as the most load bearing task of the first week and execute it as a small structured experiment rather than casual clicking around.

I will create a dedicated folder at `02-projects/2026-06-01-explore-quick-desktop/` and use it as the workspace for this exploration. Inside that folder I will keep a `downloads/` subdirectory for the desktop app installer plus any sample inputs (small PDFs, sample docs) that I feed into the product, and a notes file capturing what each feature does, where it gets slow, where it surprises me, and where it visibly fails. Small input artifacts (a handful of small binary files) go into git so the exploration is reproducible. Large outputs do not.

The features I want to touch in this first pass, in priority order, are:

- The chat surface with a file granted from the local filesystem, repeating Jonathan's "what is in C.pdf" example on my own files.
- The "generate a docx that says hello world" capability that Jonathan demoed, end to end, including downloading and opening the resulting Word file.
- The scheduled task capability ("every Friday email me a summary"), even with a trivial task, to feel the boundary between chat and automation.
- The "My Contacts" knowledge graph: deliberately seed a tone preference and a fake relationship, then see whether and how it persists across sessions.
- Any visible Workstreams or spaces or canvas surface, even if early, because that is where the product is heading.

### 2.2 Onboarding, environment, and relationships

In parallel with product exploration I will keep moving the standard onboarding forward. The embark task list is the canonical track. I will work through day one and week one tasks rather than batching them, because the Bazel and CR workflow context lives inside those tasks and I want it in working memory before the project is scoped.

I will also use the day 1 inbox invitations to actually book 1on1s with Sairam and a few other peers this week. The manager framed this lightly, but in a window where the management layer is thin and shifting, lateral relationships are the structural support, not a nice to have. I will aim for at least three peer 1on1s in week one.

On the management side I will propose a weekly 1on1 time to the manager rather than waiting for the meeting to be put on the calendar, and I will treat Jonathan's daily 15 minute standup as the primary channel for everything tactical. For both meetings I will arrive with a one screen agenda rather than open ended check ins.

### 2.3 Local environment and AI assisted workflow

In parallel I will get my local AI assisted workflow ready so that by the time the project is scoped I can start writing code immediately. Three concrete steps.

First, set up the Amazon sanctioned LLM tooling for coding. I will confirm with Jonathan which tool or tools I should be using inside Amazon (this is one of my questions in Section 3.2) and then complete whatever internal setup is required.

Second, set up Claude Code on my local machine, configured against this same project repository. I am already using it to author my meeting digests, my actionable items, and small project skills. I want it ready in the same environment where the prototype code will live, so the same context window covers both.

Third, prepare the Agent Skills I expect to use early. The `digest-transcript` skill is already in place and I am using it on every meeting. I plan to add small skills as patterns repeat: for example, a skill to summarize Amazon embark tasks I complete, and a skill to scaffold a CRUD on resource service skeleton once the prototype direction is confirmed. The principle is to keep the toolkit thin and only add a skill when I notice myself doing the same shape of work more than twice.

---

## 3. For Tomorrow's 15 Minute Standup with Jonathan

The goal of this segment is to make tomorrow's standup useful in two directions. First, I want to show Jonathan how I am processing the day 1 information firehose, and confirm that my early opinions about the project shape are pointed at the right thing. Second, I want to ask him a small number of high leverage questions where his answer will measurably change what I work on next.

### 3.1 My early opinions, which I want to confirm with Jonathan

These are not facts. They are the first round of judgments I formed by reading the day 1 transcripts side by side. I want to put them on the table so Jonathan can either validate them or correct them early, before I invest a week of effort in the wrong direction.

- **What I think my prototype should center on.** Given that the product is moving from chat first to outcome first and that the desktop app is the unifying surface, my working assumption is that a useful prototype focuses on the **API and interface layer**: define the operations that a Workstream or canvas needs to perform, treat them as CRUD on a typed `Resource` (where a `Resource` is whatever piece of intake context the user brings in, for example a document, a Slack thread, a meeting), and mock the underlying services with plain Python functions. This keeps the design honest about contracts while staying small enough to ship. I want to check with you whether that framing is in the right neighborhood, too shallow, or too far from where the team is actually heading.
- **A concrete way to make this dependency free.** To keep the prototype unblocked while the platform decisions are still being made, I would abstract every `Resource` as a binary blob plus a bag of metadata. The binary can be anything: pure text, a typed MIME payload, a JPEG, a PDF, an audio file. Whatever the producer is, the CRUD layer sees a uniform shape and the downstream processors only need to look at the metadata to decide how to handle it. This means the prototype does not depend on a specific backend, a specific connector, or a specific Workstream surface to make progress. It feels like a low risk, easy to demo starting point.
- **Why CRUD on a Resource feels like the right abstraction.** Both Sahil's Watchman demo and Ibrahim's Chorus demo are ultimately mutating a shared object (a canvas, a document) based on a mix of human and agent input. If I keep the object model crisp and the mutation surface small, I can show the contract before any backend is real, and I can swap in a real backend later without rewriting the front edge.
- **My judgment on Slack as a surface.** From the meeting I would deprioritize building a Slack ingress in week 1 of the prototype, because Arvind framed Slack as an ingress point, not as the primary surface, and the meeting host noted Slack work likely moves to a later phase. I want to check with you that this matches how you see scope.
- **My judgment on what is in scope for "differentiation."** The differentiation the team keeps coming back to is proactiveness on the canvas plus durable personalized context. So if I prototype anything that touches user facing behavior, it should lean into one of those two, not into project management features that overlap with Jira or Notion.
- **How I am processing meeting information.** I would like to briefly share my screen and walk through the `digest-transcript` Agent Skill I built (file path `.claude/skills/digest-transcript/SKILL.md` in my project repo). It is what turned the three raw Teams transcripts from yesterday into the clean dialogues, the bilingual digests, and ultimately this document. The point is to show the workflow I am using to compress meeting information so I can apply my own judgment on top, not to spend long on the tool itself.

### 3.2 Questions I want to ask Jonathan

These are the questions I picked deliberately. The filter I used was: would the answer change what I do tomorrow? If yes, it stays. If it is just generally interesting, it waits.

- The two chains of command I heard today do not overlap. Pankhuri or Siddharth or Sid Uppal on one side, Prateek or Kartik on the other. Can you walk me through which chain handles administrative and HR matters, and which one I should go to for project and technical direction? I want a clear default routing.
- Where exactly does the `UniversalAICapabilities` package live, and is it reasonable for me to read the on call weekly report you shared in the meeting? I would like to use it as a real artifact to learn the operational shape of the codebase while waiting for project scope.
- When you say "we heavily use LLMs for coding," which tool or tools are sanctioned at Amazon for me to use, and is there an internal setup I should follow on day one to avoid using something I should not? I want to get this right before I start writing any code.
- For the desktop app exploration this week, are there specific capabilities, edge cases, or known rough edges you would most want a fresh pair of eyes on? I am going to explore broadly, but I would rather collect signal that is useful to you.
- You mentioned the project will be scoped in about two days. To make that conversation faster when it happens, is there one or two reference documents (a design doc, a vision deck, a prior intern's project, even a Slack thread) you would point me at to prepare?
- On the canvas direction, Arvind's "democratic shared canvas, no per user views yet" decision was very deliberate. Is that a constraint I should treat as fixed when I start sketching prototype ideas, or is it open for the prototype to challenge?
- Finally, on cadence: would it work for you if I come into our daily 15 minutes with a short written agenda (three or four bullets) instead of an open ended sync? I want to make the time useful for you, not just for me.

---

## 4. Slack-Async Questions to Jonathan (Not for Standup)

These are two questions I want to send to Jonathan on Slack rather than bring into the daily standup. The standup time budget is tight and neither is best served by a live answer. Q1 is strategic and Jonathan should have time to think before replying. Q2 is tactical and a one line reply unblocks me. I will send them as two separate Slack messages. Q2 goes first because it is low cost and builds rapport, and Q1 follows an hour or two later so it does not get buried under the tactical exchange.

### 4.1 Scope alignment with Jonathan (send second, an hour or two after Q2)

The goal here is to convert the ambiguity in "you own the design and the vision" into a concrete multiple choice so Jonathan can pick one quickly. Front-loading the prep evidence (AWS account, hands-on time with Spaces, Flows, Research, and connectors, and the boto3 Quick APIs) is deliberate. It tells Jonathan in the first sentence that I am not a blank slate, which should change how he calibrates the answer.

The exact Slack message to send:

> Hi Jonathan, this is a non-urgent ask whenever you have a moment.
>
> Some quick context before I get to the question. Before the internship started I spun up my own AWS account, set up Quick Suite, and spent time hands-on with Spaces, Flows, Research, and the connectors. I also used the boto3 Quick APIs against my own resources, so I am coming in with real product context rather than starting from zero.
>
> Here is what I want to align on. On Monday Pankhuri framed the project as mine to own, including the design, the vision, the prototype, and the end-to-end delivery. That gives me a lot of room, which I appreciate. The flip side is that because I do not yet have visibility into the internal roadmap, I am worried about proposing a direction that the team has already shipped, is currently building, or has already considered and decided against. That would burn my cycles, and it would also make my proposal look naive in front of senior engineers.
>
> To make our scope conversation later this week go faster, could you tell me which of these I should be planning around?
>
> 1. **Free design.** I explore Quick Suite, identify a gap I think is worth solving, and bring you a written one-pager. You veto or steer.
> 2. **Constrained design.** You or Pankhuri name a problem area such as connector reliability, Workstream context, or the My Contacts knowledge graph, and I design within that frame.
> 3. **Specific project.** You or Pankhuri already have a concrete project in mind. I take the scope as given and own the design and prototype on top of it.
>
> Any of the three works for me. Knowing which one we are in will let me spend the next two or three exploration days much more pointedly.

### 4.2 Desktop app login issue (send first)

I hit a real blocker on the desktop app and I want to surface it cleanly. The framing is deliberate. I lead with the fact that I am on a personal AWS account so Jonathan does not assume an internal dev env problem. I show I already debugged it with a hypothesis plus a web search. I split the question into "is desktop load-bearing for what you want me to learn" versus "should I file a bug". And I end with a default action so I am not blocked while waiting.

The exact Slack message to send:

> Hi Jonathan, this is a quick exploration question and not urgent.
>
> I tried logging into Amazon Quick Desktop using my own AWS account (an IAM user on my personal account, since I do not have an internal dev env yet and have been using my personal AWS for product exploration). The desktop hung on a spinning state after the auth step. Retry, cancel, and signing in again did not help, and signing out of the AWS account in the browser did not reset it either.
>
> My current hypothesis, after a quick web search, is that the OAuth callback is not jumping back to the desktop app. It looks like a desktop-side bug, possibly specific to the IAM-user auth path rather than to Identity Center or the consumer Gmail flow.
>
> Two small questions for you.
>
> 1. For the exploration you want me to do this week (chat with local files, generating a docx, scheduled tasks, My Contacts), is the **web console** sufficient to cover most of it, or is the **desktop app** load-bearing for something specific I should not skip? I am happy to wait on a desktop fix if it is the latter.
> 2. Is this worth filing as a bug somewhere? I can put together a clean repro if it would help.
>
> I will keep exploring on the web console in the meantime unless you say otherwise.
