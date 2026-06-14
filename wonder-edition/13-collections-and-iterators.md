# Module 13 — Collections and Iterators: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Collections and Iterators," this chapter covers JUnit testing, executable behavioral claims, regression detection, and lambda/stream operations as verified transformations.

---

## The Strange Question

A method passes every test you run. It compiles. It produces output that looks correct. A teammate changes one unrelated class. You run the method again — it fails.

Nothing in the method changed. So what broke it?

---

## First Intuition

Most people answer: something must have changed in the method after all. Or: the tests were not thorough enough. Or: the teammate introduced a bug.

All three feel plausible. None of them is the deepest answer.

The instinct points toward the code. The deeper answer points toward the claims made about the code. When the method "worked," what exactly did that word mean? What had been verified, and by whom, and when?

Before reading further, write down your answer to this question: what is the difference between "I ran the method and the output looked right" and "the method is correct"?

> **Planning Metacognitive Prompt:** What assumptions are you making about what "correct" means? Are those assumptions written anywhere the computer can check them?

---

## The Surprise

The method did not fail because something changed in the method. It failed because a claim about the method was never written down.

On Monday, the system happened to be in a state that made the output look right. The developer looked at the output and judged it correct. That judgment lived in a person's memory. It could not run again on Tuesday. It could not compare Tuesday's output to Monday's output. It could not report a failure.

The method was never "correct." It was "unreported." The passing behavior was an observation about one moment, not a verifiable claim about the method's requirements.

But here is what makes this uncomfortable: the test suite that exists on Tuesday also does not prove the method is correct. A passing test proves exactly one thing — that on this specific input, with this specific setup, the output matched the stated requirement at the time the test ran. Nothing more.

> **Monitoring Metacognitive Prompt:** Does the existence of a test suite change whether the method is correct? Or does it change what you know about the method? Hold the distinction — it is not resolved yet.

---

## The Hidden Structure

The chapter resolves the puzzle by separating two activities that most developers conflate: observing output and verifying claims.

Observing output is informal. It requires a developer to be present, to run the program, to judge whether the result looks right, and to remember that judgment. The judgment cannot be rerun. It cannot be shared automatically. It decays as the system changes.

Verifying a claim is formal. A claim takes the form: "When the library has these books and the query is this string, the search method returns this specific list." That sentence is a requirement. A test encodes the requirement as an assertion the computer can check, anytime, without a developer present.

It is tempting to think that tests prove code is correct. But tests cannot enumerate every possible input, so no finite test suite covers all cases. The correct model holds that tests make claims explicit and executable. A passing test is evidence that a specific stated claim holds. It is not a proof of general correctness. The value is precision and repeatability, not certainty.

The null-input failure in the chapter illustrates this exactly. The assumption "the query is never null" was real — it was embedded in the implementation. It was never stated as a requirement. The test did not create a bug; it surfaced an assumption that was already there, invisible.

---

## Try Looking At It This Way

Consider how a legal contract works.

**The base domain — contracts.** Before two parties sign a contract, their obligations exist only as intentions and verbal agreements. Those intentions may be genuine. They cannot be enforced automatically. After the contract is signed, the obligations are written down in a form a third party can interpret. If a dispute arises, the contract is consulted. The contract does not prevent bad behavior. It makes the expected behavior explicit enough to detect when it is violated.

**The target domain — test suites.** Before a test exists, a method's expected behavior exists only as the developer's intention. That intention may be genuine. It cannot be checked automatically. After the test is written, the expected behavior is encoded in assertions a test runner can execute. If a change breaks the behavior, the test runner detects it. The test does not prevent bugs. It makes the expected behavior explicit enough to detect when it is violated.

**Shared features.** Both a contract and a test transform informal obligations into formal claims. Both enable automatic detection of violations. Both are written before disputes arise, not after. Both are more valuable over time than at the moment of writing.

**Mapped commonalities.** The assertion in a test corresponds to a contract clause. The test setup corresponds to the conditions under which the clause applies. The test runner corresponds to a judge checking whether the clause was violated. A regression corresponds to a breach.

**Boundary of the analogy.** A contract negotiates between parties with different interests. A test has no negotiating parties — the developer writes both the requirement and the implementation. Contracts can be ambiguous by design; test assertions must be precise or they fail to compile. The analogy holds for the detection-of-violations structure, not for adversarial dynamics.

**Conclusion.** A test suite is a self-enforcing contract between a developer and their future self. Its value increases as the codebase grows, because there are more clauses to violate.

---

## Where The Analogy Breaks

A contract is enforced by a third party after a violation occurs. A test suite runs before deployment and catches violations before they reach users. This is not a minor difference. It changes when information arrives. Tests shift the moment of discovery from after a failure is observed to before it is released. No contract analogy captures this temporal inversion. Do not let the analogy suggest that tests are reactive — they are proactive by design.

---

## Small Discovery

Here is a short inquiry into a domain outside software.

Consider a recipe for bread. A baker follows the recipe and produces a loaf. The loaf looks right — golden crust, correct height, hollow sound when tapped. The baker declares success.

**Raw data.** The same baker follows the same recipe on five consecutive days. On day one: perfect loaf. On day two: dense, flat loaf. On day three: perfect loaf. On day four: dense, flat loaf. On day five: perfect loaf.

**Pattern search.** The recipe did not change. The oven did not change. What varied between the days?

Here is what the baker recorded: day one, flour from a new bag, humidity 40%. Day two, same flour bag, humidity 80%. Day three, new bag, humidity 41%. Day four, same bag, humidity 79%. Day five, new bag, humidity 38%.

**Guided prediction.** Before reading the next sentence, write down: what does the pattern suggest is the hidden variable? What is the "assumption" the recipe never stated?

**Revelation.** The recipe assumed low ambient humidity. Flour absorbs moisture from the air. At high humidity, the flour's water content changed, and the recipe's stated ratios no longer produced the right dough consistency. The assumption was real. It was embedded in every successful bake. It was never written down. The five bakes did not reveal the assumption — only the variation between conditions did.

This is what a boundary test does. The normal case (new bag, low humidity) always passes. The edge case (same bag, high humidity) reveals the assumption. A recipe that only specifies ingredients but not environmental conditions is an incomplete specification — exactly as a method that handles the happy path but never states its assumptions about null inputs is an incomplete specification.

---

## What This Changes

A reader who has worked through this can now explain three things they could not explain before.

First: why a method that "worked" can fail after a change to a different class. The method's behavior depended on an assumption embedded in the surrounding state. No test stated that assumption. No test ran to detect when the assumption was violated. When the state changed, the assumption broke silently.

Second: why five targeted tests — normal, empty, no-match, boundary, invalid input — are more valuable than fifty variations of the happy path. Each of the five covers a category of claim. The fifty variations cover one category more thoroughly without extending coverage to the others. The goal is not test count; it is claim coverage.

Third: why writing the assertion before writing the implementation is not pedantic. The assertion states the requirement. Writing it first forces the developer to have a requirement before they check whether the implementation satisfies it. Writing it after produces tests that verify whatever the implementation already does — which may or may not be the requirement.

The question that comes next is this: what happens when multiple components interact? A search method can pass all its unit tests and still fail in the application because the component calling it passes the wrong argument. Unit tests verify components in isolation. They cannot verify the interactions between them. That is the gap Module 14 will address.

---

## Wonder Questions

1. If a passing test is not a proof of correctness, what would a proof of correctness even look like — and why do most production systems not attempt it?

2. The chapter says a failing test is information. A developer says a failing test is an obstacle to shipping. Both are describing the same event. What are they actually disagreeing about?

3. Regression tests catch behavior that breaks after a change. But who decides which behavior matters enough to protect with a test? What gets left unprotected, and why?

4. A test is written for requirement A. The requirement changes to requirement B. The test still passes because the implementation satisfies both. The developer concludes the software is fine. What is wrong with this reasoning?

5. The chapter draws a hard boundary: write assertions before asking AI to suggest test cases. What assumption does this boundary rest on? Under what conditions would that assumption be false?

> **Precision Summary**
>
> **What the concept is:** A test is an executable, precise claim that on specific inputs with specific setup, a method produces a specific required output.
>
> **What it explains:** Why code that "worked" can break without the code changing; why boundary and invalid-input cases matter more than additional happy-path variations; why tests grow more valuable as a codebase grows.
>
> **What it does NOT mean:** Tests prove code is correct. Tests are complete specifications. A passing test suite means no bugs remain.
>
> **What comes next:** How to verify behavior that spans multiple interacting components — the gap between unit testing and system correctness.
