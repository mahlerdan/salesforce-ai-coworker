# Video 5: "How I Use My AI Coworker as a Salesforce BA"

**Format:** Full workflow demo. 6-8 minutes.
**Goal:** Show one complete end-to-end workflow. Pure demonstration, no setup.

---

## Opening (30 seconds)

> "This is a real workflow I do at least twice a week. I come out of a client meeting
> with messy notes, and I need to turn them into something my team can build from.
>
> Let me show you how Scout and I do this together."

---

## The Scenario (30 seconds)

> "I just had a requirements meeting with a client. They want to build a customer
> portal in Experience Cloud where contacts can view their cases, submit new ones,
> and update their account information.
>
> Here are my raw meeting notes."

*[Show: messy, realistic meeting notes — incomplete sentences, shorthand, tangents,
 decisions mixed in with questions]*

---

## Step 1: Raw Extraction (2 minutes)

> "First pass — I give Scout everything and ask for structure."

*[Paste notes into Slack, ask Scout to extract requirements]*

*[Show: Scout outputting organized user stories, acceptance criteria, decisions,
open questions, out-of-scope items]*

> "In about 30 seconds, Scout separated requirements from decisions from open questions.
> The stuff that would take me half an hour of copy-paste-reorganize."

---

## Step 2: Refinement (2 minutes)

> "But it's not perfect. Let me refine."

*[Show: asking Scout to add complexity estimates, break a large story into smaller ones,
add Salesforce-specific implementation notes]*

> "'For the case submission story, add notes about which record types to use and
> whether we need a custom LWC or if standard components work.'
>
> Scout adds implementation-level detail because the SOUL tells it I'm working with
> Experience Cloud and LWCs."

---

## Step 3: Gap Analysis (60 seconds)

> "Now I ask Scout: 'What did we miss?'"

*[Show: Scout identifying gaps — security model questions, guest vs authenticated user
 access, email notifications, file attachments on cases, mobile responsiveness]*

> "Five things that weren't in the meeting but will absolutely come up during build.
> Now I can ask the client *before* it becomes a blocker."

---

## Step 4: Output (60 seconds)

> "Scout writes the final requirements doc to my project folder. Formatted, organized,
> ready to share."

*[Show: the final document]*

> "Total time: about 5 minutes of conversation. Normally this is 30-45 minutes of
> organizing notes, writing stories, and trying to remember what someone said.
>
> And the next time I have a requirements meeting, Scout already knows my format
> preferences, my project context, and my Salesforce stack. It just gets faster."

---

## Close (30 seconds)

> "This is one workflow. I use Scout for troubleshooting, documentation, architecture
> review, deployment checklists, and more. Each one started the same way — I did
> the work manually, noticed the pattern, and turned it into a skill.
>
> If you're a Salesforce BA, admin, developer, or consultant and you're spending
> hours on work that follows a pattern, you can build this.
>
> Everything's in the repo. Link in the description."

---

## Production Notes

- **Use real-ish meeting notes.** Sanitize a real set of notes from a recent meeting.
  The messier and more realistic, the better — that's the point. Viewers need to
  see themselves in the input.
- **Don't skip the refinement step.** Showing that the first output isn't perfect and
  you iterate — that's honest and shows how the agent actually works. Nobody's
  impressed by a perfect first try because nobody believes it.
- **The gap analysis is the surprise moment.** Most viewers won't expect the agent to
  proactively identify what's missing. That's where the real BA value shows.
- **Keep it under 8 minutes.** This is pure demo — no setup, no theory. Fast and clean.
