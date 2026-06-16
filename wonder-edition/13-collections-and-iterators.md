# Module 13 — Collections and Iterators: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Collections and Iterators," this chapter covers JUnit testing, executable behavioral claims, regression detection, assertions, and lambda/stream operations. The Collections Framework appears briefly. The central subject is testing discipline.

---

## The Strange Question

Consider this specific scenario. A developer writes a `searchByTitle` method. It receives a query string and returns a list of matching books from the library catalog. The developer runs it. Five books appear. The right five books appear. The developer moves on.

Three days later, a teammate refactors the `Book` class to normalize titles to lowercase on construction. The teammate does not touch `searchByTitle`. Nobody runs `searchByTitle` again.

At the demo, `searchByTitle("Design")` returns an empty list. The method is unchanged. The teammate's change is unrelated. So what, precisely, caused the failure?

---

## First Intuition

Most people reach for the teammate's change immediately. The teammate touched the `Book` class. The search broke. Therefore the teammate broke it.

This feels logical. It is also incomplete. The teammate's change is the trigger, not the cause. The cause is older.

The developer ran `searchByTitle` and saw correct output. That observation lived in the developer's memory. It could not run again on Tuesday. It could not compare new output to old output. It was a judgment made once about one moment. That is not verification.

> **Planning prompt:** Before reading further — what mental model do you hold right now about what "the code works" means? Rate your confidence on a 1–5 scale. Predict: will your model change after this chapter, or will it be confirmed? Write your prediction before continuing. This matters because you will check it at the end.

---

## The Surprise

But the teammate did not break the method. The teammate changed an assumption the method depended on without knowing it was an assumption.

The `searchByTitle` method compared the query string to book titles using `contains`. Before the refactor, book titles were stored exactly as entered — "Design Patterns" with mixed case. After the refactor, they were stored as "design patterns" in lowercase. The query "Design" no longer matched.

The method never stated that it required titles in their original case. That assumption was invisible. It was embedded in the setup every time the method ran and produced correct output. Nothing in the method changed. The ground beneath the method changed.

What still goes unexplained: if the developer had written a test before the demo, would the test have caught this? Yes — but only if the test was written in a way that created a specific title and searched for a specific string. A test that added a book titled "Design Patterns" and searched for "Design" would fail after the refactor. It would have flagged the regression the moment the refactor ran.

> **Monitoring prompt:** Name the hidden assumption the method made. Identify the moment that assumption was contradicted. Ask: what would it look like to write that assumption down in a form the computer can check?

---

## The Hidden Structure

Therefore, the puzzle resolves when you separate two activities that look identical from the outside: observing output and verifying a claim.

Observing output requires a developer, a running program, a moment of judgment, and a memory. The judgment is informal. It cannot be replayed. It cannot detect change. It belongs to one person at one time.

Verifying a claim requires none of those things. A claim takes the form: "When the catalog contains a book titled 'Design Patterns' and the query is 'Design', `searchByTitle` returns a list of size one." That sentence is a requirement. A test encodes it as an assertion. The computer can check it at any time, without anyone present, including after the surrounding code has changed.

**Misconception Checkpoint**

It is tempting to think that tests prove code is correct. But no finite test suite can enumerate every possible input, every possible system state, or every future change to the code's environment. The correct model holds that tests make claims explicit and executable — a passing test is evidence that a specific stated claim holds under specific conditions. The key distinction is between a test that confirms output looks right in one moment and a test that states a verifiable requirement that can be checked automatically whenever the codebase changes.

**Code Trace**

Here is a test that appears to check the search method but proves nothing:

```java
// Version 1 — no assertion; this is observation, not verification
@Test
void searchLooksRight() {
    Library library = new Library();
    library.addBook(new Book("Design Patterns", "Gang of Four"));
    List<Book> results = library.searchByTitle("Design");
    System.out.println(results);  // developer reads the output
}
```

This test will always pass. It contains no assertion. The test runner cannot distinguish correct output from incorrect output. Now compare the corrected version:

```java
// Version 2 — assertion present; this is verification
@Test
void searchByTitleReturnsSingleMatch() {
    Library library = new Library();
    library.addBook(new Book("Design Patterns", "Gang of Four"));
    List<Book> results = library.searchByTitle("Design");
    assertNotNull(results);
    assertEquals(1, results.size());
}
```

The second version states a requirement. After the `Book` refactor, this test fails. That failure is information. It tells the developer exactly when the assumption broke and what the assumption was.

---

## Try Looking At It This Way

**Target:** A JUnit test suite for a method — a set of assertions that state what the method is required to do and check it automatically.

**Base:** A building inspection checklist used by a licensed inspector before a structure is approved for occupancy.

**Features:**
- Both encode requirements as explicit, checkable items before deciding whether the subject satisfies them.
- Both can be re-run after changes — a remodel triggers a new inspection; a code change triggers the test suite.
- Both distinguish failure modes: a checklist item can fail because the building is wrong, or because the requirement changed, or because the inspector set up the check incorrectly — parallel to the three reasons a test fails.
- Both grow more valuable as the thing being checked grows more complex. A small shed needs fewer checklist items than a twelve-story building. A small method needs fewer tests than a method with six branches and three boundary conditions.

**Commonalities:**
- The checklist item "emergency exit must open from inside without a key" corresponds to the assertion `assertEquals(1, results.size())` — each makes the requirement precise enough to check without judgment. This matters because precision is what enables automatic re-checking.
- The inspector who re-runs the checklist after a remodel is performing regression detection. This matters because the passing tests from before the remodel are not guaranteed to pass after it.
- The inspector does not write the checklist while inspecting. The checklist is written before the inspection begins, from the building code. This matters because writing a test after seeing the output biases the assertion toward what the implementation already does.

**Boundaries:**
- Unlike a building inspection, a test suite is written by the same person who wrote the code under test. A building inspector has no involvement in the construction. This creates a blind-spot risk: the developer's assumptions about how the method works will shape the tests they think to write. An inspector has no assumptions to import. This is why the chapter recommends asking AI to suggest cases after writing your own assertions — not to offload thinking, but to find the cases your assumptions made invisible.

**Conclusions:** A test suite is an inspector's checklist written by the builder. Its strength is repeatability and precision. Its weakness is that it reflects the builder's assumptions about what matters. Writing the assertion before the implementation is the closest analog to separating the inspector's role from the builder's role that a solo developer can achieve.

---

## Where The Analogy Breaks

Unlike a building inspection checklist, a test suite runs before the structure is occupied — before the code reaches users. An inspection happens after construction completes. Tests run continuously during construction, after every change. This matters because it shifts the moment of discovery. A test failure during development is cheap to fix. A regression discovered at the demo, or by a user, is expensive. The inspection analogy suggests a one-time review at the end. The test-suite reality is continuous re-checking throughout. Do not let the analogy imply that testing is a final step.

---

## Small Discovery

Consider what happens in commercial food manufacturing before a product reaches store shelves.

**Raw data:** A cookie manufacturer runs a production line. The formula specifies flour, sugar, butter, and baking time. The cookies that come out of the oven look correct — golden, uniform, the right diameter. Quality control passes. The product ships.

Three weeks later, a supplier substitutes a different grade of butter with a slightly higher water content. The formula is unchanged. The oven temperature is unchanged. The cookies that come out are softer, with a shorter shelf life. Customer complaints arrive six weeks after the substitution.

**Pattern search:** What changed? Not the formula. Not the oven. Not the baking time. The butter changed. But the quality control check only measured the output cookies — color, diameter, hardness at time of production. It did not measure the input ingredients against the formula's assumptions.

**Prediction — write before reading the next paragraph:** The quality control check passed because the cookies looked right at the time of production. What does this correspond to in software testing? What would a "boundary test" look like in this manufacturing context? Write your answer before continuing.

---

The revelation: the quality control check was observing output, not verifying claims about inputs. A proper specification would state: "butter must have water content below X percent." A check against that specification would fail immediately when the substitution occurred — not six weeks later when customers complained.

This is the boundary test. The normal case (standard butter, low water content) always passes. The boundary case (substitute butter, elevated water content) reveals the assumption the formula depended on. A recipe that specifies only output appearance but not input tolerances is an incomplete specification — exactly as a method that handles the happy path but never states its assumptions about input conditions is an incomplete specification.

---

## What This Changes

A reader who has worked through this can now answer questions that were unanswerable before.

First: a method that "worked" on Monday can fail on Tuesday after an unrelated change because the method's correct behavior depended on an assumption embedded in the system state. No assertion stated the assumption. No test ran to detect when the assumption was violated. The failure was silent until a state change made the assumption false.

Second: specific test code looks different now. A test that contains only `System.out.println` is not a test — it is a print statement annotated with `@Test`. A test that contains `assertNotNull(results)` and `assertEquals(2, results.size())` is a test. The assertion is what separates observation from verification.

**Practice Bridge:** Write five JUnit tests for your project's `searchByTitle()` method — or the most search-like method in your domain. Cover: (1) normal case returning one result, (2) normal case returning multiple results, (3) empty collection returning an empty list, (4) query that matches nothing returning an empty list, (5) null input not throwing a `NullPointerException`. Each test must include at least one `assertEquals` or `assertNotNull`. At least one test must fail on first run and reveal an assumption in the implementation. Document what assumption it revealed and what you changed.

The open question pointing forward: a method can pass all five of these tests and still fail in the running application. The controller calling it can pass the wrong argument. The persistence layer can load malformed data. The GUI can display results before the method returns. Unit tests verify components in isolation. They cannot verify the interactions between them. Module 14 addresses that gap.

---

## Wonder Questions

1. If a passing test is not a proof of correctness, what would a proof of correctness look like? Formal verification tools exist — why do most production systems not use them?

2. The chapter says a failing test is information. A developer says a failing test is an obstacle to shipping. They are describing the same event. What, precisely, are they disagreeing about?

3. Regression tests protect behavior that previously worked. Who decides which behavior matters enough to protect? What gets left unprotected, and what is the cost of that decision?

4. A test is written for requirement A. The requirement changes to requirement B. The test still passes because the implementation satisfies both. The developer concludes the software is fine. What is wrong with this reasoning, and how would you detect it?

5. The chapter draws a boundary: write assertions before asking AI to suggest test cases. What assumption does this boundary rest on? Under what conditions would the assumption be false — and would the boundary still matter?

> **Precision Summary**
>
> **What the concept is:** A test is an executable, precise claim that on specific inputs with specific setup, a method produces a specific required output — a claim the computer can check automatically, anytime, without a developer present.
>
> **What it explains:** Why code that "worked" can break after an unrelated change; why five targeted tests covering normal, empty, no-match, boundary, and invalid-input cases are more valuable than fifty happy-path variations; why tests grow more valuable as the codebase grows and as the number of possible regressions increases.
>
> **What it does NOT mean:** Tests prove code is correct. A passing test suite means no bugs remain. Writing tests is a substitute for stating requirements before implementation.
>
> **What comes next:** How to verify behavior that spans multiple interacting components — the gap between unit testing and system correctness that Module 14 addresses through integration testing and end-to-end verification.
