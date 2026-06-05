# Worked Exercises: Claude Code for Java
*Chapter 95 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

## Prerequisites
- You can state a Requirement, name the Artifact (class/method/field/test) where behavior lives, and define the Evidence that would prove the answer acceptable — the three statements you write before asking Claude Code.
- You can run the Three-Question Audit on an AI-assisted component: explain what it does without Claude's words, explain why it is designed this way including the rejected alternative, and trace its non-trivial behavior to a test or an explicit reason it was not tested.
- You hold the appendix's central rule: *you cannot verify what you do not understand*, and Claude Code may help only after you have enough understanding to verify what comes back.

---

## Part A — Full Worked Example: Verifying an AI-generated `Catalog.searchByTitle`

**What this demonstrates:** That code which compiles and passes the demo can still fail an untested edge case, and that verification means tracing behavior to evidence rather than trusting fluent output.

**The problem:** You asked Claude Code for a title search. You first wrote the three pre-ask statements:

```text
Requirement: searchByTitle(query) returns every Book whose title contains
             the query, case-insensitively; null query returns an empty list.
Artifact:    Catalog.searchByTitle(String query) -> List<Book>
Evidence:    empty catalog -> []; "design" matches "Design Patterns" and
             "The Design of Everyday Things" -> 2 results; no match -> [];
             null query -> [] (not a throw).
```

Claude Code returned:

```java
public List<Book> searchByTitle(String query) {
    List<Book> results = new ArrayList<>();
    String needle = query.toLowerCase();
    for (Book book : books) {
        if (book.getTitle().toLowerCase().contains(needle)) {
            results.add(book);
        }
    }
    return results;
}
```

It compiles. In the demo you typed "design" and got the two expected books. The task is not to admire it — it is to **verify it against the Evidence you wrote**.

**The solution:**

**Step 1 — Restate the Requirement and the Evidence as a checklist, before reading the code closely.** Five claims must hold: empty catalog → `[]`; multi-match → both books; no-match → `[]`; case-insensitive; null query → `[]`.
*Why:* The threshold is "you must be able to verify what comes back." Verification compares output to *your stated* requirement, not to whether the code looks like what you would write. Listing the claims first prevents the demo's success from standing in for all five.
*Check:* You have five explicit claims; the demo only exercised one (multi-match, case-insensitive on "design").

**Step 2 — Trace each claim against the code path, not the demo.** Walk the method for each input.

| Evidence claim | input | code path | result | verdict |
| --- | --- | --- | --- | --- |
| multi-match | "design" | loops, two titles `.contains("design")` | 2 books | passes |
| empty catalog | "x", `books` empty | loop body never runs | `[]` | passes |
| no-match | "zzz" | loop runs, no `.contains` | `[]` | passes |
| case-insensitive | "DESIGN" | `needle="design"`, titles lowered | 2 books | passes |
| **null query** | `null` | `query.toLowerCase()` on `null` | **NullPointerException** | **FAILS** |

*Why:* The null branch is the one the demo never touched. `query.toLowerCase()` is called before any null check, so a null query throws `NullPointerException` — violating the Requirement that null returns an empty list.
*Check:* This is exactly the appendix's failure mode: the code "compiles and passes the demo but fails an untested edge case."

**Step 3 — Apply the Three-Question Audit to the failing path.**
- *Can you explain what it does on null without Claude's words?* "It calls `.toLowerCase()` on the query before checking for null, so null input crashes." Yes.
- *Can you explain the design and the rejected alternative?* The author implicitly assumed non-null input; the alternative — guard null at entry — was not chosen. The Requirement says it should be.
- *Can you trace the null behavior to a test?* Not yet. That untested path is the gap.
*Why:* "Untested does not mean correct." A null path you have not exercised needs either a test or an explicit reason the requirement rules out null — and here the requirement *requires* null handling.
*Check:* Question three returns "no," so the component is not ready. Put it back.

**Step 4 — Fix to satisfy the Requirement, then prove it with Evidence.**
```java
public List<Book> searchByTitle(String query) {
    if (query == null) {
        return new ArrayList<>();   // requirement: null -> empty list, not a throw
    }
    List<Book> results = new ArrayList<>();
    String needle = query.toLowerCase();
    for (Book book : books) {
        if (book.getTitle().toLowerCase().contains(needle)) {
            results.add(book);
        }
    }
    return results;
}
```
And the test that pins the previously-failing claim:
```java
@Test
void searchByTitleReturnsEmptyListOnNull() {
    Catalog catalog = new Catalog();
    catalog.add(new Book("Design Patterns", "GoF"));
    assertTrue(catalog.searchByTitle(null).isEmpty());
}
```
*Why:* The guard implements *your* null policy (empty list, not exception), and the test converts the formerly invisible null assumption into an executable, repeatable claim.
*Check:* Run the test before the guard — it fails (NPE). Add the guard — it passes. The failing-then-passing test is the evidence.

**Step 5 — Write the AI Use Disclosure that proves the gate held.**
```text
I asked Claude Code to implement Catalog.searchByTitle from a signature and a
case-insensitive "contains" requirement.
Claude produced a loop-based search that handled empty, no-match, multi-match,
and case-insensitivity correctly but called query.toLowerCase() with no null guard.
I caught the null case by tracing against my stated Evidence (null -> empty list).
I added the null guard and wrote a JUnit test that failed before the fix.
I own the null policy: null is an empty query, not an error.
```
*Why:* A disclosure that names the task, what was kept, what was wrong, and how it was verified "proves something" — it shows Claude suggested, you verified, you corrected on substantive grounds.
*Check:* You can fill in "what I changed or rejected." If you could not, you would have accepted everything — the signal to go back.

**Final answer:** The AI search was 80% correct and demo-clean but violated the stated null requirement; verification meant tracing every Evidence claim through the code path (not the demo), catching the untested null branch, fixing it to your policy, and pinning it with a failing-then-passing test.

**What made this work:** The central concept is the appendix's threshold — *you cannot verify what you do not understand* — operationalized as "trace each stated Evidence claim through the actual code path." The naive approach (accept because it compiles and the demo worked) fails because the demo only exercised one of five claims; the danger of fluent AI output is precisely that it is *shaped exactly for your problem* and looks like what you would have written, which is mistaken for "I verified it."

**Self-explanation prompt:** Why is "it looks like the code I would have written" not a verification, and what specific activity replaces that feeling?

---

## Part B — Matched Practice Problem: Verifying an AI-generated `Patron.borrow` limit check

**What this demonstrates:** That AI code enforcing a business rule can pass the happy path and silently violate the rule at the boundary — the same trace-against-evidence discipline, different rule.

**The problem:** Your domain rule: a patron may hold at most 3 books; a 4th `borrow` must be rejected. You wrote the pre-ask statements and Claude Code returned:

```java
public boolean borrow(Book book) {
    if (borrowedBooks.size() < 4) {      // AI's interpretation of "at most 3"
        borrowedBooks.add(book);
        return true;
    }
    return false;
}
```

It compiles and works when you borrow one or two books in the demo. Verify it against the Requirement that the limit is **3**.

Produce a verification with the same deep structure as Part A:

**Step 1 — Restate the Requirement and Evidence as a checklist.** (What should happen at 2 held, 3 held, and the attempted 4th?)
**Step 2 — Trace each claim against the code path, not the demo.** (Build a trace table for `size()` = 2, 3, 4; what does `< 4` allow?)
**Step 3 — Apply the Three-Question Audit to the failing path.**
**Step 4 — Fix to satisfy the Requirement, then prove it with a boundary test.**
**Step 5 — Write the AI Use Disclosure that proves the gate held.**

Include a trace table showing the result of the 4th borrow under the AI code versus the requirement.

**Stuck?** The phrase "at most 3" makes the boundary `size() < 3` (or `<= 2`), not `< 4`. AI chose a plausible-but-wrong off-by-one; your Evidence at the boundary (3 held → 4th rejected) is what exposes it.

> Instructor note: No solution is provided for Part B. Work it fully before moving on.

---

## Part C — Completion Problem: Verifying an AI-written test (not just AI code)

**What this demonstrates:** That AI-written *tests* can assert only the happy path, so a passing AI test suite is not evidence the requirement is covered.

**The problem:** You asked Claude Code to "write tests for `Catalog.searchByTitle`." It returned a single test:

```java
@Test
void searchFindsMatchingBook() {
    Catalog catalog = new Catalog();
    catalog.add(new Book("Clean Code", "Martin"));
    assertEquals(1, catalog.searchByTitle("Clean").size());
}
```

The test passes. Decide whether this test suite is sufficient evidence for the Requirement (case-insensitive contains; empty/no-match/null all defined).

**Step 1 — State what the one AI test actually proves.** It proves exactly one claim: a single exact-prefix, same-case match returns one result.
*Why:* A passing test is evidence only for the specific input it supplies. This input is the happy path — it does not exercise empty, no-match, case-insensitivity, or null.

**Step 2 — List the Requirement claims the AI test leaves unverified.** Empty catalog → `[]`; no-match → `[]`; case-insensitive ("clean" lowercased matches "Clean Code"); null → `[]`.
*Why:* "Trusting AI-written tests that only assert the happy path" is a named failure mode; the suite's green checkmark hides four unchecked claims.

**Step 3 — [BLANK] Write the case-insensitivity test and the no-match test.**
*Your work here:*

*Why (your explanation):*

**Step 4 — [BLANK] Write the null-query test that encodes *your* policy (empty list, not a throw).**
*Your work here:*

*Why (your explanation):*

**Step 5 — Judge the suite and disclose.** Only after the suite covers normal, empty, no-match, case-insensitive, and null is it evidence for the Requirement.
*Why:* Coverage of the claims you care about — including failure modes — is the goal, not test count. To disclose: note that Claude's single test asserted only the happy path and you added four cases it omitted.

**Final answer:** An AI-written test that passes proves only its one happy-path claim; you must add tests for the empty, no-match, case-insensitive, and null claims before the suite counts as evidence — a green AI test suite is not coverage.

**Self-explanation prompt:** Why can a test suite written by AI be *entirely passing* and still leave your stated requirement almost completely unverified?

---

## Part D — Error-Recognition Problem: Accepting a plausible refactor

> **Use this section only after completing Parts A–C.**

**The problem:** You asked Claude Code to refactor a verbose `getAvailableBooks` method. Below is your verification write-up. Steps 1, 2, and 4 are correct. One step contains an error.

**Original method (verified correct earlier):**
```java
List<Book> available = new ArrayList<>();
for (Book b : books) {
    if (b != null && b.isAvailable()) available.add(b);
}
return available;
```

**Claude's refactor:**
```java
return books.stream()
    .filter(Book::isAvailable)
    .collect(Collectors.toList());
```

**Step 1 — State the Requirement (correct).** "Return all available books; the `books` list may contain a null entry from a malformed CSV load, which must be skipped, not crash."

**Step 2 — Confirm the happy path matches (correct).** On a catalog with no nulls, both versions return the same available books; the demo passes.

**Step 3 — ⚠ Accept the refactor.**
> "The refactor is cleaner and behaves identically — `filter(Book::isAvailable)` does the same job as the loop's `if`. The stream version is equivalent, so I accept it and delete the old method."

**Step 4 — Disclosure note (correct).** "Claude refactored the loop into a stream pipeline; I kept the same method signature and return type."

**Your tasks:**
1. Identify the misconception in Step 3 — what behavior changed that the happy-path demo did not reveal.
2. Explain exactly what `filter(Book::isAvailable)` does when `books` contains a `null` element, and what the original loop did differently.
3. Rewrite Step 3 as a correct verification: trace the null-entry case, decide whether the refactor preserves the requirement, and state the fix (e.g., add `.filter(Objects::nonNull)` before the availability filter).
4. Explain why Step 4's disclosure looks complete but is insufficient because it never names what was *verified* on the null path.

**Why this error is common:** A refactor that produces identical output on the inputs you happen to test is mistaken for one that preserves *all* behavior — but a plausible-looking refactor can silently change behavior on nulls or empties (`Book::isAvailable` calls a method on a null reference and throws), and "behaves identically in the demo" is not "behaves identically."

---

## Part E — Transfer Problem: Verifying AI-generated persistence code

**Same principle, new domain.** You asked Claude Code to generate `Catalog.saveToFile(String path)` and `loadFromFile(String path)`. The methods compile, and a save-then-load in the demo round-trips three books correctly. Before accepting, run the verification discipline against the four data-loss questions you own: What if the file does not exist on first run? What if a read fails mid-file? What if a write fails halfway? How much data loss is acceptable?

Your verification must:
- Restate the Requirement and Evidence (the four data-loss policies) as a checklist.
- Trace the AI code's behavior for the missing-file-on-first-run case specifically — does it crash, return empty silently, or throw?
- Apply the Three-Question Audit, focusing on Question three: which paths are untested?
- Decide what to fix and write one test that pins the first-run case.

**Hint (use only if stuck after 10 minutes):** The demo only exercised "file exists with valid data." The untested path is "file absent on first launch" — AI cannot know your deployment context, so it likely chose one of {throw, silent empty} without being told; your data-loss policy decides which is correct, and that decision is yours, not Claude's.

**Reflection prompt:**
1. Which of the four data-loss questions is a *deployment* decision that AI literally cannot make for you, and why?
2. How is verifying this persistence code structurally identical to Part A's search verification, even though one touches files and the other touches a list?

---

## Part F — Interleaved Review

**Problem F1 (this chapter).** Claude Code generated a `removeBook(String isbn)` method. Write the three pre-ask statements (Requirement, Artifact, Evidence) you *should* have written first, then list the specific Evidence claims you would trace — including at least one edge case the demo would not catch (e.g., ISBN not present). State the threshold rule that decides whether you may accept the method.
*Chapter this draws from: Chapter 95 (Claude Code / verifying AI-generated code).*

**Problem F2 (named previous chapter).** For the AI-generated `searchByTitle` from Part A, write the full five-case test suite — normal/one-result, multiple-results, empty-collection, no-match, and null-input — using `@Test` and the appropriate assertions, and identify which one case fails before the null guard is added. Name each case before writing it.
*Chapter this draws from: Chapter 13 — Collections and the testing discipline (the five-case taxonomy: normal, empty, no-match, boundary, invalid input).*

**Problem F3 (discrimination).** You are given three AI-generated artifacts: (a) a method, (b) a unit test, (c) a refactor of working code. For each, state the *one* verification question that most reliably exposes its characteristic failure mode — untested edge case for the method, happy-path-only assertion for the test, changed behavior on null/empty for the refactor. Then explain how you decided which failure mode pairs with which artifact.
*Note to instructor: F3 forces the student to match the verification move to the artifact type instead of applying a single rote check to everything.*

**Closing reflection:** Across F1–F3 the recurring question is: which stated claim did the demo *not* exercise? Name, for each problem, the untested claim that verification had to reach.

---

## Instructor Notes

**Common errors:**
- Accepting AI code because it compiles and passes the demo, without tracing the edge cases the demo never touched (null, empty, boundary, missing file).
- Trusting an AI-written test suite that is fully green but asserts only the happy path, then treating "tests pass" as "requirement covered."
- Accepting a plausible refactor as behavior-preserving when it silently changes behavior on nulls or empties, and writing a disclosure that names what AI did but not what the student verified.

**Signs a student needs to return:**
- They cannot explain a component's behavior without borrowing Claude's words, or cannot name the alternative design that was rejected.
- Their AI Use Disclosure cannot fill in "what I changed or rejected and why" — a sign they accepted everything.

**Scaffolding adjustments:** If a student struggles with Part A, give them the five-claim checklist pre-filled and have them only build the trace table, circling the row the demo never ran. If a student finishes Part F quickly, have them write a deliberately-wrong AI method and a happy-path test that hides its bug, then hand it to a peer to catch — teaching the failure mode from the attacker's side.

**Domain adaptation note:** Replace the library search/borrow/persistence artifacts with inventory quantity checks or scheduling conflict detectors; the discipline — write Requirement/Artifact/Evidence first, trace every claim through the code path, audit untested branches — is identical regardless of domain.
