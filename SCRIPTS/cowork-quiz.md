# Cowork Prompt: Generate End-of-Chapter Quizzes for Each Chapter

---

## ROLE & CONTEXT

You are working on a university-level textbook. You have access to all chapter
files in `chapters/`. Your job is to generate a quiz file for each relevant
instructional module and write it to `quiz/`.

This is a generation pass, not an extraction pass. You are writing new quiz
content derived from each chapter's concepts, vocabulary, and learning
objectives — not copying or paraphrasing sentences from the chapter.

These quizzes are **formative retrieval practice tools**, not summative
tests. Their purpose is to strengthen long-term memory through effortful
recall (the testing effect), not to assign grades. Design every item to
teach through testing.

---

## STEP 1 - IDENTIFY MODULES TO PROCESS

Read the `chapters/` directory. Process only instructional course modules.
Skip files that are front matter, introduction-only material, appendices,
back matter, or exams. Process every relevant `.md` file except:

- `00-frontmatter.md`
- `00-introduction.md`
- `99-back-matter.md`
- Any file whose name contains `exam`, `midterm`, `appendix`, or
  `back-matter`
- Any appendix-style file starting with `95-`, `96-`, `97-`, `98-`, or `99-`

For each chapter file, extract before writing:

- Chapter number and title (from the filename and `# heading`)
- Stated learning objectives (explicit `## Learning Objectives` block, or
  inferred from the chapter's opening and structure)
- Core concepts (the main ideas the chapter teaches)
- Key vocabulary (any terms defined, bolded, or introduced in the chapter)
- Named examples, cases, datasets, or primary sources used in the chapter
- The lab, exercise, assignment, CLI task, evidence packet, or project
  artifact students are asked to produce
- Concrete Java artifacts, commands, files, code snippets, GUI components,
  tests, data records, or workflows used in the chapter
- Named failure modes, bugs, setup errors, design risks, or debugging
  moments the chapter teaches students to prevent
- Common misconceptions the chapter explicitly addresses or that are
  predictable from the content
- What the student can do after this chapter that they couldn't before

Before generating questions, write a private extraction table for each
chapter with these columns:

| Field | Extraction |
|---|---|
| Chapter file | |
| Chapter heading | |
| Stated learning objectives | |
| Actual body topic | |
| Filename/objective/body mismatch? | Yes/No, with note |
| Core concepts | |
| Exact vocabulary to reinforce | |
| Named examples/labs/project artifacts | |
| Concrete Java or workflow artifacts | |
| Common misconceptions/failure modes | |
| What students can do afterward | |

If the filename or stated learning objectives do not match the chapter body,
do not blindly follow the filename. Use the chapter's `#` heading and actual
body content as the source of truth, and note the mismatch in the generation
report. If the mismatch is severe enough that a quiz would misrepresent the
module, stop and flag it instead of generating a misleading quiz.

**Do not begin writing quiz items until you have completed this extraction.**
Generic quiz items that could belong to any textbook are a generation failure.

---

## STEP 2 — GENERATE THE QUIZ FILE

For each chapter, generate one file:

**Filename:** same as the chapter file but with `-quiz` appended before
the `.md` extension.

Examples:
- `chapters/04-literacy-narrative.md`
  → `quiz/04-literacy-narrative-quiz.md`
- `chapters/01-fundamentals-of-programming-in-java.md`
  → `quiz/01-fundamentals-of-programming-in-java-quiz.md`

**Write to:** `quiz/` directory alongside `chapters/`.
Create the directory if it does not exist.

---

## STEP 3 — FILE STRUCTURE

Each quiz file must follow this structure exactly:

---

```markdown
# Chapter Quiz: [Chapter Title]

*Chapter [N] of [Book Title]*

> **Instructions:** Attempt every question before checking the answer key.
> Do not look at the answers while working — the act of retrieval is the
> learning. If you are unsure, make your best attempt and mark it with (?).
> Review the answer key after completing all questions, not after each one.

---

## Learning Objectives Covered

This quiz assesses the following chapter objectives:

- [LO 1 — copied or inferred from the chapter]
- [LO 2]
- [LO 3 if applicable]

---

## Section 1 — Recall and Recognition (Questions 1–[N])

*Target: Bloom's Remember / Understand*
*Format: Multiple-choice (3 options) and True/False*
*Target difficulty: p = 0.77–0.85*

[Generate 4–5 questions at this level. Follow the rules below for each format.]

---

**Question 1** *(Multiple-Choice)*

[A complete, direct question — not a fill-in-the-blank stem. The student
should be able to read the stem, cover the options, and formulate the
correct answer from memory before revealing the choices.]

A) [Plausible distractor — based on a real misconception from this chapter]
B) [Correct answer]
C) [Plausible distractor — based on a different real misconception]

---

**Question 2** *(Multiple-Choice)*

[Same rules. Vary which position (A/B/C) holds the correct answer across
the question set. Do not always place the correct answer in the same slot.]

A) [Option]
B) [Option]
C) [Option]

---

**Question 3** *(True/False)*

[A single declarative statement. Make it precise — not trivially obvious
and not unfairly tricky. It should test whether the student understands
the concept, not just whether they remember a specific sentence.]

☐ True  ☐ False

---

**Question 4** *(Multiple-Choice)*

[Use a different concept from the chapter than Questions 1–3. Each question
in Section 1 should map to a different learning objective.]

A) [Option]
B) [Option]
C) [Option]

---

**Question 5** *(True/False)*

[Target a common misconception the chapter addresses. A student who skimmed
but did not read carefully should plausibly get this wrong.]

☐ True  ☐ False

---

## Section 2 — Application and Analysis (Questions [N+1]–[N+4])

*Target: Bloom's Apply / Analyze*
*Format: Multiple-choice (3 options) and Short-Answer*
*Target difficulty: p = 0.50–0.70*

[Generate 3–4 questions at this level. At least one must be scenario-based:
embed a realistic situation or mini-case from the chapter's domain, then
ask the student to apply a concept or make a judgment.]

---

**Question [N+1]** *(Scenario-Based Multiple-Choice)*

[A realistic scenario — 2–4 sentences setting up a situation grounded in
the chapter's domain and named examples where possible. Then a direct
question requiring application of a chapter concept to that scenario.]

A) [Plausible distractor — a student who knows the surface procedure
   but missed the underlying principle would choose this]
B) [Option]
C) [Correct answer — requires actual conceptual understanding, not
   just pattern-matching to the chapter's worked examples]

---

**Question [N+2]** *(Short-Answer)*

[A question requiring the student to produce an answer — a term, a number,
a classification, or a brief explanation. No answer choices provided.
The question must not be answerable by guessing or by elimination.]

*Your answer:*

_____________________

---

**Question [N+3]** *(Multiple-Choice)*

[A comparison or inference question: "Why is X approach used instead of Y
in this context?" or "What would happen if [condition] changed?" Tests
whether the student understands the mechanism, not just the outcome.]

A) [Option]
B) [Option]
C) [Option]

---

**Question [N+4]** *(Short-Answer)*

[A question requiring a brief explanation — 1–2 sentences. Not a
definition. The student must connect two chapter concepts or explain
why a procedure works.]

*Your answer:*

_____________________

---

## Section 3 — Synthesis and Evaluation (Questions [N+5]–[N+6])

*Target: Bloom's Evaluate / Create*
*Format: Short-Answer or Brief-Response*
*Target difficulty: p = 0.30–0.50*
*Note: Omit this section for bridge chapters (under 2,500 words, no
anchor assignment). Add note: `*Bridge chapter — Section 3 omitted.*`*

[Generate 1–2 questions at this level. These are the hardest questions in
the quiz. They require judgment, critique, or transfer — not recall or
procedure-following.]

---

**Question [N+5]** *(Brief-Response)*

[A question requiring evaluation or justification: "Given [situation],
which approach would be more appropriate and why?" or "What is a
limitation of the method described in this chapter, and under what
conditions would it fail?" The student must take a position and defend it
using chapter concepts.]

*Your response (2–4 sentences):*

_____________________

---

**Question [N+6]** *(Transfer — Brief-Response)* *(optional)*

[A question that applies the chapter's core concept to a context not
discussed in the chapter. The surface is unfamiliar; the deep structure
is the same. No worked example or hint is provided. This question rewards
students who understood the principle, not just the examples.]

*Your response (2–4 sentences):*

_____________________

---

## Answer Key

> Read this section only after completing all questions.

---

**Q1 — [Correct option letter]**
*Correct because:* [One or two sentences explaining the concept that makes
this answer correct. Use the chapter's exact vocabulary.]
*Why the distractors are wrong:*
- A) [If A is wrong: one sentence explaining the misconception it reflects]
- C) [If C is wrong: one sentence explaining the misconception it reflects]
*Chapter reference:* [Section or concept name in the chapter — not a page
number, since page numbers vary by format]

---

**Q2 — [Correct option letter]**
*Correct because:* [Explanation]
*Why the distractors are wrong:*
- [Distractor]: [Misconception explanation]
- [Distractor]: [Misconception explanation]
*Chapter reference:* [Section or concept name]

---

**Q3 — [True / False]**
*Correct because:* [Explanation — if False, state precisely what would make
the statement true, or what the common error in the statement is]
*Chapter reference:* [Section or concept name]

---

**Q4 — [Correct option letter]**
*Correct because:* [Explanation]
*Why the distractors are wrong:*
- [Distractor]: [Misconception explanation]
- [Distractor]: [Misconception explanation]
*Chapter reference:* [Section or concept name]

---

**Q5 — [True / False]**
*Correct because:* [Explanation]
*Chapter reference:* [Section or concept name]

---

**Q[N+1] — [Correct option letter]**
*Correct because:* [Explain how the scenario requires applying the concept —
do not just restate the answer. Explain the reasoning process.]
*Why the distractors are wrong:*
- [Distractor]: [What misconception or partial knowledge leads here]
- [Distractor]: [What misconception or partial knowledge leads here]
*Chapter reference:* [Section or concept name]

---

**Q[N+2] — Short-Answer**
*Model answer:* [The correct answer or a representative correct response.
For short-answer questions with some variability, note what elements must
be present for full credit.]
*Common error:* [The most likely wrong answer and why it is wrong]
*Chapter reference:* [Section or concept name]

---

**Q[N+3] — [Correct option letter]**
*Correct because:* [Explanation]
*Why the distractors are wrong:*
- [Distractor]: [Misconception]
- [Distractor]: [Misconception]
*Chapter reference:* [Section or concept name]

---

**Q[N+4] — Short-Answer**
*Model answer:* [Representative correct response — 1–2 sentences]
*What a strong answer includes:* [2–3 bullet points naming the concepts or
connections that distinguish a complete answer from a partial one]
*Chapter reference:* [Section or concept name]

---

**Q[N+5] — Brief-Response**
*Model answer:* [A representative strong response — 2–4 sentences. This
is a model, not the only acceptable answer.]
*What a strong answer includes:*
- [Element 1 — a specific concept from the chapter that must appear]
- [Element 2 — a specific judgment or justification]
*Common error:* [What a student who understood the surface but missed
the underlying principle would write]
*Chapter reference:* [Section or concept name]

---

**Q[N+6] — Transfer Brief-Response** *(if included)*
*Model answer:* [Representative response]
*What a strong answer includes:*
- [Concept from chapter applied correctly to new context]
- [Acknowledgment of what is different in the new context]
*Chapter reference:* [Core concept, not a specific section — this question
tests transfer, so the reference is the principle, not the example]

---

## Self-Assessment Rubric

After reviewing the answer key, score yourself:

| Score | Meaning | Next step |
|---|---|---|
| 9–10 / 10 (or equivalent) | Strong retention — ready to move on | Proceed to the next chapter |
| 7–8 / 10 | Partial mastery — specific gaps present | Return to the sections flagged in wrong answers |
| 5–6 / 10 | Foundational gaps | Reread the chapter, then retake the quiz |
| Below 5 / 10 | Chapter concepts not yet consolidated | Reread, then work through the worked exercises before retaking |

*Note: Section 3 questions are weighted more heavily. Getting Q[N+5] and
Q[N+6] wrong while getting Sections 1–2 right is a signal of surface-level
knowledge — not mastery.*

---

## Instructor Notes

**Bloom's distribution for this quiz:**

| Level | Questions | % of Quiz |
|---|---|---|
| Remember / Understand | Q1–Q5 | ~45% |
| Apply / Analyze | Q[N+1]–Q[N+4] | ~36% |
| Evaluate / Create | Q[N+5]–Q[N+6] | ~18% |

**Psychometric targets:**
- Section 1 items: p-value target 0.77–0.85; r_pb ≥ 0.30
- Section 2 items: p-value target 0.50–0.70; r_pb ≥ 0.30
- Section 3 items: p-value target 0.30–0.50; r_pb ≥ 0.40

**Common errors to watch for in student work:**

- [Error 1 — specific to this chapter's concepts, based on the distractors
  used in Section 1]
- [Error 2 — specific to a misconception targeted in Section 2]
- [Error 3 — specific to the transfer failure pattern Section 3 reveals]

**Signs a student needs to return to the chapter before this quiz:**

- [Specific knowledge gap that would make Section 1 impossible]
- [Specific confusion that suggests the chapter's core concept was missed]

**Scaffolding adjustments:**

- *For students who score below 5:* [Targeted intervention — not "reread"
  but a specific section or concept to revisit first]
- *For students who score 10/10 on first attempt:* [One extension question
  or challenge that increases depth without changing the concept]

**Grading weight guidance (if used for credit):**
- Section 1 MCQ items: 0.25–0.5% of final course grade each
- Section 2 Short-Answer items: 0.5–1.0% each
- Section 3 Brief-Response items: up to 2.5% each
- Collectively, chapter quizzes should not exceed 5% of overall course grade
```

---

## RULES

**Read the chapter fully before generating any question.** Quiz items must
be grounded in the chapter's actual content — named examples, specific
vocabulary, the chapter's anchor concepts. Items that could appear in any
textbook on this subject are a generation failure.

**Do not use universal question templates.** A question stem may not be a
generic sentence with only one chapter term swapped in. Ban repeated stems
such as:

- "What is the main role of [term] in this chapter's account of application
  engineering?"
- "Why does the chapter connect [term] to the semester project rather than
  treating it as an isolated fact?"
- "A student is building the course project and reaches the part connected
  to [term]..."
- Any stem that would still make sense if moved unchanged into three or more
  other chapter quizzes.

Every question must be anchored in at least one chapter-specific element:
a named lab, setup command, code artifact, object relationship, GUI flow,
CSV record, event handler, FXML mapping, JUnit test, data-structure choice,
handoff artifact, or named failure mode.

**Use concrete artifacts.** Each quiz must include at least two questions
that ask students to interpret or reason about a concrete artifact from the
chapter. Examples include command output, Java code, object state, an array
or collection, a file row, a screen transition, a controller method, an
event chain, an FXML `fx:id`, a test case, a sort/filter result, or a final
project handoff checklist.

**Target the chapter's real misconceptions.** Distractors and True/False
items should target likely errors from this module, such as JRE vs JDK,
compilation error vs runtime error, class vs object, reference vs object,
symptom vs root cause, authentication vs authorization, Comparator vs
Comparable, model vs view, handler registration vs handler execution,
`fx:id` mismatch, passing test vs complete proof, or working code vs
defensible handoff. Choose misconceptions that fit the chapter being
processed; do not reuse this list mechanically.

**Limit course-wide AI/verification questions.** AI boundaries, verification,
evidence, and responsibility are recurring course themes, but they must not
crowd out the module topic. Use these themes only when they are tied to a
specific chapter artifact or decision.

**Distractors must reflect real misconceptions.** Every wrong answer option
must represent a misunderstanding that a student who read the chapter
carelessly or incompletely would plausibly hold. Do not invent arbitrary
wrong answers, typos, or obviously ridiculous options.

**Three-option MCQ is the standard format.** Use one correct answer and
two plausible distractors per MCQ. Do not use four or five options unless
the publisher style guide explicitly requires it. Do not use "All of the
above," "None of the above," or combo answers ("A and C only").

**Stems must be complete direct questions.** Never write an incomplete
sentence as a stem (e.g., "The primary function of X is ___"). Write
"What is the primary function of X?" The student must be able to cover
the options and attempt an answer from memory.

**Negative stems are banned.** Do not use "which of the following is NOT"
or "EXCEPT" constructions. If the chapter's content genuinely requires
testing a student's ability to identify what something is not, reframe as
a positive question about what something is.

**Correct answer position must be randomized.** Across the question set,
distribute the correct answer equally across A, B, and C. Do not default
to placing the correct answer in the same position repeatedly.

**Questions must be strictly independent.** No question may reveal or
depend on the answer to another question. Read the full question set
before finalizing — check for inadvertent clues.

**Use the chapter's exact vocabulary.** If the chapter defines a term,
use that term in the question. Do not substitute synonyms or paraphrases.
The quiz reinforces the chapter's language, not generic language.

**Answer key rationales are mandatory.** Every question — including
True/False — must have an answer key entry explaining why the correct
answer is correct and why the key distractors are wrong. A key without
rationales is incomplete.

**Do not generate model answers for Section 3 that are too narrow.**
Transfer and evaluation questions accept a range of defensible responses.
The model answer is a representative example, not the only correct one.
The "what a strong answer includes" bullets define the actual rubric.

**Bridge chapters get Sections 1 and 2 only.** If a chapter is a bridge
chapter (under 2,500 words, no anchor assignment, no distinct learning
objectives), generate only Sections 1 and 2. Add a note at the top:
`*Bridge chapter — Section 3 omitted.*`

**No absolute terms in any answer option.** Do not use "always," "never,"
"all," or "none" in any answer choice. These are flagged by test-wise
students as incorrect regardless of content.

**No emojis** except the ☐ checkbox marker in True/False questions.

**Preserve chapter vocabulary.** Use the exact terms the chapter introduces.
If the chapter defines *retrieval strength*, the quiz uses that term, not
"how well you remember something."

---

## STEP 4 — REPORT

Before writing the final report, perform this QA gate on every quiz:

- No question stem is reused across more than two quiz files.
- Every question names or depends on a chapter-specific concept, artifact,
  lab, example, workflow, failure mode, or misconception.
- At least two questions require interpreting a concrete artifact from the
  chapter rather than only explaining a term.
- At least one Section 2 question is a realistic scenario grounded in the
  chapter's lab, project shape, Java mechanism, or workflow.
- Section 3 asks for judgment, critique, transfer, or failure analysis; it
  is not a generic "apply this idea to another domain" question unless the
  deep structure is clearly tied to the chapter.
- Answer-key rationales mention the actual mechanism or misconception, not
  only broad ideas such as "responsibility," "evidence," or "verification."
- If the chapter title/objectives and body content conflict, the report
  states how the quiz handled the mismatch.
- If a quiz fails any gate, revise it before reporting completion.

After writing all files, produce a brief generation report:

```
## Quiz Generation Report

Book: [title from metadata.yaml or folder name]
Chapters processed: [N]
Files written: [N]

| Chapter | File | Sections generated | Total questions | Notes |
|---------|------|--------------------|-----------------|-------|
| Ch 01: [title] | 01-...-quiz.md | 1 2 3 | 11 | |
| Ch 05: [title] | 05-...-quiz.md | 1 2 | 9 | Bridge chapter |
| ...

Files written to: quiz/
```

---

## NOTES FOR ADAPTING

**For a writing textbook** (like *Writing Guide with LLMs*): Section 1
questions test rhetorical vocabulary and structural recognition. Section 2
scenario questions present a passage or excerpt and ask the student to
identify the technique or evaluate the move. Section 3 questions ask the
student to critique a draft excerpt or defend a revision choice using
chapter concepts.

**For a STEM textbook** (like *Info 5100*): Section 2 short-answer questions
may require a formula, a classification, or a short calculation. Show
your work is a valid instruction for these. Section 3 questions ask the
student to predict behavior under changed conditions or identify the
failure mode of a system.

**For a mixed textbook:** The section structure is stable across domains.
What changes is what counts as a "scenario" in Section 2 and what counts
as "transfer" in Section 3.

**On cognitive distribution:** The default distribution (45% LOCS / 36%
mid-order / 18% HOCS) targets introductory-to-intermediate textbooks. For
advanced or professional-tier textbooks, shift the balance: generate 3
questions in Section 1, 4 in Section 2, and 3 in Section 3, producing a
~27% / 36% / 27% LOCS/mid/HOCS split. Note this adjustment in the
generation report.

**On running this again:** Safe to re-run at any time. Existing files in
the `quiz/` directory are overwritten. Chapter files are never modified.
