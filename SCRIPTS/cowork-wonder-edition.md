# Cowork Prompt: Generate Wonder Edition Companion Chapters

---

## WHAT A WONDER EDITION IS

A Wonder Edition is a companion version of a textbook chapter that preserves
the chapter's learning goals, conceptual precision, and disciplinary standards,
but reorganizes explanation around curiosity, prediction, surprise, conceptual
tension, guided inquiry, and reflection. It is not a simplified retelling, not
a motivational preface, and not a pop-science sidecar.

It is a pedagogically structured layer that helps readers:
1. Notice a genuine information gap
2. Make an initial inference using existing intuition
3. Confront a mismatch between that intuition and reality
4. Rebuild understanding around the correct structural model
5. Monitor how their thinking changed

The design target is not "make it magical." It is: make the learner's thinking
visible, active, and revisable without compromising accuracy. Wonder is not
decoration — it is a doorway into rigorous understanding.

A Wonder Edition is especially useful when the original chapter is abstract,
concept-dense, counterintuitive, misconception-prone, or motivationally flat.
It works best for foundational ideas, model-based reasoning, threshold
concepts, and chapters students often memorize without understanding.

---

## WHEN NOT TO USE WONDER EDITION STRUCTURE

Wonder Edition structure adds extraneous cognitive load to content that does
not benefit from narrative tension. Do not apply it to:

- Safety-critical procedures that must not be ambiguous
- Purely procedural or syntactic content (keyboard shortcuts, reference tables,
  API signatures, exact command syntax)
- Content where learners have zero prior knowledge to anchor an information gap
- Any context where rhetorical buildup or deliberate ambiguity could obscure
  a precise next action

For mixed chapters (some conceptual, some procedural), apply Wonder structure
to the conceptual core and use direct exposition for the procedural steps.

---

## ROLE & CONTEXT

You are working on a university-level textbook. You have access to all chapter
files in `chapters/`. Your job is to generate a Wonder Edition companion
chapter for each textbook chapter and write it to `wonder/`.

This is a generation pass, not an extraction pass. You are writing new
companion content derived from each chapter's concepts and learning objectives
— not copying or paraphrasing sentences from the chapter.

---

## STEP 1 — IDENTIFY CHAPTERS TO PROCESS

Read the `chapters/` directory. Process every `.md` file except:

- `00-frontmatter.md`
- `99-back-matter.md`
- Any file whose name contains `exam`, `midterm`, or `back-matter`

For each chapter file, extract before writing:

1. **Chapter title and module number**
2. **Learning objectives** (stated or inferred from content)
3. **Core concepts** (the 2–4 ideas the chapter most depends on)
4. **Student misconceptions likely carried in** (everyday intuitions that
   contradict the chapter's central claim)
5. **Content/title mismatch check**: if chapter content diverges significantly
   from the chapter title, add a blockquote notice at the top of the Wonder
   file:
   > **Content note:** Despite the title "[X]," this chapter covers [Y].

---

## STEP 2 — EDITORIAL WORKFLOW (APPLY BEFORE WRITING)

Run this five-step diagnostic before drafting any section.

1. **Extract nonnegotiable learning goals.** What must the student be able to
   explain, predict, or do after this chapter?
2. **Find the hidden puzzle.** What would a thoughtful novice find surprising
   here? What seems obvious at first but turns out to be wrong or incomplete?
3. **Locate the likely intuitive misread.** What prior everyday experience
   leads students to the wrong model? Name it specifically.
4. **Choose the learner action type.** What will sharpen the concept?
   A prediction, a comparison, a near-transfer explanation, or a
   mini-application?
5. **Rewrite the structure.** Reorganize the section so the learner moves
   through: question → expectation → evidence or mechanism → revised model →
   reflection.

---

## STEP 3 — MANDATORY CHAPTER STRUCTURE

Every Wonder Edition companion chapter must follow this named section sequence.
Each section has a specific cognitive job.

```
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

### THE STRANGE QUESTION

**Cognitive job:** Open an information gap the chapter will actually resolve.

Write one precise puzzle, anomaly, contrast, or failed expectation. The
opening must make the learner think "that seems wrong" or "why would that
happen?" — not "that is surprising and interesting."

The question must:
- Point toward a real conceptual mechanism, not trivia
- Be specific enough to guide attention
- Be answerable within this chapter

**Do not** open with a thesis statement about what the chapter will teach.
**Do not** use theatrical suspense that the chapter cannot fully resolve.

**Examples of strong opening questions:**
- "How can one blueprint create many objects that each remember different
  histories?"
- "Why can a program compile perfectly and still be wrong?"
- "If printing more money creates inflation, why do governments keep doing it
  even when they can see the damage happening in real time?"

---

### FIRST INTUITION

**Cognitive job:** Surface the student's likely existing mental model before
any correction occurs.

Describe the intuitive explanation most learners bring to this topic. Do this
respectfully — the goal is not to shame error but to make the starting model
explicit enough to revise. Name the everyday experience that produces this
intuition.

End this section with a **Planning Metacognitive Prompt** that forces the
student to commit to a prediction before reading further.

**Planning Metacognitive Prompt template:**
> Before reading further, state your intuitive explanation for [phenomenon].
> What prior experience or observation are you relying on? What would you
> predict happens next, and what would prove you wrong?

---

### THE SURPRISE

**Cognitive job:** Generate productive cognitive dissonance. The student's
intuition from First Intuition must fail against an undeniable fact.

Structure this section around the narrative word **"But."** Introduce an
empirical observation, historical outcome, or system behavior that directly
contradicts the prediction made in First Intuition. The contradiction must be
concrete and undeniable — not a hedged caveat.

End this section with a **Monitoring Metacognitive Prompt** that asks the
student to articulate the friction between their old model and the new
evidence.

**Monitoring Metacognitive Prompt template:**
> In your own words, describe what your initial prediction assumed about
> [concept]. What specific part of that prediction does this new evidence
> contradict? What does your current mental model still fail to explain?

**Critical: do not resolve the tension here.** Let the gap breathe. If the
surprise and the explanation appear in the same section, the student's brain
learns that active cognitive effort is unnecessary.

**And-But-Therefore (ABT) checkpoint:**
- The Strange Question and First Intuition set up the "And" — familiar
  context, accepted assumption.
- The Surprise delivers the "But" — the contradiction that breaks the
  assumption.
- The Hidden Structure delivers the "Therefore" — the concept that resolves
  the tension.
- If there is no genuine "But," the chapter lacks narrative structure. Find
  the contradiction before writing.

---

### THE HIDDEN STRUCTURE

**Cognitive job:** Introduce the core academic concept as the direct
resolution to the tension in The Surprise.

Define the key idea, name the mechanism, and state the conditions under which
it applies. Keep the prose lean. This section provides the "Therefore" of the
ABT arc.

**Do not** introduce the concept before The Surprise. Students who receive the
answer before experiencing the puzzle have no reason to update their mental
model — they simply add the correct answer to their existing wrong model
without replacing it.

---

### TRY LOOKING AT IT THIS WAY

**Cognitive job:** Make the new concept intelligible and plausible through
structured analogy.

Build one explanatory analogy using the **Teaching with Analogies (TWA)**
framework. Execute all six steps:

| TWA Step | What to Write |
|----------|---------------|
| 1. Introduce Target | State the abstract concept clearly. |
| 2. Review Base | Introduce the familiar domain the student already knows. |
| 3. Identify Features | List the specific structural features being compared. |
| 4. Map Commonalities | Explicitly align the relational structures of base and target. |
| 5. Flag Boundaries | Name the precise points where the analogy breaks down. |
| 6. Draw Conclusions | Synthesize into a clear conceptual statement. |

Choose analogies based on **shared relational structure**, not surface
similarity. An analogy based on how two things look rather than how their
systems work will create persistent misconceptions.

One strong analogy is better than three loose ones. If the analogy is doing
too much explanatory work, it is probably hiding a weak explanation.

---

### WHERE THE ANALOGY BREAKS

**Cognitive job:** Prevent students from over-extending the analogy in The
previous section into domains where it no longer holds.

This is a standalone section, not a footnote. State explicitly where the
analogy from "Try Looking At It This Way" stops being true.

**Template:**
> "Unlike [base domain behavior], [target concept] does not [incorrect
> inference a student might draw]. This matters because [specific consequence
> of the misapplication]."

Systematically neutralize three failure modes:

1. **Surface seduction**: The analogy was chosen because two things look
   similar, not because they share relational structure. Name any attribute of
   the base domain that does NOT transfer.
2. **Inert encoding**: The student memorizes the analogy as a specific example
   rather than a transferable schema. To prevent this, provide a second,
   different base domain that maps to the same concept — stripping away
   surface features to reveal the shared structure.
3. **Unbounded application**: No boundary is stated. Every analogy breaks down
   at some threshold of scale, material, or complexity. Name it.

---

### SMALL DISCOVERY

**Cognitive job:** Turn explanation into participation. Create a felt "I see
it now" moment.

A small discovery is a self-contained inquiry loop that takes 30 seconds to
3 minutes. It is not a workbook exercise and not a quiz. It requires exactly
one meaningful act: predict an outcome, rank alternatives, choose the better
explanation, locate the mismatch, fill in a missing step, or apply the concept
to a near-transfer case.

**Structure every discovery in this order (do not reorder):**
1. **Raw data or observation** — present without explanation.
2. **Pattern search** — prompt the student to find a pattern or anomaly.
3. **Guided prediction** — ask what would happen if one variable changed.
4. **Revelation** — deliver the actual result. Confirm emerging intuition or
   expose a lingering misconception.

The discovery domain should be **different** from the one used in The Strange
Question. The relational structure must be the same; the surface must be
different. This proves the concept is transferable, not just a local answer
to one specific puzzle.

**Seductive details warning:** Do not include interesting details that are not
instructionally relevant to the chapter's core concept. Interesting but
irrelevant material distracts from learning even when it is engaging.

---

### WHAT THIS CHANGES

**Cognitive job:** Make explicit what students can now see, explain, or do
that they could not before reading this chapter.

This is not a summary. It is a statement of upgraded capacity. Answer:
- What question can the student now answer that would have confused them in
  First Intuition?
- What would look different to them now in a real situation, a piece of code,
  a text, or a data set?
- What does this concept prepare them to learn next?

---

### WONDER QUESTIONS

**Cognitive job:** Invite reflection and transfer. End the chapter with
3–5 questions that are specific, concept-building, and answerable from the
chapter — not generic or open-ended.

Strong wonder questions have three properties:
1. **Paradox constraint**: Contains inherent contradiction or counter-intuitive
   friction.
2. **Vivid concrete grounding**: Uses specific imagery, not abstract
   generalization.
3. **Agency shift**: Positions the student as an active detective — "How is
   that even possible?" not "What did you learn?"

**Weak vs. strong contrasts:**

| Weak | Strong |
|------|--------|
| Isn't it amazing how complex this topic is? | What pattern would you expect here, and what single case would force you to revise that expectation? |
| Why is this topic important? | What can this idea explain that your First Intuition cannot? |
| What do you notice? | Which detail fits your prediction, and which one contradicts it? |
| What is the function of [X]? | If the goal is [obvious outcome], why would the structure be designed in a way that seems to oppose that goal? |

---

### PRECISION SUMMARY (APPEND AT END OF WONDER QUESTIONS)

Close every chapter by naming the core idea in disciplined language. State:
- What the concept is
- What it helps explain or predict
- What it does **not** mean (common overextension)
- What question it prepares the learner to take up next

The "does not mean" element is required. Every chapter's core concept has a
common misapplication. Name it before the student encounters it.

---

## STEP 4 — MANDATORY WRITING RULES

These rules govern all phases. Violations degrade rigor and pedagogical
effectiveness.

### Voice and Person
- Write in **third person** throughout the main narrative.
  Use: "the student discovers," "the evidence suggests," "the analysis shows."
  Never use: "I," "we," "our" in the main narrative.
- Metacognitive prompts directed at the student may use second person
  ("Before reading further, state your prediction...").

### Sentence and Paragraph Length
- Sentences: **under 20 words**.
- Paragraphs: **3–5 sentences**.
- Subject and verb must be close together.

### Active Voice
- Use active constructions. Passive voice obscures causal agency.
  - Weak: "The temperature was reduced by the thermostat."
  - Strong: "The thermostat reduces the temperature."

### The One-Job Editorial Test
Every sentence must do at least one of these jobs:
- Pose a conceptual problem
- Activate relevant prior knowledge
- Identify a contrast
- Explain a mechanism
- Mark a limit
- Prompt reflection

If a sentence does none of these, cut it. Prose that sounds interesting but
does no cognitive work is extraneous load.

### Eliminating Nominalizations
Replace noun-heavy constructions with active verbs.

| Replace | With |
|---------|------|
| conduct an evaluation of | evaluate |
| make a determination about | determine |
| reach an understanding of | understand |
| the establishment of guidelines | establishing guidelines |
| the generation of output | generating output |

Scan for words ending in `-tion`, `-ment`, `-ence`, `-ity`, `-ance`. Most
can be replaced with a direct verb.

### Eliminating Hype and Empty Superlatives
Wonder is generated by mechanical precision, not adjectives. Delete all of
the following and demonstrate the mechanism instead:

| Delete | Replace with |
|--------|--------------|
| revolutionary | [demonstrate the mechanism] |
| mind-blowing / mind-boggling | [demonstrate the mechanism] |
| miraculous / magical | [demonstrate the mechanism] |
| incredible / amazing | [demonstrate the mechanism] |
| paradigm-shifting | [demonstrate the mechanism] |
| approximately | about |
| subsequently | then |
| utilize / facilitate | use / make |
| completely eliminate | eliminate |
| already existing | existing |

### Be Honest About Uncertainty
State clearly what is known, what is provisional, and what the student should
conclude now. Overstating confidence makes a passage feel satisfying in the
moment but distorts what the learner is actually supposed to know. Where the
chapter's topic is genuinely contested or context-bound, say so.

### Relevance Without Pandering
Show what the concept helps a learner explain, predict, compare, interpret,
or do. Do not bolt on "real-world" relevance as a sentimental aside. Relevance
should clarify purpose — not decorate the topic with enthusiasm.

---

## STEP 5 — METACOGNITIVE REFLECTION PROMPTS

Embed three types of prompts at structurally precise moments — not gathered
into a list at the end.

**Planning prompts** (in First Intuition):
> "Before reading further, what is your intuitive explanation for this
> phenomenon? What prior experience are you relying on? What would prove you
> wrong?"

**Monitoring prompts** (in The Surprise and The Hidden Structure):
> "What part of your first model still seems plausible, and what part now
> fails to account for this evidence?"

**Evaluation prompts** (in What This Changes and Wonder Questions):
> "What specific evidence or analogy changed your understanding? Where would
> this explanation not apply?"

> "If you had to teach this to someone with no background in [field], what
> analogy would you choose, and what warning would you add about where that
> analogy breaks down?"

Generic prompts ("reflect on your learning," "what did you find interesting")
do not engage metacognitive regulation. Prompts must target specific evidence,
specific strategy choices, or specific remaining gaps.

---

## STEP 6 — MISCONCEPTION CHECKPOINT (REQUIRED)

Every Wonder Edition chapter must include an explicit refutation moment:
state the common intuitive misunderstanding, then correct it directly.
Research on refutation text shows that explicitly naming and correcting a
misconception produces meaningfully better learning than presenting only the
correct model.

**Template:**
> "It is tempting to think [intuitive misread]. But [specific contradiction].
> The correct model holds that [disciplined restatement]. The key distinction
> is [precise conceptual boundary]."

This is separate from the analogy boundary. The misconception checkpoint
targets the intuitive misread students bring from everyday experience. The
analogy boundary targets the inferential errors students might draw from the
analogy itself.

---

## STEP 7 — DISCIPLINARY ADAPTATION

Adapt the narrative arc strategy to the chapter's academic domain.

| Domain | Primary Source of Wonder | Primary Misconception | Narrative Arc |
|--------|--------------------------|-----------------------|---------------|
| STEM | Hidden mechanisms, counter-intuitive natural laws, scale shifts, boundary conditions | Everyday physical misconceptions | Mechanism Decoupling: deconstruct a familiar process to reveal a surprising underlying force; use diagrams with tight signaling and explicit misconception checkpoints |
| Humanities | Competing interpretations, the contingency of historical events, concepts that shift meaning across contexts | Hindsight bias ("it was inevitable"); single-cause explanation | Alternative Futures: reconstruct a pivotal decision to show how easily the outcome could have been different; foreground competing values, voice, context, evidence trails |
| Social Sciences | Invisible systemic forces, counter-intuitive collective behavior, the gap between individual intent and aggregate outcome | Individualistic bias ("it's just individual choices") | The Emergent Paradox: show how rational individual choices produce irrational collective outcomes; center the move from anecdote to explanatory model |
| Professional / Technical | Expert diagnostic intuition, elegant system failure modes, judgment under complexity | Illusion of procedural linearity ("just follow the checklist") | System Autopsy: trace a catastrophic failure back to a small, overlooked coupling; use cases, near misses, diagnostic contrasts, and "what would you do next?" prompts — technical accuracy remains primary |

---

## STEP 8 — COMMON MISTAKES

**Mistake 1 — Replacing clarity with tone**
The companion becomes inspirational prose with no conceptual work. Adjectives
do the work that mechanisms should do.

**Mistake 2 — Too many questions, too few answers**
Rhetorical questions accumulate without resolution. The student learns that
questions in this text need not be taken seriously.

**Mistake 3 — Pre-answering (The Explanatory Rush)**
A wonder question is asked and answered in the next paragraph. The student's
brain learns that active engagement is unnecessary. Allow at least one full
section between question and resolution.

**Mistake 4 — Surface analogy mapping**
An analogy is chosen because two things look similar. The shared relational
structure is never mapped, and the limits are never flagged. Use the TWA
framework for every analogy.

**Mistake 5 — Delaying definitions too long**
Key terms are withheld so long that learners build an incorrect model before
the correction arrives. Surface the intuitive misread, then correct it within
the same section.

**Mistake 6 — Mistaking activity for guidance**
Every inquiry step is pre-answered or over-scaffolded. The student has no
genuine prediction to make. Leave at least one step in Small Discovery
genuinely open before revealing the result.

**Mistake 7 — Emotional reflection prompts**
Reflection questions ask only "How did this make you feel?" or "What was
interesting?" These do not engage metacognitive regulation. Prompts must ask
for evidence, explanation, or strategy.

**Mistake 8 — Seductive details**
Interesting but irrelevant facts are included because they are engaging. These
distract from the chapter's core concept even when the student enjoys them.
Every detail must serve the chapter's learning objectives.

---

## STEP 9 — PRE-PUBLICATION CHECKLIST

| Category | Checklist Item | Status |
|----------|---------------|--------|
| Learning goals | Original learning objectives and factual content are preserved. | [ ] |
| Information gap | The opening creates a real conceptual gap, not generic excitement. | [ ] |
| ABT structure | A genuine "But" introduces an undeniable contradiction — not a soft transition. | [ ] |
| First intuition | A prediction prompt appears before any academic content is introduced. | [ ] |
| Misconception checkpoint | At least one common intuitive misunderstanding is named and explicitly corrected. | [ ] |
| Analogy rigor | Every analogy uses all six TWA steps; "Where The Analogy Breaks" is a standalone section. | [ ] |
| Small discovery | Data or observations are presented before explanation; order is data → pattern → prediction → revelation. | [ ] |
| Seductive details | Every interesting detail is instructionally relevant to the chapter's core concept. | [ ] |
| One-job test | Every sentence poses a problem, activates prior knowledge, identifies a contrast, explains a mechanism, marks a limit, or prompts reflection. | [ ] |
| Precision summary | The close states what the concept is, what it explains, what it does NOT mean, and what question it prepares the learner for next. | [ ] |
| Metacognitive prompts | Planning prompt in First Intuition, monitoring prompt in The Surprise, evaluation prompt in What This Changes. | [ ] |
| Active voice | No passive constructions obscuring causal agency. | [ ] |
| No nominalizations | No `-tion`/`-ment`/`-ence`/`-ity` noun-verb constructions that could be direct verbs. | [ ] |
| No hype | No "revolutionary," "miraculous," "mind-blowing," or empty superlatives anywhere in the text. | [ ] |
| Uncertainty | Provisional or context-bound claims are flagged as such. | [ ] |
| Third-person prose | Main narrative uses third person throughout (metacognitive prompts may use second person). | [ ] |

---

## STEP 10 — OUTPUT FORMAT

Write each Wonder Edition companion to `wonder/[chapter-filename].md`.

Use this file header:

```markdown
# Module [N] — [Chapter Title]: Wonder Edition
## Companion Chapter

> **Wonder Edition:** This companion transforms Module [N]'s core concepts
> into a curiosity-driven narrative. Read it alongside the chapter, not
> instead of it.

[Content mismatch notice if applicable]
```

Use these H2 section headers in order:

```
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

End each file with:

```markdown
---
## Author Notes

**Core misconception targeted:** [State the primary intuitive assumption this
chapter disrupts.]

**Analogy base domain:** [Name the base domain used and the specific boundary
that was flagged.]

**Bloom's arc:** The Strange Question (Remember) → The Surprise (Analyze) →
The Hidden Structure (Understand/Apply) → Small Discovery (Apply/Evaluate) →
What This Changes (Evaluate/Create)
```

---

## UNIVERSAL GENERATION PROMPT

Use this system prompt when generating a Wonder Edition chapter with an LLM.
Append the raw chapter content after the final line.

---

Create a "Wonder Edition" companion for the textbook chapter provided below.

**Goal:**
Write a companion chapter that preserves the original learning objectives,
conceptual accuracy, and disciplinary rigor while increasing curiosity,
surprise, intuition, and conceptual fascination.

**Nonnegotiable constraints:**
- Do not invent facts, examples, claims, or citations not supported by the
  source chapter.
- Do not simplify away necessary precision.
- Do not become vague, flowery, inspirational, or theatrical.
- Keep the style engaging but intellectually serious.
- Treat this as a companion, not a replacement.

**Voice and style rules:**
- Write in third person in all main narrative sections. Never use "I," "we,"
  "our" in the main narrative. Metacognitive prompts may use second person.
- Keep sentences under 20 words and paragraphs to 3–5 sentences.
- Use active voice. Minimize nominalizations.
- Every paragraph must do at least one clear job: pose a problem, state a
  contrast, explain a mechanism, mark a limit, or prompt reflection.
- Delete any sentence that sounds interesting but teaches nothing.

**Output structure:**
Use these sections in order:

`## The Strange Question` — One precise puzzle, anomaly, or failed expectation
that creates a real conceptual gap.

`## First Intuition` — The intuitive explanation most learners bring. End with
a planning metacognitive prompt asking for a prediction.

`## The Surprise` — The undeniable empirical contradiction. Structure around
"But." End with a monitoring metacognitive prompt.

`## The Hidden Structure` — The core academic concept as the direct resolution
to the tension. Define the mechanism clearly.

`## Try Looking At It This Way` — One bounded analogy using the TWA framework:
introduce target, introduce base, map relational features, state where the
analogy breaks down.

`## Where The Analogy Breaks` — Standalone section. State explicitly where
the analogy stops being true and why.

`## Small Discovery` — A self-contained 30-second to 3-minute inquiry loop in
a different domain: data → pattern search → guided prediction → revelation.
Do not reveal the result before the prediction.

`## What This Changes` — What the student can now explain, predict, or see
that they could not before. State one thing the chapter prepares them to
learn next.

`## Wonder Questions` — 3–5 questions that are specific, concept-building, and
anchored to the chapter's core mechanism. End with a precision summary:
what the concept is, what it explains, what it does NOT mean, and what it
prepares the learner for next.

**Additional requirements:**
- Surface at least one common misconception and correct it explicitly
  (refutation text: name the wrong model, then replace it).
- Include one planning prompt, one monitoring prompt, and one evaluation
  prompt — placed at their structural positions, not gathered at the end.
- Keep every interesting detail instructionally relevant. Cut seductive details
  that do not serve the chapter's learning objectives.
- Communicate uncertainty honestly where the topic requires it.

**Editing pass — after drafting, revise against these seven questions:**
1. Where is the actual knowledge gap? Is it visible by the end of The Strange
   Question?
2. What intuitive but incomplete idea will readers likely bring? Is it named in
   First Intuition?
3. Is every "wonder" moment tied to a specific concept from the chapter?
4. Is any analogy likely to mislead? Have its limits been explicitly stated?
5. Where can wording be made more precise?
6. What sentence sounds exciting but teaches nothing? Cut it.
7. What should a student be able to explain after reading this — in their own
   words, to a non-expert?

**Chapter to translate:**
[paste chapter text here]
