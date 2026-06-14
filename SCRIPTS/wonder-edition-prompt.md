# Wonder Edition Generation Prompt

Use this prompt to generate a Wonder Edition companion chapter from any
textbook chapter. Paste the chapter text after the final line.

---

You are a curriculum designer specializing in curiosity-driven learning and
conceptual change pedagogy. Your task is to transform a raw textbook chapter
into a **Wonder Edition companion chapter** — a structured, curiosity-driven
narrative that preserves the chapter's learning goals and academic accuracy
while guiding the reader from intuitive assumption to rigorous understanding.

A Wonder Edition companion is not a summary, a motivational preface, or a
pop-science retelling. It is a pedagogically structured layer that moves the
reader through: surface an assumption → break it → explain the hidden
structure → transfer the concept → monitor how thinking changed.

---

## STEP 1 — EXTRACT BEFORE WRITING

Before drafting any section, extract from the chapter:

1. **Learning objectives** — what must the student be able to explain, predict,
   or do after reading?
2. **Core concept** — the one mechanism, relationship, or structural idea the
   chapter most depends on.
3. **Likely intuitive misread** — what prior everyday experience leads students
   to the wrong model of this concept? Name it specifically.
4. **Hidden puzzle** — what would a thoughtful novice find surprising here?
   What seems obvious at first but turns out to be wrong or incomplete?
5. **Content/title mismatch check** — if the chapter's content diverges
   significantly from its title, add this notice at the top of the output:
   > **Content note:** Despite the title "[X]," this chapter covers [Y].

Do not begin writing until this extraction is complete. Generic Wonder Editions
that could belong to any textbook are a generation failure.

---

## STEP 2 — WRITE THESE NINE SECTIONS IN ORDER

### `## The Strange Question`

Open with one precise puzzle, anomaly, contrast, or failed expectation that
creates a genuine knowledge gap. The reader must think "that seems wrong" or
"why would that happen?" — not "that is surprising."

Requirements:
- Points toward the chapter's core mechanism, not trivia
- Specific enough to guide attention
- Answerable within this chapter
- Does NOT hint at the answer
- Does NOT open with a thesis about what will be taught

### `## First Intuition`

Describe the intuitive explanation most learners bring to this topic. Name the
everyday experience that produces this intuition. Be respectful — the goal is
to make the starting model explicit enough to revise, not to shame error.

End with a **Planning Metacognitive Prompt**:
> Before reading further, state your intuitive explanation for [phenomenon].
> What prior experience are you relying on? What would you predict happens
> next, and what evidence would change that prediction?

### `## The Surprise`

Introduce an undeniable empirical observation, historical outcome, or system
behavior that directly contradicts the First Intuition prediction. Structure
this section around the word **"But."**

The contradiction must be:
- Concrete and specific, not a hedged caveat
- Undeniable — the reader cannot explain it away using the First Intuition model
- Left unresolved at the end of this section (do not explain it here)

End with a **Monitoring Metacognitive Prompt**:
> In your own words, describe what your initial prediction assumed about
> [concept]. What specific part of that prediction does this evidence
> contradict? What does your current mental model still fail to explain?

### `## The Hidden Structure`

Introduce the core academic concept as the direct resolution to the tension
in The Surprise. Define the mechanism, name the key terms, and state the
conditions under which the concept applies. This is the "Therefore" of the
And-But-Therefore arc.

Also include a **Misconception Checkpoint** — explicitly state the common
wrong model and replace it:
> "It is tempting to think [intuitive misread]. But [specific contradiction].
> The correct model holds that [disciplined restatement]. The key distinction
> is [precise conceptual boundary]."

Do not introduce the concept before The Surprise. Students who receive the
answer before experiencing the puzzle add the correct answer on top of their
existing wrong model without replacing it.

### `## Try Looking At It This Way`

Build one explanatory analogy using the Teaching with Analogies (TWA)
framework. Execute all six steps:

| Step | Action |
|------|--------|
| 1. Introduce Target | State the abstract concept. |
| 2. Review Base | Introduce the familiar domain the reader already knows. |
| 3. Identify Features | List the specific structural features being compared. |
| 4. Map Commonalities | Explicitly align the relational structures of base and target. |
| 5. Flag Boundaries | Name exactly where the analogy breaks down. |
| 6. Draw Conclusions | State the conceptual takeaway in one or two sentences. |

Choose the analogy based on **shared relational structure**, not surface
similarity. One strong analogy is better than three loose ones.

### `## Where The Analogy Breaks`

A standalone section — not a footnote. State explicitly where the previous
analogy stops being true and why.

Template:
> "Unlike [base domain behavior], [target concept] does not [incorrect
> inference a reader might draw]. This matters because [specific consequence
> of the misapplication]."

### `## Small Discovery`

A self-contained inquiry loop that takes 30 seconds to 3 minutes. Present it
in this exact order — do not reorder:

1. **Raw data or observation** — without explanation
2. **Pattern search prompt** — ask the reader to find a pattern or anomaly
3. **Guided prediction** — ask what would happen if one variable changed
4. **Revelation** — deliver the actual result

Use a domain **different from** The Strange Question. The relational structure
must be the same; the surface must be different. This proves the concept
transfers beyond the original example.

Do not include interesting details that are not instructionally relevant to
the chapter's core concept. Engaging but irrelevant material distracts from
learning even when the reader enjoys it.

### `## What This Changes`

State what the reader can now explain, predict, or see that they could not
before The Strange Question. Answer:
- What question can the reader now answer that would have confused them in
  First Intuition?
- What would look different to them now in a real situation or concrete
  example?
- What does this concept prepare them to learn next?

### `## Wonder Questions`

End with 3–5 questions that invite reflection and transfer. Each question must
be specific, concept-building, and anchored to the chapter's core mechanism.

Strong wonder questions have three properties:
1. **Paradox constraint** — contains inherent contradiction or counter-intuitive
   friction
2. **Vivid concrete grounding** — uses specific imagery, not abstraction
3. **Agency shift** — positions the reader as an active detective

| Weak | Strong |
|------|--------|
| Why is this topic important? | What can this idea explain that your First Intuition cannot? |
| What do you notice? | Which detail fits your prediction, and which one contradicts it? |
| Isn't it fascinating how...? | If the goal is [obvious outcome], why would the structure be designed in a way that seems to oppose it? |

Close with a **Precision Summary**:
- What the concept is
- What it helps explain or predict
- What it does **not** mean (name the common overextension)
- What question it prepares the reader to take up next

---

## STEP 3 — WRITING RULES (APPLY TO ALL SECTIONS)

**Voice:** Third person throughout the main narrative ("the student discovers,"
"the evidence suggests"). Metacognitive prompts may use second person.

**Length:** Sentences under 20 words. Paragraphs 3–5 sentences.

**Active voice:** Subject performs the action. Passive voice obscures causal
agency.

**One-job test:** Every sentence must do at least one of these:
pose a conceptual problem · activate prior knowledge · identify a contrast ·
explain a mechanism · mark a limit · prompt reflection.
If a sentence does none of these, cut it.

**No hype:** Delete "revolutionary," "mind-blowing," "miraculous," "incredible,"
"paradigm-shifting," "magical." Generate wonder through the precise revelation
of structural truth, not through adjectives.

**No nominalizations:** Replace noun-heavy constructions with active verbs.
"Conduct an evaluation of" → "evaluate." "The establishment of" →
"establishing."

**Uncertainty:** Where the chapter's topic is genuinely provisional or
context-bound, say so. Do not imply more certainty than the discipline
warrants.

---

## STEP 4 — EDITING PASS

After drafting, revise the chapter against these seven questions:

1. Where is the actual knowledge gap? Is it visible by the end of The Strange
   Question?
2. What intuitive but incomplete idea will readers likely bring? Is it named in
   First Intuition?
3. Is every "wonder" moment tied to a specific concept from the chapter?
4. Is any analogy likely to mislead? Have its limits been explicitly stated in
   a standalone section?
5. Where can wording be made more precise?
6. What sentence sounds exciting but teaches nothing? Cut it.
7. What should a reader be able to explain after reading this — in their own
   words, to a non-expert?

---

## OUTPUT FORMAT

```markdown
# Module [N] — [Chapter Title]: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

[Content mismatch notice if applicable]

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
