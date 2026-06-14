# Wonder Edition Generation Prompt

Use this prompt to generate a Wonder Edition companion chapter from any
textbook chapter. Paste the chapter text after the final line.

A Wonder Edition companion is not a summary, a motivational preface, or a
pop-science retelling. It is a pedagogically structured layer that moves the
reader through a precise arc: surface an assumption → break it → explain the
hidden structure → ground it in code or practice → transfer it to a new
domain → monitor how thinking changed.

**Generation failure modes to avoid:**
- A companion that could belong to any chapter in any textbook (too generic)
- A companion that describes but does not challenge (no genuine puzzle)
- A companion whose analogy fits the surface but not the mechanism
- A companion whose "wonder" stays conceptual and never touches what the
  student actually does with the code

---

## STEP 0 — ALIGNMENT CHECK (do this before everything else)

Read the chapter title and the first three paragraphs of the chapter body.

**Ask:** Does the chapter's actual content match its title? Even partially
misaligned titles disorient students. Apply a low threshold — if the chapter's
primary concept is not what the title names, add the notice below at the top of
the output, immediately after the standard header.

> **Content note:** Despite the title "[module title]," this chapter covers
> [actual content]. This companion follows the actual chapter content.

**Do not skip this check.** A content note costs one line. A missing note
leaves a student wondering why the chapter they opened does not match what they
were told to study.

---

## STEP 1 — EXTRACT BEFORE WRITING

Before drafting any section, extract and record:

1. **Learning objectives** — what must the student be able to explain, predict,
   or do after reading? State these as actions, not topics ("distinguish X from Y
   in a running program," not "understand X").

2. **Core concept** — the one mechanism, relationship, or structural idea the
   chapter most depends on. If you cannot name it in one sentence, you have not
   found it yet.

3. **Likely intuitive misread** — what specific prior everyday experience causes
   students to arrive with the wrong model? Name the experience, not just the
   error ("because spreadsheet cells are independent copies" not "students think
   objects are independent").

4. **Hidden puzzle** — the thing that seems obvious at first but turns out to be
   wrong or incomplete when examined carefully. This becomes The Strange Question.

5. **Concrete code moment** — one short snippet (3–10 lines) or one traceable
   execution sequence that makes the core concept visible and verifiable. A
   student should be able to run or trace it in under two minutes.

6. **Practical task** — what the student will actually do in their project using
   this concept. "Design the Checkout handler to delegate, not execute" is
   practical. "Understand polymorphism" is not.

Do not begin writing until this extraction is complete.

---

## STEP 2 — WRITE THESE NINE SECTIONS IN ORDER

---

### `## The Strange Question`

Open with one precise puzzle, anomaly, or failed expectation that creates a
genuine knowledge gap. The reader must think "that seems wrong" or "why would
that happen?" — not "that is surprising" or "I wonder what comes next."

Requirements:
- Points toward the chapter's core mechanism, not trivia or vocabulary
- Specific enough that a student knows exactly what to look for
- Answerable within this chapter — the puzzle resolves inside the companion
- Does NOT hint at the answer
- Does NOT open with a thesis about what will be taught

If the chapter covers code, the Strange Question should involve a specific
observable code behavior — a result that contradicts expectation, a bug that
has no visible cause, a design that looks redundant but turns out to be
necessary.

---

### `## First Intuition`

Describe the intuitive explanation most learners bring. Name the everyday
experience that produces it. Be precise: name the source domain ("this feels
right because spreadsheet cells work that way"), not just the wrong belief.

The goal is to make the starting model explicit enough to revise. A student
who cannot name their prior model cannot notice when it breaks.

End with a labeled **Planning Metacognitive Prompt** using this format:

> **► Planning prompt:** Before reading further, [ask the student to state
> their current model, name their prior experience, and predict a specific
> outcome]. Write it down before continuing.

---

### `## The Surprise`

Introduce an undeniable fact, system behavior, or concrete observation that
directly contradicts the First Intuition prediction. Structure this section
around the word **"But."**

The contradiction must be:
- Concrete and specific — name the exact output, behavior, or result
- Undeniable — the reader cannot explain it away with the First Intuition model
- Left unresolved at the end of this section — do not explain it here

If the chapter covers code, the Surprise should show the unexpected output or
behavior directly. A student who can see the exact failure has no escape from
the contradiction.

End with a labeled **Monitoring Metacognitive Prompt** using this format:

> **► Monitoring prompt:** In your own words, describe what your initial
> prediction assumed about [concept]. What specific part does this evidence
> contradict? What does your current model still fail to explain?

---

### `## The Hidden Structure`

Introduce the core academic concept as the direct resolution to the tension
in The Surprise. Open with "Therefore" or an equivalent that signals this
section answers the puzzle. Define the mechanism, name the key terms, and state
the conditions under which the concept applies.

**Required: Misconception Checkpoint.** Explicitly state the wrong model and
replace it using this exact four-part template:

> "It is tempting to think [intuitive misread]. But [specific contradiction
> from The Surprise]. The correct model holds that [disciplined restatement].
> The key distinction is [the precise boundary that separates the wrong model
> from the correct one]."

All four parts are required. The fourth part ("The key distinction is…") is
the most commonly omitted and the most important: it names the exact line
between the old model and the new one.

**Required: Code Trace or Concrete Example.** Include a short snippet (3–10
lines) or a step-by-step execution trace that makes the mechanism visible.
Label it clearly. A student should be able to read it and confirm the concept
holds. This grounds the abstract explanation in something verifiable.

Do not introduce the concept before The Surprise. Students who receive the
answer before experiencing the puzzle add the correct answer on top of their
existing wrong model without replacing it.

---

### `## Try Looking At It This Way`

Build one explanatory analogy using the Teaching with Analogies (TWA)
framework. All six steps are mandatory and must be labeled using the exact
headings below. Prose that covers the steps without labeling them is not
sufficient — the labels allow a reader to verify each step was taken.

**Target:** [State the abstract concept being taught.]

**Base:** [Introduce the familiar domain the reader already knows.]

**Features:** [List the specific structural features being compared — at least
three. Use parallel phrasing: "the X in the base corresponds to the Y in the
target."]

**Commonalities:** [Explicitly map the relational structure of the base onto
the target. For each mapping, state why the structural relationship is the
same, not just that the names correspond.]

**Boundaries:** [Name exactly where the analogy stops being accurate. At least
one boundary is required. Do not bury this in the next section — state it here
so the reader knows the limit before finishing the analogy.]

**Conclusions:** [State the conceptual takeaway in one or two sentences.]

Choose the analogy based on **shared relational structure**, not surface
similarity. One strong analogy is better than three loose ones. Reject an
analogy that fits the vocabulary but not the mechanism.

---

### `## Where The Analogy Breaks`

A standalone section — not a footnote, not a parenthetical. State explicitly
where the previous analogy stops being true and why this specific failure
matters.

Use this template as the anchor sentence:

> "Unlike [base domain behavior], [target concept] does not [incorrect
> inference a reader might draw]. This matters because [specific consequence
> of applying the analogy past its limit]."

One precise, high-stakes limit is more useful than a list of minor caveats.
Choose the boundary most likely to mislead a student who over-applies the
analogy.

---

### `## Small Discovery`

A self-contained inquiry loop that takes 30 seconds to 3 minutes. This section
proves the core concept transfers beyond the original example by applying it to
a domain with different surface content but the same relational structure.

**Domain rule:** For a programming or computer science course, the domain must
be entirely outside programming and computing. Acceptable domains: cooking,
logistics, architecture, law, biological systems, manufacturing, weather,
finance, medicine, sports. A second programming example does not qualify —
even a different language or paradigm. If the Strange Question involves code
behavior, the Small Discovery must involve an entirely non-code scenario.

Present in this exact order. Do not reorder. Do not reveal before the
prediction step.

1. **Raw data or observation** — present without any explanation. A table, a
   scenario, a sequence of measurements, or a short narrative. The student
   should be able to engage with it directly.

2. **Pattern search** — ask the student to find a pattern or anomaly in the
   raw data. One specific, answerable question.

3. **Prediction** — ask the student what would happen if one variable changed.
   End with an explicit direction to write the answer before continuing. Add a
   visual separator (three dashes `---`) after the prediction prompt.

4. **Revelation** — deliver the actual result and connect it explicitly to the
   chapter's core concept. Name the concept by name. Do not let the connection
   remain implicit.

---

### `## What This Changes`

State what the reader can now explain, predict, or do that they could not
before The Strange Question. Be concrete and specific.

Answer all four of these:

1. What question can the reader now answer that would have confused them in
   First Intuition? (Name the question.)

2. What would look different to them now in a specific piece of real code or a
   real design decision? (Name the code or decision.)

3. **Practice Bridge:** What can the student now do in their project that they
   could not do correctly before? Name the specific task — a method to write,
   a design decision to make, a bug to diagnose. This is the most important of
   the four. If you cannot name a specific practical action, the concept was not
   grounded in the chapter's actual learning objectives.

4. What question does this concept leave open, and which module or concept
   addresses it next?

---

### `## Wonder Questions`

End with 3–5 questions that invite reflection and transfer. Each question must
be anchored to the chapter's core mechanism, not to the course in general.

Strong wonder questions have three properties:
1. **Paradox friction** — contains a contradiction or counter-intuitive element
2. **Concrete grounding** — names specific code, a specific situation, a
   specific person making a decision — not an abstraction
3. **Agency shift** — positions the reader as someone making a choice or
   finding a cause, not as an observer

| Weak | Strong |
|------|--------|
| Why is this important? | If both programs produce the same output, what question reveals which one will fail at scale? |
| What do you notice? | The test passes but the requirement is violated. What kind of error is this, and what would catch it? |
| Isn't it interesting that…? | If the handler's job is only coordination, what is the minimum evidence that a given handler is doing its job correctly? |

Close with a **Precision Summary** containing all four parts:

> **What the concept is:** [definition in one sentence]
>
> **What it explains:** [two or three specific things this concept accounts for
> that the First Intuition model could not]
>
> **What it does NOT mean:** [name the most common overextension or
> misapplication of the concept]
>
> **What comes next:** [the specific question or concept this chapter prepares
> the student to take up next]

All four parts are required. A Precision Summary missing any part is incomplete.

---

## STEP 3 — WRITING RULES (apply to all sections)

**Voice:** Third person throughout the main narrative. Metacognitive prompts
and direct instructions to the reader may use second person.

**Length:** Sentences under 20 words. Paragraphs 3–5 sentences. Sections
should vary in length and rhythm — a chapter where every section is three
paragraphs of five sentences feels generated, not written.

**Active voice:** Subject performs the action. "The JVM dispatches the call"
not "the call is dispatched."

**One-job test:** Every sentence must do at least one of these:
pose a conceptual problem · activate prior knowledge · identify a contrast ·
explain a mechanism · mark a limit · prompt reflection.
If a sentence does none of these, cut it.

**No hype:** Delete "revolutionary," "mind-blowing," "miraculous," "incredible,"
"paradigm-shifting," "magical." Wonder comes from the precise revelation of
structural truth, not from adjectives.

**No nominalizations:** "Conduct an evaluation of" → "evaluate."
"The establishment of" → "establishing."

**No decorative questions:** Do not open a section with a rhetorical question
that the next paragraph immediately answers. The Strange Question is the only
opening question, and it remains open for three sections.

**Uncertainty principle:** Where the chapter's topic is genuinely context-
bound or contested, say so explicitly. Do not imply more certainty than the
discipline warrants.

---

## STEP 4 — EDITING PASS

After drafting, check these ten questions. Fix anything that fails.

1. Is the knowledge gap visible by the end of The Strange Question — not hinted
   at, not implied, but visible as a specific unanswered puzzle?

2. Is the intuitive misread named in First Intuition with its source domain
   (the everyday experience that produces it)?

3. Does The Surprise use "But" and leave the puzzle unresolved? Does it include
   code or concrete evidence — not just a claim that something is wrong?

4. Does The Hidden Structure open with "Therefore" or equivalent? Does the
   Misconception Checkpoint include all four parts, including "The key
   distinction is…"? Does the Code Trace exist and correctly illustrate the
   concept?

5. Does the TWA analogy use all six labeled headings? Is the analogy chosen for
   structural similarity, not surface vocabulary?

6. Does Where The Analogy Breaks use the required template and name one high-
   stakes limit?

7. Does the Small Discovery domain avoid programming and computing entirely?
   Does it present raw data before any explanation? Does it place a visual
   separator before the Revelation?

8. Does What This Changes name a specific practical task in the Practice Bridge?
   A vague "the student can now apply this concept" is not a practical task.

9. Does the Precision Summary include all four parts?

10. Read the companion without the source chapter. Does it stand alone as a
    coherent pedagogical arc from puzzle to understanding? Could it belong to a
    different chapter? If yes, it is too generic — revise the Strange Question
    and the Code Trace to anchor it to this specific chapter.

---

## OUTPUT FORMAT

```markdown
# Module [N] — [Chapter Title]: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

[Content mismatch notice — required if title and content diverge in any
significant way. Low threshold: when in doubt, add it.]

## The Strange Question
## First Intuition
## The Surprise
## The Hidden Structure
## Try Looking At It This Way
## Where The Analogy Breaks
## Small Discovery
## What This Changes
## Wonder Questions
```

---

## CHAPTER TO TRANSFORM:

[paste chapter text here]
