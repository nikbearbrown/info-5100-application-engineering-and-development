# Module 13 — Collections and Iterators: JUnit Testing
## Exercise Set

**Learning Objectives**
1. Write JUnit tests with correct setup-execution-assertion structure
2. Cover all five test case types for a given method
3. Reason about what passing tests prove and what they do not
4. Use regression tests as safety nets for change

**Core Concepts:** JUnit, `@Test` annotation, `assertEquals` / `assertTrue` / `assertNull` / `assertThrows`, setup-execution-assertion anatomy, five cases (normal / empty / no-match / boundary / invalid), passing test as limited proof, regression as previously-working behavior failure, test coverage reasoning

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1.** (Tests: recall — three parts of a JUnit test)
What are the three parts of a JUnit test? Name each part and describe what it does in one sentence. Use a test for `Library.addBook()` as your example to make each part concrete.

**Exercise 2.** (Tests: true/false — passing tests prove correctness)
True or False — then explain your answer in 2–3 sentences:

> "If all your JUnit tests pass, your program is correct."

**Exercise 3.** (Tests: five test case types — applied to a single method)
Name the five test case types from this chapter. For a `findByStudentId(String id)` method, write a one-sentence description of what each case would test. Be specific — name the input and what the method should return or do for each case.

**Exercise 4.** (Tests: vocabulary — regression and regression tests)
What is a regression? Why is a regression test useful even after the bug that caused it has been fixed? Answer in 3–4 sentences.

**Exercise 5.** (Tests: true/false — more tests always better)
True or False — then explain your answer in 2–3 sentences:

> "Writing more test cases always improves your test suite quality."

---

## Tier 2 — Application

*(Tests: writing tests, error analysis, reasoning about proof, AI interaction, regression)*

**Exercise 6.** (Tests: writing JUnit tests — four behaviors of searchByTitle)
A `Catalog.searchByTitle(String query)` method should:
- Return all books whose title contains the query (case-insensitive)
- Return an empty list when no books match the query
- Return an empty list when the catalog is empty
- Throw `IllegalArgumentException` for a null query

Write four JUnit tests — one for each behavior. Use correct `@Test` structure with setup, execution, and assertion. Include concrete book titles and queries (not `"test"` or `"abc"`).

**Exercise 7.** (Tests: error analysis — test with no assertion, wrong test anatomy)
A student writes this JUnit test for a library checkout:

```java
@Test
public void testCheckout() {
    Library library = new Library();
    library.addBook(new Book("1984", "Orwell"));
    library.addPatron(new Patron("Alice", "P001"));
    library.checkout("1984", "P001");
    System.out.println("Checkout worked!");
}
```

Identify two problems with this test. For each problem: name it and write a corrected version of the relevant part.

**Exercise 8.** (Tests: reasoning about what tests prove — precise language)
A student runs 15 JUnit tests on their checkout system and all pass. They declare: *"My checkout system is correct."*

Write a 3-sentence response that:
- (a) States precisely what the 15 passing tests do prove
- (b) States one specific thing the tests do not prove
- (c) Gives a concrete example of a bug that could exist in a checkout system even with all 15 tests passing

**Exercise 9.** (Tests: AI interaction — five test case types, gaps in AI suggestion)
A student writes a `Catalog.findByIsbn(String isbn)` method and asks an AI: *"What test cases should I write for this method?"*

The AI suggests:

> "Test with a valid ISBN, test with an invalid ISBN, and test with a null ISBN. Three tests should be sufficient."

- Identify the strongest point in the AI's response.
- Identify which of the five test case types the AI missed. There are at least two.
- Write the corrected and complete list of test cases, using the five-case taxonomy as your framework.

**Exercise 10.** (Tests: regression — diagnosing a feature-caused test failure)
A developer adds a new feature to a library system: the ability to add multiple copies of the same book (identified by the same ISBN). After adding this feature, a previously passing test for `findByIsbn()` now fails.

- (a) What is this called? Use the correct term from this chapter.
- (b) What does this failure tell you about the new feature?
- (c) Write a one-sentence description of the specific test that most likely failed and what it revealed about the interaction between the new feature and `findByIsbn()`.

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration, named prior chapters explicitly)*

**Exercise 11.** (Tests: synthesis — Ch 13 + Ch 8, persistence round-trip test)
In Ch 8, you learned to save and load data with CSV persistence. In Ch 13, you learned to write tests with correct structure and the five-case taxonomy.

Write a JUnit test (in real Java or clean pseudocode) for the persistence round-trip: save a catalog of three books to a CSV file, then load the CSV into a new catalog object, and verify that the loaded catalog contains the same three books.

- Identify which of the five test case types this test represents.
- Explain what it proves and one thing it does not prove.

A surface answer writes the test. A strong answer has correct setup-execution-assertion structure, explicitly tests both directions of the round-trip (save AND load), and distinguishes between what the test proves and what would require additional tests to prove.

**Exercise 12.** (Tests: synthesis — Ch 13 + Ch 4, test failure as symptom, debugging loop)
In Ch 4, you learned to use breakpoints and the hypothesis-isolate-test debugging loop to find evidence. In Ch 13, you learned that a test failure reveals a symptom, not a cause.

A test fails after a refactor. Describe:
- (a) What you know from the test failure alone — what it tells you and what it does not tell you
- (b) How you would use the debugging loop from Ch 4 to move from symptom to root cause — describe the specific steps
- (c) Why "fixing the test" (changing the expected value to match the new output) is not the same as fixing the bug, and what that approach hides

A surface answer describes debugging steps. A strong answer distinguishes test failure as symptom (Ch 13) from root cause (Ch 4), uses hypothesis-isolate-test vocabulary, and explicitly addresses the "fix the test" anti-pattern as a form of suppressing evidence.

---

## Tier 4 — Challenge

*(No answer key. Rubric only. Open-ended analysis.)*

**Exercise 13.** (Tests: taxonomy gap — identifying a sixth category of test)
The five-case taxonomy (normal, empty, no-match, boundary, invalid) covers many common failure modes but not all. Identify one class of behavior that the five-case taxonomy does not adequately cover — one type of failure that requires a sixth category of test.

Justify why this category is genuinely different from the five existing ones. Give a concrete example from a library or student enrollment system. Write a test (real JUnit or clean pseudocode) that catches a bug the five-case taxonomy would miss.

**Rubric — what distinguishes a strong response:**
- Identifies a real gap rather than a variation on an existing case (e.g., "sequence-dependent state," "concurrent modification," "side-effect leakage across tests," "floating-point precision," "locale-dependent behavior")
- Justifies why it is a new category — explains what property of the system it tests that none of the five cases test
- Provides a concrete test with setup, execution, and assertion that catches a specific real bug
- The proposed bug is plausible in the named domain (library/enrollment) — not contrived

---

## Full Answer Key — Tiers 1–3

### Exercise 1
The three parts of a JUnit test:

1. **Setup** — creates the objects and initial state the test needs. Example: `Library library = new Library(); Book book = new Book("Dune", "Herbert");`
2. **Execution** — calls the method being tested. Example: `library.addBook(book);`
3. **Assertion** — verifies the result matches expectation. Example: `assertEquals(1, library.getBookCount());`

### Exercise 2
**False.** Passing tests only prove that the specific behaviors those tests check work correctly with the specific inputs those tests use. They do not prove correctness for inputs not tested, behaviors not covered by any test, or interactions between components not exercised. A program can pass 100 tests and still have a bug on the 101st input.

### Exercise 3
Five cases applied to `findByStudentId(String id)`:

1. **Normal:** Search for an ID that exists — e.g., `"S1042"` — and verify the correct `Student` object is returned.
2. **Empty:** Call `findByStudentId("S1042")` on an empty enrollment system and verify `null` (or an empty result) is returned without throwing an exception.
3. **No-match:** Search for an ID that does not exist in a non-empty system — e.g., `"S9999"` — and verify `null` is returned.
4. **Boundary:** Search for the first and last students added (edge positions in the underlying collection) to verify ordering does not cause lookup failures.
5. **Invalid:** Pass `null` as the ID and verify the method throws `IllegalArgumentException` rather than a `NullPointerException`.

### Exercise 4
A regression is when a change to code causes a previously correct, passing behavior to break. A regression test documents that specific behavior by encoding it as a test case — even after the original bug is fixed. It remains useful because future changes could re-introduce the same failure. Without the regression test, a developer making an unrelated change would not know they had broken a previously fixed behavior until users reported it.

### Exercise 5
**False.** More tests only improve a suite if they cover new behaviors or new cases not already tested. Writing five tests for the same normal input adds no additional proof — it covers the same case five times. Worse, a large suite of redundant tests increases maintenance cost without increasing confidence. Quality of test coverage (which behaviors are exercised) matters more than quantity of test count.

### Exercise 6
```java
@Test
public void searchByTitle_returnsMatchingBooks_whenTitleContainsQuery() {
    // Setup
    Catalog catalog = new Catalog();
    catalog.add(new Book("The Hitchhiker's Guide to the Galaxy", "Adams"));
    catalog.add(new Book("A Farewell to Arms", "Hemingway"));
    // Execution
    List<Book> results = catalog.searchByTitle("hitchhiker");
    // Assertion
    assertEquals(1, results.size());
    assertEquals("The Hitchhiker's Guide to the Galaxy", results.get(0).getTitle());
}

@Test
public void searchByTitle_returnsEmptyList_whenNoTitleMatches() {
    Catalog catalog = new Catalog();
    catalog.add(new Book("The Hitchhiker's Guide to the Galaxy", "Adams"));
    List<Book> results = catalog.searchByTitle("Moby");
    assertTrue(results.isEmpty());
}

@Test
public void searchByTitle_returnsEmptyList_whenCatalogIsEmpty() {
    Catalog catalog = new Catalog();
    List<Book> results = catalog.searchByTitle("Hitchhiker");
    assertTrue(results.isEmpty());
}

@Test
public void searchByTitle_throwsIllegalArgumentException_whenQueryIsNull() {
    Catalog catalog = new Catalog();
    assertThrows(IllegalArgumentException.class, () -> catalog.searchByTitle(null));
}
```

### Exercise 7
**Problem 1 — No assertion:**
The test calls `library.checkout(...)` and prints to console, but asserts nothing. If the checkout silently fails or corrupts state, the test passes anyway. A `System.out.println` is not an assertion.

Correction: Add an assertion, e.g., `assertTrue(library.isCheckedOut("1984", "P001"))` or `assertEquals(CheckoutStatus.CHECKED_OUT, library.getStatus("1984"))`.

**Problem 2 — Test name does not describe the expected behavior:**
`testCheckout` does not say what outcome is being verified. If this test later fails, the name provides no information about what broke.

Correction: Rename to `checkout_marksBookAsCheckedOut_whenBookAndPatronExist()`.

### Exercise 8
(a) The 15 passing tests prove that for each specific input and scenario covered by those 15 tests, the checkout system produces the expected output.

(b) The tests do not prove that the system handles any input or scenario not represented in those 15 tests — for example, checking out a book that has already been checked out by another patron.

(c) A concrete undetected bug: the system allows the same book to be checked out to two different patrons simultaneously if the second checkout call happens before the first is recorded to disk. If none of the 15 tests test concurrent or rapid successive checkouts, this bug exists and all 15 tests pass.

### Exercise 9
**Strongest point:** The AI correctly identified the invalid case (null ISBN) and the valid case (a found book). Null handling is a common source of bugs and is appropriate to test.

**Cases the AI missed:**
- **Empty catalog case:** `findByIsbn` called on an empty catalog — the AI did not mention this.
- **No-match case:** A non-null ISBN that does not exist in a non-empty catalog — "invalid ISBN" is ambiguous (could mean malformed format), not the same as an ISBN that is syntactically valid but absent.
- **Boundary case:** The first and last books added, to verify the underlying data structure does not skip edge positions.

**Corrected test case list using the five-case taxonomy:**
1. Normal: ISBN `"978-0-06-112008-4"` exists in the catalog — returns the correct `Book`.
2. Empty: catalog is empty — returns `null` (or throws, per contract).
3. No-match: ISBN `"978-0-00-000000-0"` does not exist in a non-empty catalog — returns `null`.
4. Boundary: the first and last books added to the catalog can be found by their ISBNs.
5. Invalid: `null` ISBN — throws `IllegalArgumentException`.

### Exercise 10
(a) This is called a **regression** — a previously passing behavior that now fails due to a code change.

(b) The failure indicates that the new feature (multiple copies per ISBN) changed the contract or behavior of a method that other code depended on. Specifically, it suggests `findByIsbn()` was written with the assumption that one ISBN maps to exactly one book, and the new feature violated that assumption.

(c) The test that likely failed: `findByIsbn_returnsCorrectBook_whenIsbnExists()` — after adding the multiple-copy feature, `findByIsbn()` may now return a list or the first match rather than a single `Book`, causing the assertion `assertEquals(book, result)` to fail because the return type or behavior changed.

### Exercise 11
```java
@Test
public void saveAndLoad_roundTrip_preservesAllBooks() throws IOException {
    // Setup
    Catalog original = new Catalog();
    original.add(new Book("978-0743273565", "The Great Gatsby", "Fitzgerald"));
    original.add(new Book("978-0061120084", "To Kill a Mockingbird", "Lee"));
    original.add(new Book("978-0451524935", "1984", "Orwell"));
    String testFile = "test_catalog_roundtrip.csv";

    // Execution
    CsvPersistence.save(original, testFile);
    Catalog loaded = CsvPersistence.load(testFile);

    // Assertion
    assertEquals(3, loaded.size());
    assertNotNull(loaded.findByIsbn("978-0743273565"));
    assertEquals("The Great Gatsby", loaded.findByIsbn("978-0743273565").getTitle());
}
```

**Case type:** This is a **normal case** test for the persistence system — it tests the primary happy-path behavior (save and load three books successfully).

**What it proves:** That saving three complete book records and reloading them produces a catalog with the same count and the same data for the tested fields.

**What it does not prove:** That the round-trip preserves all fields (e.g., if a `notes` field is not serialized, this test would not catch it). It also does not prove that loading a corrupted or empty CSV file is handled correctly.

### Exercise 12
(a) From the test failure alone, you know: a method that previously returned (or did) X now returns (or does) something different after the refactor. You do not know why — the failure is a symptom pointing to a location, not an explanation of the cause. The specific line of code that changed behavior is unknown until you investigate.

(b) Using the Ch 4 debugging loop:
1. **Form a hypothesis** — the refactor changed method Y, so the failure is likely in method Y or something Y calls.
2. **Set a breakpoint** at the entry to the failing method and inspect input values.
3. **Isolate** — step through the method to find where the actual output diverges from the expected output.
4. **Test the hypothesis** — check whether reverting the refactored line restores the passing behavior.
5. Repeat with a narrowed hypothesis if the first is wrong.

(c) Changing the expected value in the test to match the new (wrong) output hides the bug: it records "this new broken behavior is acceptable" and removes the test's ability to detect future regressions of the same behavior. The test now passes, but the underlying change — which broke the contract the method was supposed to fulfill — is no longer detectable. This is sometimes called "papering over" a failure: the symptom disappears but the disease remains.

---

## Instructor Notes

**Common student errors in this module:**

1. **Tests with no assertions:** Exercise 7's pattern — using `System.out.println` as a substitute for `assertEquals` — is extremely common. Students believe if the code runs without crashing, the test is passing. Demonstration: write a method that returns the wrong value, wrap it in a test with only a print statement, and show it "passes." Then add the assertion and watch it fail.

2. **Conflating "all tests pass" with "correct":** Exercise 8 addresses this directly. The corrective framing: tests are *evidence*, not *proof*. Each test is a specific claim. No finite number of specific claims proves a universal statement.

3. **Five-case coverage gaps:** Students write one or two tests (usually normal + null) and feel done. Exercises 3, 6, and 9 reinforce the taxonomy. Consider running Exercise 9 as a class activity: show the AI's response on screen and ask students to identify the gaps before reading the answer.

**Sequencing recommendation:** Assign Exercise 1 (anatomy) and Exercise 6 (write tests) before Exercise 7 (error analysis). Students who have written at least four tests with correct structure find the errors in Exercise 7 obvious. Students who have not written tests yet find Exercise 7 abstract.

**Tier 3 notes:** Exercise 11 requires Ch 8 persistence vocabulary. If students did not implement CSV persistence in Ch 8, substitute: "write a test for a `toString()` and `fromString()` round-trip on a single Book object." Exercise 12 requires Ch 4 debugging vocabulary (breakpoint, hypothesis, isolate). Students who did not internalize the Ch 4 loop will give generic "I would debug it" answers — push them to name the specific steps and the specific hypothesis.

**Tier 4 note:** Common valid sixth categories include: concurrent modification (two threads modify catalog simultaneously), test isolation failure (one test leaves state that corrupts the next test's setup), floating-point precision (GPA calculations that are close but not equal to expected), and locale-dependent behavior (date parsing that works in one timezone but not another). Accept any of these with a concrete justification. Reject "edge case" as a category name — that is not meaningfully different from boundary.
