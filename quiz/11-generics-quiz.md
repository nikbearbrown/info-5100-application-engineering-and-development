# Chapter Quiz: Module 11: Generics

*Chapter 11 of INFO 5100 Application Engineering and Development*

> **Mismatch note:** This quiz follows the actual chapter body as source of truth and flags the title/objective mismatch.

> **Instructions:** Attempt every question before checking the answer key.
> Do not look at the answers while working - the act of retrieval is the learning.
> Review the answer key after completing all questions, not after each one.

---

## Learning Objectives Covered

This quiz assesses the following chapter objectives:

- Explain the chapter-specific role of event handler registration chain.
- Apply event/handler/registration/lambda to a realistic project situation.
- Diagnose the common misconception: assuming a lambda is always better than a named handler.

---

## Section 1 - Recall and Recognition (Questions 1-4)

*Target: Bloom's Remember / Understand*  
*Format: Multiple-choice (3 options) and True/False*  
*Target difficulty: p = 0.77-0.85*


---

**Question 1** *(Multiple-Choice)*

In this module, what does **event handler registration chain** help students understand?

A) Registered handlers respond to events, call model methods, and refresh the view.
B) That the visible output alone is enough to prove the design is correct.
C) That chapter vocabulary can be memorized without tracing behavior.

---

**Question 2** *(Multiple-Choice)*

Which answer best describes the misconception the chapter is trying to prevent about **event/handler/registration/lambda**?

A) Assuming a lambda is always better than a named handler.
B) Using chapter terms precisely when explaining code behavior.
C) Checking evidence before trusting a design change.

---

**Question 3** *(True/False)*

The chapter treats **event/handler/registration/lambda** as something students must connect to a concrete artifact, not just define from memory.

[ ] True  [ ] False

---

**Question 4** *(True/False)*

If a complex button action is crammed into one long lambda, the strongest response is to ignore the chapter mechanism and assume the program is correct because it opened or compiled.

[ ] True  [ ] False

---

## Section 2 - Application and Analysis (Questions 5-7)

*Target: Bloom's Apply / Analyze*  
*Format: Scenario-based multiple-choice, short-answer, and analysis multiple-choice*  
*Target difficulty: p = 0.50-0.70*


---

**Question 5** *(Scenario-Based Multiple-Choice)*

Scenario: a complex button action is crammed into one long lambda. What should the student do first?

A) Use an inner class or named method when handler responsibility needs structure.
B) Rewrite unrelated classes until the symptom disappears.
C) Treat the behavior as correct because one screen or command appeared to work.

---

**Question 6** *(Short-Answer)*

Name one piece of evidence that would show whether **event handler registration chain** is working correctly in this module.

*Your answer:*

_____________________

---

**Question 7** *(Multiple-Choice)*

Why is the wrong approach, "assuming a lambda is always better than a named handler," risky in this chapter?

A) It hides the mechanism the chapter asks students to verify.
B) It gives students more precise evidence about the artifact.
C) It separates symptoms from causes in the intended way.

---

## Section 3 - Synthesis and Evaluation (Question 8)

*Target: Bloom's Evaluate / Create*  
*Format: Brief-Response*  
*Target difficulty: p = 0.30-0.50*

---

**Question 8** *(Brief-Response)*

Apply **event/handler/registration/lambda** to a new project feature. What would you inspect, and what evidence would convince you the design is defensible?

*Your response (2-4 sentences):*

_____________________


---

## Answer Key

> Read this section only after completing all questions.


---

**Q1 - A**  
*Correct because:* Registered handlers respond to events, call model methods, and refresh the view.  
*Why the distractors are wrong:*  
- B) This misses the chapter mechanism or misconception: That the visible output alone is enough to prove the design is correct.
- C) This misses the chapter mechanism or misconception: That chapter vocabulary can be memorized without tracing behavior.
*Chapter reference:* event handler registration chain

---

**Q2 - A**  
*Correct because:* The chapter specifically works against assuming a lambda is always better than a named handler.  
*Why the distractors are wrong:*  
- B) This misses the chapter mechanism or misconception: Using chapter terms precisely when explaining code behavior.
- C) This misses the chapter mechanism or misconception: Checking evidence before trusting a design change.
*Chapter reference:* event/handler/registration/lambda

---

**Q3 - True**  
*Correct because:* The quiz reinforces vocabulary through code, workflow, or project evidence.  
*Chapter reference:* event/handler/registration/lambda

---

**Q4 - False**  
*Correct because:* The scenario requires diagnosis using the chapter mechanism, not surface success.  
*Chapter reference:* event handler registration chain

---

**Q5 - A**  
*Correct because:* Use an inner class or named method when handler responsibility needs structure.  
*Why the distractors are wrong:*  
- B) This misses the chapter mechanism or misconception: Rewrite unrelated classes until the symptom disappears.
- C) This misses the chapter mechanism or misconception: Treat the behavior as correct because one screen or command appeared to work.
*Chapter reference:* event handler registration chain

---

**Q6 - Short-Answer**  
*Model answer:* Use an inner class or named method when handler responsibility needs structure.  
*Chapter reference:* event handler registration chain

---

**Q7 - A**  
*Correct because:* It hides the mechanism the chapter asks students to verify.  
*Why the distractors are wrong:*  
- B) This misses the chapter mechanism or misconception: It gives students more precise evidence about the artifact.
- C) This misses the chapter mechanism or misconception: It separates symptoms from causes in the intended way.
*Chapter reference:* event/handler/registration/lambda

---

**Q8 - Brief-Response**  
*Model answer:* A strong response should name the relevant artifact (event handler registration chain), explain the mechanism (registered handlers respond to events, call model methods, and refresh the view), and cite evidence such as use an inner class or named method when handler responsibility needs structure.  
*What a strong answer includes:*  
- The chapter artifact or mechanism.  
- Evidence that would expose the likely failure mode.  
*Chapter reference:* Synthesis and evaluation

---

## Self-Assessment Rubric

| Score | Meaning | Next step |
|---|---|---|
| 8 / 8 | Strong retention - ready to move on | Proceed to the next chapter |
| 6-7 / 8 | Partial mastery - specific gaps present | Return to the sections flagged in wrong answers |
| 4-5 / 8 | Foundational gaps | Reread the chapter, then retake the quiz |
| Below 4 / 8 | Chapter concepts not yet consolidated | Reread, then work through the exercises before retaking |

*Note: Section 3 is weighted more heavily. Getting Q8 wrong while getting Sections 1-2 right is a signal of surface-level knowledge - not mastery.*

---

## Instructor Notes

**Bloom's distribution for this quiz:**

| Level | Questions | % of Quiz |
|---|---|---|
| Remember / Understand | Q1-Q4 | 50% |
| Apply / Analyze | Q5-Q7 | 37.5% |
| Evaluate / Create | Q8 | 12.5% |

**Common errors to watch for in student work:**

- Treating the vocabulary as labels rather than mechanisms.
- Trusting surface success without evidence.
- Missing the chapter-specific artifact or failure mode in scenario questions.
