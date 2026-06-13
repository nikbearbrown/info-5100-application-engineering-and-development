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

**Do not begin writing exercises until you have completed this extraction.**
Generic exercises that could belong to any textbook on this subject are a
generation failure.

---

## STEP 2 — DETERMINE EXERCISE VOLUME

Before writing, count the chapter's major learning objectives (LOs).

| Major LOs | Core items to generate | Capstone items |
|---|---|---|
| 3–4 | 12–16 | 2 |
| 5–6 | 18–24 | 3–4 |
| 7+ | 24–30 | 4 |

Every major LO must appear in **more than one exercise, in more than one
format**. A single appearance is not enough.

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

- [LO 1 — copied or inferred from the chapter]
- [LO 2]
- [LO 3 if applicable]

*Every exercise below maps to at least one of these objectives. The
`(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Tier 1 — Warm-up (Exercises 1–[N])

*Bloom's Level: Remember / Understand*
*Purpose: Verify that the chapter's core concepts and vocabulary are in place
before you apply them. These should feel straightforward after a careful
reading.*

[Generate 40–50% of the total exercise count at this tier.
Format options: direct recall, definition-in-own-words, true/false with
explanation, short identification. No scenario required. Student should be
able to answer without performing a full task.]

---

**Exercise 1**

[A direct recall question — a term, a definition, a classification, or a
factual relationship introduced in the chapter. Write it as a complete
question, not a fill-in-the-blank.]

*(Tests: [specific concept from the chapter])*

---

**Exercise 2**

[A true/false question on a concept the chapter explicitly defines. Make it
precise — not trivially obvious and not unfairly tricky. A student who
skimmed but did not read carefully should plausibly get this wrong. Follow
immediately with "Explain your reasoning in one sentence." This forces
retrieval even on true/false items.]

True / False: [Declarative statement]

*Explain your reasoning in one sentence:*

*(Tests: [specific concept])*

---

**Exercise 3**

[A definition-in-own-words prompt: "In your own words, explain [term] as
introduced in this chapter. Do not quote the chapter directly." This forces
active encoding rather than recognition.]

*(Tests: [key vocabulary term])*

---

[Continue Tier 1 exercises following the same pattern, covering different
LOs. Each exercise maps to a different LO. Do not repeat the same concept
in two consecutive Tier 1 exercises.]

---

## Tier 2 — Application (Exercises [N+1]–[N+M])

*Bloom's Level: Apply / Analyze*
*Purpose: Use the chapter's concepts in realistic situations. This is where
most of the learning happens. Expect these to take more time than Tier 1.*

[Generate 35–40% of the total exercise count at this tier.
Mandatory: at least one error analysis exercise, at least one AI interaction
exercise. All scenarios must be concrete and domain-appropriate — no abstract
placeholder names (Foo, Bar, MyClass).]

---

**Exercise [N+1]** *(Scenario-Based Application)*

[A realistic scenario — 2–4 sentences setting up a situation grounded in
the chapter's domain and named examples where possible. Then a direct
question requiring the student to apply a chapter concept to that specific
situation. The student cannot answer this by re-reading a single sentence
from the chapter; they must make a decision.]

*(Tests: [specific concept applied to a new situation])*

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

*(Tests: [misconception targeted — name the specific concept])*

---

**Exercise [N+3]** *(AI Interaction)*

[One of the following formats — choose whichever fits the chapter's content
most naturally:]

**Option A — Evaluate and critique:**
> The following response was generated by an AI assistant when asked:
> "[A plausible student question about this chapter's core concept]"
>
> *AI response:* "[Write a plausible AI answer that contains at least one
> factual error, one oversimplification, or one missing nuance specific to
> this chapter's content. Make it realistic — not obviously wrong.]"
>
> 1. Identify the strongest point in the AI's response.
> 2. Identify the most significant error, gap, or oversimplification.
>    Explain why it is wrong using concepts from this chapter.
> 3. Write a corrected version of the problematic sentence or paragraph.

**Option B — Prompt and assess:**
> Write a prompt you would give an AI assistant to help you [specific task
> from this chapter — e.g., "debug this type of error," "explain this
> concept to a beginner," "generate a practice problem on this topic"].
> Then describe: what a good AI response would include, and what would
> signal that the AI's response is incomplete or misleading.

*(Tests: [core concept] + critical evaluation of AI output)*

---

**Exercise [N+4]** *(Comparison / Discrimination)*

[A question requiring the student to distinguish between two related concepts
from the chapter that are often confused. Format: "What is the difference
between X and Y? Give an example of a situation where using X is correct and
using Y would be an error." This targets the most common misconception in the
chapter.]

*(Tests: [concept A] vs. [concept B])*

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
`*First chapter — Tier 3 omitted (no prior chapters to synthesize).*`]

---

**Exercise [N+M+1]** *(Cross-Chapter Synthesis)*

[Set up a situation that genuinely requires drawing on this chapter AND a
specific prior chapter. Name both chapters in the question. The student must
integrate two concepts — not just mention them. A surface-level answer will
apply them independently; a strong answer will show how they interact.]

*[One sentence teaser: "This question connects [Chapter N concept] to
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
*Model answer:* [For Option A: identify the strongest point, the error,
and provide the corrected version. For Option B: describe the key elements
of a good prompt and the signals of an incomplete AI response.]
*What a strong answer includes:*
- [Element 1 — specific chapter concept correctly applied in the critique]
- [Element 2 — what distinguishes a surface critique from a substantive one]
*Chapter reference:* [Section or concept name]

---

**Ex [N+4] — Comparison**
*Model answer:* [The key distinction between the two concepts, stated
clearly in the chapter's vocabulary. The example must show a scenario
where the difference matters — not just name both terms.]
*Common error:* [The most common way students conflate these two concepts]
*Chapter reference:* [Section or concept name]

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
| Tier 1 — Warm-up | Ex 1–[N] | Remember / Understand | ~45% |
| Tier 2 — Application | Ex [N+1]–[N+M] | Apply / Analyze | ~37% |
| Tier 3 — Synthesis | Ex [N+M+1]–[N+M+2] | Analyze / Evaluate | ~12% |
| Tier 4 — Challenge | Ex [N+M+3] | Evaluate / Create | ~6% |

**Assignment recommendations:**
- Tier 1: appropriate for completion credit or pre-class preparation
- Tier 2: appropriate for graded homework (0.5–1.0% of course grade per item)
- Tier 3: appropriate for discussion posts or written assignments (1.0–2.0% each)
- Tier 4: appropriate for optional extension, extra credit, or capstone work

**Error analysis exercise (Ex [N+2]):**
The deliberate error targets [specific misconception]. In student work,
watch for [what this misconception looks like in practice].

**AI interaction exercise (Ex [N+3]):**
The AI response contains [describe the specific error embedded in the
AI output]. Students who accept the AI response without checking have
missed [specific concept]. Use this exercise to open a discussion about
[the broader principle at stake].

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
specific concept or LO being assessed, not a generic description like
"application" or "critical thinking."

**Scenarios must be concrete and domain-appropriate.** Never use abstract
placeholder names (Foo, Bar, MyClass, PersonA, PersonB). Use relatable,
domain-appropriate scenarios: for a Java textbook, use student grade
trackers, inventory systems, library catalogs, or weather data apps. For
a writing textbook, use real genres and realistic writing situations.

**Error analysis exercises must contain a real misconception.** The error
in the "fake student's" work must reflect something a student who read the
chapter carelessly or incompletely would plausibly produce — not a typo,
not an obviously wrong answer, not something the chapter never covered.

**The AI response in Ex [N+3] must be plausibly realistic.** Write an AI
response that sounds confident and mostly correct, with one embedded flaw.
An AI response that is obviously wrong does not build critical evaluation
skills. The student should need the chapter's content to spot the error.

**Synthesis exercises must name the prior chapter explicitly.** Do not
write "as you learned earlier." Write "as introduced in Chapter [N]:
[Title]." The student must know which chapter to return to.

**Tier 4 gets no model answer.** The challenge exercise is intentionally
open-ended. Provide only the rubric criteria. A model answer would defeat
the purpose.

**Every answer key entry must include a common error.** Knowing the right
answer is less useful than knowing what the wrong answer reveals. For every
exercise, name the most likely incorrect response and the misconception
behind it.

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
each one requires, not just imitate the preceding item. This is the
interleaving principle applied at the exercise level.

**On re-running:** Safe to re-run at any time. Existing files in
`exercises/` are overwritten. Chapter files are never modified.

**For ChatGPT / Gemini:** This prompt works as-is. Remove references to
Cowork file-writing if running interactively — instead, ask the model to
generate one chapter at a time and paste the output manually.
