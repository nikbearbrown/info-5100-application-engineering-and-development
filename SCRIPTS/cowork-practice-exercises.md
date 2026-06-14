# Cowork Prompt: Generate End-of-Chapter Practice Exercises for Each Chapter

---

## ROLE & CONTEXT

You are working on a university-level textbook. You have access to all chapter
files in `chapters/`. Your job is to generate a practice exercise file for each
chapter and write it to `exercises/`.

This is a generation pass, not an extraction pass. You are writing new exercise
content derived from each chapter's concepts, vocabulary, and learning
objectives — not copying or paraphrasing sentences from the chapter.

These exercises are **learning tools first, assessment tools second**. Their
purpose is to move the student from passive reading to active cognitive
engagement through retrieval, application, diagnosis, and transfer. Design
every item to teach through doing.

---

## STEP 1 — IDENTIFY CHAPTERS TO PROCESS

Read the `chapters/` directory. Process every `.md` file except:

- `00-frontmatter.md`
- `99-back-matter.md`
- Any file whose name contains `exam`, `midterm`, or `back-matter`

For each chapter file, extract before writing:

- Chapter number and title (from the filename and `# heading`)
- Stated learning objectives (explicit `## Learning Objectives` block, or
  inferred from the chapter's opening and structure)
- Core concepts (the main ideas the chapter teaches — count them; this
  determines exercise volume)
- Key vocabulary (any terms defined, bolded, or introduced)
- Named examples, cases, datasets, tools, or procedures used in the chapter
- Common misconceptions the chapter explicitly addresses or that are
  predictable from the content
- Prior chapter concepts that connect naturally to this chapter's content
  (needed for Tier 3 Synthesis questions)
- What the student can do after this chapter that they couldn't before

**Content/title mismatch check:** After extraction, verify whether the
chapter's actual content matches its filename and title. If the content
diverges significantly from the title (e.g., a chapter titled "Recursion"
whose content is actually about FXML), add this notice at the top of the
generated exercise file:

```
> **Content note:** This chapter's filename refers to [title topic], but the
> chapter content covers [actual topic]. All exercises below are based on the
> actual chapter content.
```

**Do not begin writing exercises until you have completed this extraction.**
Generic exercises that could belong to any textbook on this subject are a
generation failure.

---

## STEP 2 — DETERMINE EXERCISE VOLUME

Before writing, count the chapter's major learning objectives (LOs).

| Major LOs | Core items to generate | Capstone items |
|---|---|---|
| 3–4 | 14–16 | 2 |
| 5–6 | 20–24 | 3–4 |
| 7+ | 26–30 | 4 |

Target difficulty distribution across the full set:
- 20–30% short retrieval (Tier 1)
- 30–40% guided or near-transfer application (Tier 2)
- 20–25% mixed/cumulative application including at least one interleaved item
  from a prior chapter (Tier 2 / Tier 3)
- 10–15% synthesis and challenge (Tier 3 + Tier 4)

Every major LO must appear in **more than one exercise, in more than one
format**. A single appearance is not enough. No single LO may appear more
than twice consecutively within a tier.

For bridge chapters (under 2,500 words, no anchor assignment, no distinct
learning objectives): generate Tiers 1 and 2 only. Add a note at the top:
`*Bridge chapter — Tier 3 and Tier 4 omitted.*`

---

## STEP 3 — GENERATE THE EXERCISE FILE

For each chapter, generate one file:

**Filename:** same as the chapter file but with `-exercises` appended before
the `.md` extension.

Examples:
- `chapters/04-objects-and-classes.md`
  → `exercises/04-objects-and-classes-exercises.md`
- `chapters/01-fundamentals-of-programming-in-java.md`
  → `exercises/01-fundamentals-of-programming-in-java-exercises.md`

**Write to:** `exercises/` directory alongside `chapters/`.
Create the directory if it does not exist.

---

## STEP 4 — FILE STRUCTURE

Each exercise file must follow this structure exactly:

---

```markdown
# Practice Exercises: [Chapter Title]

*Chapter [N] of [Book Title]*

> **How to use these exercises:**
> Work through each tier in order. Do not skip ahead to later tiers before
> completing earlier ones — the tiers scaffold your understanding. Attempt
> every exercise before checking the answer key. For open-ended questions,
> write at least 2–3 sentences before reading the model answer. The act of
> attempting is where the learning happens.

---

## Learning Objectives Covered

- [LO 1 — copied or inferred from the chapter, stated as a full concept phrase]
- [LO 2 — full concept phrase, not abbreviated as "LO1" or "LO2"]
- [LO 3 if applicable]

*Every exercise below maps to at least one of these objectives. The
`(Tests: ...)` tag on each exercise identifies which one(s) by full concept
name.*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and
try to recall the key steps from memory before moving on.*

[Provide one complete worked example using this chapter's core concept applied
to a concrete scenario. Show every step of the reasoning — not just the final
answer. This is guidance fading: the worked example gives maximum support
before the student works independently.

Format:
**Problem:** [A realistic scenario — same domain used throughout the chapter]
**Approach:** [Step 1: ... Step 2: ... Step 3: ...]
**Answer:** [The result and why it follows from the approach]
**What to notice:** [One sentence on what principle this example demonstrates]

Do NOT skip this section. For novice chapters (early in the book), this is
the most important item in the file. For later chapters, keep it but make it
more concise.]

---

## Tier 1 — Warm-Up (Exercises 1–[N])

*Bloom's Level: Remember / Understand*
*Purpose: Verify that the chapter's core concepts and vocabulary are in place
before you apply them. These should feel straightforward after a careful
reading.*

[Generate 20–30% of the total exercise count at this tier.
Format mix required: direct recall, contrastive classification,
definition-in-own-words, true/false with explanation.
Each exercise must map to a different LO.
Do not repeat the same LO in consecutive exercises.]

---

**Exercise 1**

[A direct recall question — a term, a definition, a classification, or a
factual relationship introduced in the chapter. Write it as a complete
question, not a fill-in-the-blank.]

*(Tests: [full concept name from the chapter LO list])*

---

**Exercise 2**

[A true/false question on a concept the chapter explicitly defines. Make it
precise — not trivially obvious and not unfairly tricky. A student who
skimmed but did not read carefully should plausibly get this wrong. Follow
immediately with "Explain your reasoning in one sentence." This forces
retrieval even on true/false items.]

True / False: [Declarative statement]

*Explain your reasoning in one sentence:*

*(Tests: [full concept name])*

---

**Exercise 3**

[A definition-in-own-words prompt: "In your own words, explain [term] as
introduced in this chapter. Do not quote the chapter directly." This forces
active encoding rather than recognition.]

*(Tests: [key vocabulary term — full concept name])*

---

**Exercise 4**

[A contrastive classification item: "Why is [X] tempting but wrong?" or
"Label each of the following as [concept A] or [concept B], then give one
sentence explaining the difference." This targets the most common
misconception the chapter addresses. It is distinct from T/F — it requires
discrimination, not just verification.]

*(Tests: [concept A vs. concept B — both named])*

---

[Continue Tier 1 exercises following the same pattern, covering different LOs.
Each exercise maps to a different LO. Do not repeat the same concept in two
consecutive Tier 1 exercises. Aim for 4–6 Tier 1 items for a standard chapter.]

---

## Tier 2 — Application (Exercises [N+1]–[N+M])

*Bloom's Level: Apply / Analyze*
*Purpose: Use the chapter's concepts in realistic situations. This is where
most of the learning happens. Expect these to take more time than Tier 1.*

[Generate 30–40% of the total exercise count at this tier.
Mandatory items:
  - At least one error analysis exercise
  - At least one AI interaction exercise (with verification requirement)
  - At least one cumulative exercise pulling a concept from a prior chapter
  - At least one self-explanation exercise (see format below)
All scenarios must be concrete and domain-appropriate — no abstract
placeholder names (Foo, Bar, MyClass).
Vary format across consecutive exercises — no two consecutive items of the
same type.]

---

**Exercise [N+1]** *(Scenario-Based Application)*

[A realistic scenario — 2–4 sentences setting up a situation grounded in
the chapter's domain and named examples where possible. Then a direct
question requiring the student to apply a chapter concept to that specific
situation. The student cannot answer this by re-reading a single sentence
from the chapter; they must make a decision.]

*(Tests: [full concept name applied to a new situation])*

---

**Exercise [N+2]** *(Error Analysis)*

[Provide a short piece of work — a code snippet, a calculation, a written
argument, a process description, or a diagram — in which a "fake student"
has made a deliberate error that reflects a real misconception from this
chapter. Frame it like this:]

> The following [code / argument / solution] was submitted by a student.
> It contains an error.

```
[Insert the flawed work here. The error should be subtle — not a typo or
obvious syntax mistake, but a conceptual misunderstanding the chapter
explicitly addresses.]
```

1. Identify exactly where the error occurs.
2. Explain the misconception that caused it — what did the student
   misunderstand about [concept]?
3. Write the corrected version.

*(Tests: [misconception targeted — full concept name])*

---

**Exercise [N+3]** *(AI Interaction — with verification requirement)*

[One of the following formats — choose whichever fits the chapter's content
most naturally:]

**Option A — Evaluate, verify, and correct:**
> First, write your own answer to this question without consulting AI:
> "[A question about this chapter's core concept]"
>
> Then read the following AI-generated response:
>
> *AI response:* "[Write a plausible AI answer that contains at least one
> factual error, one oversimplification, or one missing nuance specific to
> this chapter's content. Make it realistic — not obviously wrong.]"
>
> 1. Identify the strongest point in the AI's response.
> 2. Identify the most significant error, gap, or oversimplification.
>    Explain why it is wrong using concepts from this chapter.
> 3. Write a corrected version of the problematic sentence or paragraph.
> 4. State the specific evidence or test you would use to verify
>    the corrected claim before trusting it.

**Option B — Answer first, then compare:**
> Without using AI, write your answer to: "[A chapter question]"
>
> Now ask an AI the same question and record its response.
>
> 1. Mark one place where the AI's explanation is clearer than yours.
> 2. Mark one place where the AI's explanation is incomplete or misleading.
> 3. State what evidence from the chapter you would use to check the
>    AI's claim.

*(Tests: [core concept] + verification of AI output)*

---

**Exercise [N+4]** *(Self-Explanation)*

[A self-explanation prompt anchored to a concrete comparison, decision, or
design choice from this chapter. Ask the student to explain why one approach
is preferable to another — not as a generic opinion, but using the chapter's
vocabulary and reasoning.

Format: "In this chapter, [approach A] is used instead of [approach B] for
[task]. Explain in 2–3 sentences why [approach A] is preferable in this
context. Your explanation must use the term '[key term]' correctly."

This is distinct from a recall item — the student must reason from a
principle, not retrieve a definition.]

*(Tests: [concept pair — both named] — self-explanation)*

---

**Exercise [N+5]** *(Cumulative — prior chapter concept)*

[An exercise that requires a concept from a specific prior chapter to be
applied alongside this chapter's content. Name the prior chapter explicitly
in the prompt. The student must integrate both — not just mention them.

Format: "In [Prior Chapter N], you learned [concept X]. In this chapter,
you are working with [concept Y]. [Scenario that requires both]. How does
[concept X] affect [concept Y] in this situation?"

This is the interleaving mechanism: students must retrieve the prior concept
from memory without the prior chapter being open in front of them.]

*(Tests: [this chapter concept] + [prior chapter concept] — interleaved)*

---

[Continue Tier 2 exercises. Each exercise must target a different LO.
Vary the format: scenario, error analysis, comparison, short construction,
step-by-step procedure. Do not generate two consecutive exercises of the
same format.]

---

## Tier 3 — Synthesis (Exercises [N+M+1]–[N+M+2])

*Bloom's Level: Analyze / Evaluate*
*Purpose: Connect this chapter's concepts to a concept from a prior chapter.
These questions have no single correct answer — a strong response requires
judgment, not formula-following.*

[Generate exactly 2 synthesis exercises per chapter. Each must connect to a
specific prior chapter — name it explicitly. Do not create synthesis questions
for the first chapter of the book; write a note instead:
`*First chapter — Tier 3 omitted (no prior chapters to synthesize).*`

The two synthesis exercises must reference different prior chapters.

Every Tier 3 answer key entry must include:
- A model answer (3–5 sentences showing how the concepts interact)
- A "common error" note describing what a surface answer looks like
  (mentions both concepts but does not show how they interact)]

---

**Exercise [N+M+1]** *(Cross-Chapter Synthesis)*

[Set up a situation that genuinely requires drawing on this chapter AND a
specific prior chapter. Name both chapters in the question. The student must
integrate two concepts — not just mention them. A surface-level answer will
apply them independently; a strong answer will show how they interact.]

*[One sentence: "This question connects [Chapter N concept] to
[Chapter M concept]."]*

*What distinguishes a surface answer from a strong one:*
- [Criterion 1 — a specific concept from this chapter that must appear]
- [Criterion 2 — a specific concept from the prior chapter that must appear]
- [Criterion 3 — what the integration looks like, not just listing both]

*(Tests: [this chapter concept] + [prior chapter concept] — Ch. [N] + Ch. [M])*

---

**Exercise [N+M+2]** *(Cross-Chapter Synthesis)*

[A second synthesis exercise connecting to a different prior chapter or a
different pair of concepts. Same format. Different chapters, different
concepts from this exercise.]

*What distinguishes a surface answer from a strong one:*
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]

*(Tests: [this chapter concept] + [prior chapter concept] — Ch. [N] + Ch. [M])*

---

## Tier 4 — Challenge (Exercise [N+M+3])

*Bloom's Level: Evaluate / Create*
*Purpose: Transfer beyond what was explicitly taught. This exercise is
genuinely difficult. Solvable with the tools introduced in this chapter, but
not by following a formula or imitating a worked example.*

[Generate exactly 1 challenge exercise per chapter. No answer key entry
is required — the rubric note is the guide.]

---

**Exercise [N+M+3]** *(Transfer Challenge)*

[A question that applies the chapter's core concept to a context, constraint,
or combination that the chapter never directly addressed. The surface is
unfamiliar; the deep structure requires genuine understanding. A student
who understood only the examples will be stuck. A student who understood
the principle will be able to reason through it.]

*A strong response will address:*
- [Criterion 1 — a specific aspect of the principle, not the example]
- [Criterion 2 — an acknowledgment of what makes this context different]
- [Criterion 3 — a judgment call or design decision that cannot be copied
  from the chapter]

*(Tests: [core concept] applied to novel context)*

---

## Answer Key

> Attempt all exercises before reading this section.
> For Tier 3 and Tier 4, your answer does not need to match the model exactly —
> use the "what a strong answer includes" criteria to evaluate your own response.

---

**Worked Example**
*No answer needed — the worked example is its own model.*

---

**Ex 1**
*Model answer:* [Correct answer using the chapter's exact vocabulary]
*Common error:* [The most likely wrong answer and the misconception behind it]
*Chapter reference:* [Section or concept name — not a page number]

---

**Ex 2**
*Answer:* [True / False]
*Correct because:* [One or two sentences. If False, state precisely what
would make the statement true.]
*Common error:* [What a student who skimmed would likely answer and why]
*Chapter reference:* [Section or concept name]

---

**Ex 3**
*Model answer:* [A representative correct definition in plain language.
Note what key elements must be present — do not penalize for different
phrasing as long as the concept is accurate.]
*What a strong answer includes:*
- [Element 1 — a specific aspect of the definition that must appear]
- [Element 2 — what distinguishes this term from a related term]
*Chapter reference:* [Section or concept name]

---

**Ex 4**
*Model answer:* [Correct classification of all items with the key
distinguishing principle stated.]
*Common error:* [How students typically conflate these two concepts]
*Why this is tempting:* [The surface feature that makes the wrong answer
plausible — what the chapter addresses about this confusion]
*Chapter reference:* [Section or concept name]

---

[Continue answer key entries for all Tier 1 and Tier 2 exercises,
following the format above. Every entry must include:
1. The correct answer or model response
2. At least one common error and the misconception behind it
3. A chapter reference (section or concept name)]

---

**Ex [N+1] — Scenario Application**
*Model answer:* [Describe the correct approach and the reasoning — not just
the outcome. Explain why this application of the concept is correct in this
specific scenario.]
*Common error:* [What a student who knows the surface procedure but missed
the underlying principle would do]
*Chapter reference:* [Section or concept name]

---

**Ex [N+2] — Error Analysis**
*Where the error occurs:* [Precise location in the provided work]
*The misconception:* [What the student misunderstood — name the concept]
*Corrected version:* [The fixed code, calculation, or argument]
*Chapter reference:* [Section or concept name]

---

**Ex [N+3] — AI Interaction**
*Model answer:* [Identify the strongest point, the error, the correction,
and the verification step. The verification step answer must name a specific
test, source, or method — not "check the documentation" generically.]
*What a strong answer includes:*
- [Element 1 — specific chapter concept correctly applied in the critique]
- [Element 2 — what distinguishes a surface critique from a substantive one]
- [Element 3 — what a valid verification step looks like for this concept]
*Chapter reference:* [Section or concept name]

---

**Ex [N+4] — Self-Explanation**
*Model answer:* [The correct explanation using the chapter's vocabulary,
showing the causal or structural reason one approach is preferable.]
*Common error:* [A response that names both approaches but does not explain
why one is preferable — describing instead of reasoning]
*Chapter reference:* [Section or concept name]

---

**Ex [N+5] — Cumulative**
*Model answer:* [How the prior concept and this chapter's concept interact
in the scenario. Must show integration, not just co-mention.]
*Common error:* [A response that mentions both concepts but treats them as
independent, missing the interaction]
*Chapter reference:* [Both chapters referenced by name]

---

[Continue for remaining Tier 2 exercises.]

---

**Ex [N+M+1] — Synthesis**
*Model answer:* [A representative strong response — 3–5 sentences showing
how the two concepts interact, not just coexist.]
*What a strong answer includes:*
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]
*Common error:* [What a surface answer looks like — mentions both concepts
but does not connect them]
*Chapter reference:* [Both chapters referenced]

---

**Ex [N+M+2] — Synthesis**
*Model answer:* [Representative response]
*What a strong answer includes:*
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]
*Common error:* [Surface-answer pattern]
*Chapter reference:* [Both chapters referenced]

---

**Ex [N+M+3] — Challenge**
*No model answer provided.*
*A strong response will address:*
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]
*This question is intentionally open-ended. Discuss your response with a
peer or instructor to evaluate your reasoning.*

---

## Self-Assessment Rubric

After reviewing the answer key, evaluate your work:

| Score | Meaning | Next step |
|---|---|---|
| Tier 1 complete, most correct | Core concepts in place | Move to Tier 2 |
| Tier 2 mostly correct | Applying concepts well | Move to Tier 3 |
| Tier 2 struggling (>2 wrong) | Gaps in application | Return to flagged sections, then redo Tier 2 |
| Tier 3 attempted and close | Strong conceptual understanding | Proceed to Tier 4 |
| Tier 3 missed the integration | Concepts learned in isolation | Revisit the prior chapter referenced in the question |
| Tier 4 attempted seriously | Ready for advanced work | Compare with a peer or discuss with instructor |

*Tiers 3 and 4 are not required for all students in all courses. Check your
syllabus for which tiers are assigned.*

---

## Instructor Notes

**Bloom's distribution for this chapter:**

| Tier | Exercises | Bloom's Level | % of Set |
|---|---|---|---|
| Tier 1 — Warm-up | Ex 1–[N] | Remember / Understand | ~25% |
| Tier 2 — Application | Ex [N+1]–[N+M] | Apply / Analyze | ~55% |
| Tier 3 — Synthesis | Ex [N+M+1]–[N+M+2] | Analyze / Evaluate | ~12% |
| Tier 4 — Challenge | Ex [N+M+3] | Evaluate / Create | ~8% |

**Suggested point distribution:**
- Tier 1: 5 points per item (completion/retrieval credit)
- Tier 2: 10 points per item (graded application)
- Tier 3: 15 points per item (written assignment or discussion post)
- Tier 4: 20 points (optional extension or extra credit)

**Assignment recommendations:**
- Tier 1: appropriate for completion credit or pre-class preparation
- Tier 2: appropriate for graded homework (0.5–1.0% of course grade per item)
- Tier 3: appropriate for discussion posts or written assignments (1.0–2.0% each)
- Tier 4: appropriate for optional extension, extra credit, or capstone work

**Worked example note:**
The worked example in this chapter targets [specific concept]. If students
struggle with Tier 1 after completing it, ask them to close the worked example
and reproduce the reasoning steps from memory before attempting the exercise
again. The retrieval attempt — not re-reading — is where the encoding happens.

**Error analysis exercise (Ex [N+2]):**
The deliberate error targets [specific misconception]. In student work,
watch for [what this misconception looks like in practice].

**AI interaction exercise (Ex [N+3]):**
The AI response contains [describe the specific error embedded in the
AI output]. Students who accept the AI response without checking have
missed [specific concept]. The verification step (part 4) is the most
important part: push students to name a concrete test or source, not a
generic statement like "I would look it up."

**Self-explanation exercise (Ex [N+4]):**
Students often describe the two approaches instead of explaining why one is
preferable. The target vocabulary for a strong response is [key term(s)].
Watch for answers that say "because it is better" without stating the
mechanism.

**Cumulative exercise (Ex [N+5]):**
This exercise requires [prior chapter concept]. If students have not retained
that concept, use the failure as a teaching moment: revisit the prior chapter's
key idea in one sentence, then ask them to reattempt. Do not simply provide
the answer — the retrieval attempt from the prior chapter is the pedagogical
goal.

**Common errors to watch for:**
- [Error 1 — tied to a specific Tier 1 concept]
- [Error 2 — tied to the error analysis exercise]
- [Error 3 — tied to the synthesis question's cross-chapter connection]

**Scaffolding adjustments:**
- *For students who struggle with Tier 1:* [Targeted section to revisit —
  not just "reread the chapter" but the specific concept to re-examine]
- *For students who complete Tier 4 quickly:* [One extension direction that
  increases depth — a related concept, a harder case, a real-world reference]

**DEI note:**
All scenarios in this exercise set have been written to avoid cultural,
regional, or socioeconomic assumptions. If you adapt scenarios for your
course context, apply the same standard: any student from any background
should be able to access the problem without prior cultural knowledge.
```

---

## RULES

**Read the chapter fully before generating any exercise.** Items must be
grounded in the chapter's actual content — named examples, specific
vocabulary, the chapter's anchor concepts. Items that could appear in any
textbook on this subject are a generation failure.

**Every exercise must have a `(Tests: ...)` tag.** The tag must name the
specific concept or LO using its full concept phrase — never abbreviations
like "LO1" or "LO2", and never generic descriptions like "application" or
"critical thinking."

**The Worked Example is mandatory.** Every chapter file must begin with a
worked example before Tier 1. It may be shorter for later (non-novice)
chapters, but it must be present. An exercise file without a worked example
is incomplete.

**Tier 1 must include at least one contrastive classification item.** The
"contrastive classification" format (Exercise 4 template) targets the most
common misconception in the chapter. It is not optional.

**Tier 2 must include a self-explanation exercise and a cumulative exercise.**
Both are mandatory. The self-explanation exercise asks the student to reason
from a principle using chapter vocabulary. The cumulative exercise names a
specific prior chapter and requires integrating both chapters' concepts.

**AI interaction exercises must require a verification step.** "Option A"
format must include part 4: "State the specific evidence or test you would
use to verify the corrected claim." An AI exercise without a verification
step is incomplete.

**Scenarios must be concrete and domain-appropriate.** Never use abstract
placeholder names (Foo, Bar, MyClass, PersonA, PersonB). Use relatable,
domain-appropriate scenarios: for a Java textbook, use student grade
trackers, inventory systems, library catalogs, or weather data apps. For
a writing textbook, use real genres and realistic writing situations.

**Error analysis exercises must contain a real misconception.** The error
in the "fake student's" work must reflect something a student who read the
chapter carelessly or incompletely would plausibly produce — not a typo,
not an obviously wrong answer, not something the chapter never covered.

**The AI response in the AI interaction exercise must be plausibly realistic.**
Write an AI response that sounds confident and mostly correct, with one
embedded flaw. An AI response that is obviously wrong does not build critical
evaluation skills. The student should need the chapter's content to spot
the error.

**Synthesis exercises must name the prior chapter explicitly.** Do not
write "as you learned earlier." Write "as introduced in Chapter [N]:
[Title]." The student must know which chapter to return to. The two
synthesis exercises must reference two different prior chapters.

**Every Tier 3 answer key entry must include a "common error" note.**
This is mandatory for Tier 3, not just Tier 1 and 2. The common error
describes what a surface answer looks like — mentions both concepts but
does not show how they interact.

**Tier 4 gets no model answer.** The challenge exercise is intentionally
open-ended. Provide only the rubric criteria. A model answer would defeat
the purpose.

**Every answer key entry (Tiers 1–3) must include a common error.** Knowing
the right answer is less useful than knowing what the wrong answer reveals.
For every exercise, name the most likely incorrect response and the
misconception behind it.

**Do not use absolute terms in any exercise or answer option.** Do not
write "always," "never," "all," or "none" in any question stem or answer
choice.

**No negative stems.** Do not write "which of the following is NOT" or
"EXCEPT" constructions. Reframe as a positive question about what something
is, does, or requires.

**Exercises within a tier must cover different LOs.** Do not generate two
consecutive exercises testing the same concept. Vary the concept, the
format, and the cognitive demand across the tier.

**Feedback is mandatory for all exercises except Tier 4.** Every Tier 1,
2, and 3 exercise must have a complete answer key entry. An exercise without
feedback is incomplete.

**Apply DEI principles to every scenario.** Before finalizing any scenario,
verify: does this assume cultural familiarity, socioeconomic context, or
regional knowledge that some students may not have? If yes, rewrite it.

---

## STEP 5 — REPORT

After writing all files, produce a brief generation report:

```
## Exercise Generation Report

Book: [title from metadata.yaml or folder name]
Chapters processed: [N]
Files written: [N]

| Chapter | File | Tiers | Total exercises | Notes |
|---------|------|-------|-----------------|-------|
| Ch 01: [title] | 01-...-exercises.md | 1 2 3 4 | 22 | |
| Ch 05: [title] | 05-...-exercises.md | 1 2 | 14 | Bridge chapter |
| ...

Files written to: exercises/
```

---

## NOTES FOR ADAPTING

**For a writing textbook:** Tier 2 scenario exercises present a passage,
draft, or rhetorical situation and ask the student to apply a chapter concept
to it. Error analysis exercises provide a flawed draft and ask the student
to diagnose the structural or rhetorical problem. Tier 3 synthesis questions
connect rhetorical concepts across chapters (e.g., connecting argument
structure from Chapter 3 to evidence evaluation from Chapter 6).

**For a STEM textbook:** Tier 2 exercises may include short calculations,
classifications, or procedure-following tasks. Error analysis exercises
provide broken code, a flawed derivation, or an incorrect algorithm output.
Show-your-work is a valid instruction for these. Tier 4 challenge questions
ask the student to predict behavior under changed conditions or identify the
failure mode of a system.

**For a mixed textbook:** The four-tier structure is stable across domains.
What changes is what counts as a "scenario" in Tier 2, what counts as
"synthesis" in Tier 3, and what counts as "transfer" in Tier 4.

**On interleaving:** Within Tier 2, vary the format across consecutive
exercises so that students must identify which type of cognitive work
each one requires, not just imitate the preceding item. The mandatory
cumulative exercise is the explicit interleaving mechanism — it forces
retrieval from a prior chapter without the prior chapter being open.

**On the worked example:** The worked example is not a bonus — it is the
first cognitive event in the exercise set. Novice learners need one final
guided model before they retrieve and transfer independently. Do not replace
it with a hint or a tip box. It must show complete reasoning, not just the
answer.

**On AI exercises:** The four most effective AI-aware patterns for this
textbook are: (1) answer first yourself, then compare with AI; (2) find and
fix errors in the AI answer; (3) state the evidence you used to verify the
AI output; (4) explain what you rejected and why. All four should appear
somewhere across the chapter set, not just in the AI exercise slot.

**On re-running:** Safe to re-run at any time. Existing files in
`exercises/` are overwritten. Chapter files are never modified.

**For ChatGPT / Gemini:** This prompt works as-is. Remove references to
Cowork file-writing if running interactively — instead, ask the model to
generate one chapter at a time and paste the output manually.
