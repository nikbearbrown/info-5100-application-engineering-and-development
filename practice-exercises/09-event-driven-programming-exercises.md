# Module 9 — Event-Driven Programming: Java Collections Framework
## Exercise Set

**Learning Objectives**
1. Choose collection types based on operation patterns (operation profiles)
2. Design and verify `Comparator` chains, including null handling
3. Use the stream API for filter/sort/collect pipelines
4. Specify operation profiles before choosing a collection type

---

## Tier 1 — Warm-Up

*(Tests: recall, vocabulary, true/false with explanation)*

---

**Exercise 1** (Tests: recall — HashMap vs ArrayList lookup performance)

What is the primary performance difference between looking up an element by key in a `HashMap` versus searching for it by value in an `ArrayList`? Express both in O-notation and explain what the notation means in plain terms for each case.

---

**Exercise 2** (Tests: true/false — Set and index access)

**True or False:** "A `Set` is the right collection to use when you need to retrieve elements by their index position."

State whether the claim is true or false, then write two to three sentences explaining what a `Set` does guarantee and what operation it is optimized for instead.

---

**Exercise 3** (Tests: vocabulary — operation profiles)

What is an **operation profile**? What two pieces of information does it capture, and why should you write it before choosing a collection type rather than after?

---

**Exercise 4** (Tests: recall — Comparable vs Comparator)

What is the difference between `Comparable` and `Comparator` in Java? Give a concrete example of when you would use each, using a library or hospital system scenario.

---

**Exercise 5** (Tests: true/false — ArrayList dual use)

**True or False:** "You can use the same `ArrayList` for both O(1) lookup by student ID and O(1) membership testing."

State whether the claim is true or false, then write two to three sentences explaining what data structure would be required for each operation and why a single `ArrayList` cannot serve both.

---

## Tier 2 — Application

*(Tests: scenario design, error analysis, AI interaction)*

---

**Exercise 6** (Tests: operation profile design — hospital appointment system)

A hospital appointment system needs three distinct collections. For each collection below:
- Write the operation profile (primary operation + performance requirement)
- Choose the correct Java collection type
- Justify your choice in one sentence

**(a)** A collection of `Doctor` objects that must support lookup by doctor ID in O(1) average time.

**(b)** A collection of upcoming appointments that must be displayed in chronological order.

**(c)** A collection of patient IDs that currently have active appointments, used only for fast membership testing (checking whether a patient has an active appointment).

---

**Exercise 7 — Error Analysis** (Tests: error identification — Comparator design)

A student writes a `Comparator` to sort books by publication year:

```java
Comparator<Book> byYear = (a, b) -> a.getYear() - b.getYear();
```

They then chain it with a title sort:

```java
Comparator<Book> byYearThenTitle = byYear.thenComparing(b -> b.getTitle());
```

During testing, they discover two problems: incorrect sort order for some year values, and a `NullPointerException` when sorting books with null titles.

**(a)** Explain why subtracting years in a `Comparator` can produce incorrect sort results. Provide a specific example with year values that would produce the wrong answer.

**(b)** Identify what causes the `NullPointerException` in the chained comparator.

**(c)** Rewrite both the year comparator and the chained comparator to fix both problems. Use `Comparator.comparingInt()` and `Comparator.nullsLast()` where appropriate.

---

**Exercise 8** (Tests: stream pipeline design — enrollment system)

A student grade management system has a `List<Enrollment> enrollments`. Each `Enrollment` has fields: `courseId`, `studentLastName`, `studentId`, and `grade`.

**(a)** Write a stream pipeline that:
- Filters to enrollments for a specific `courseId` (e.g., `"CS3200"`)
- Sorts by student last name alphabetically
- Collects to a new `List<Enrollment>`

**(b)** Explain what happens at runtime if you call `.sorted()` with no argument on a stream of `Enrollment` objects that do not implement `Comparable`. Be specific about the exception type and when it is thrown.

---

**Exercise 9 — AI Interaction** (Tests: evaluating AI-generated collection advice)

A student asks an AI assistant: *"I need to find a student by their ID quickly in my enrollment system."*

The AI responds:

> "Use a `List<Student>` and loop through it with a for loop checking `if (student.getId().equals(targetId))`. This is simple and readable."

Answer the following:

**(a)** Identify the strongest point in the AI's response (what, if anything, is correct or useful).

**(b)** Identify the performance problem for a university enrollment system with thousands of students.

**(c)** Write a corrected recommendation using the operation profile framework: state the operation profile first, then recommend a collection type, then show the lookup code.

---

**Exercise 10** (Tests: collection limitation analysis — overdue tracking system)

A library overdue tracking system uses a single `ArrayList<Book> overdueBooks` for all operations. The system needs to:

**(a)** Quickly check whether a specific book (identified by ISBN) is currently overdue

**(b)** Display all overdue books sorted by due date

**(c)** Count the number of overdue books without iterating through the list

For each operation, identify the limitation of using a single `ArrayList`, and describe which collection type or combination would serve that operation better.

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration — must name prior chapters explicitly)*

---

**Exercise 11** (Tests: Ch 9 + Ch 5 — revisiting the Catalog design)

*This exercise connects Module 9 with Module 5.*

In Chapter 5, you built a `Catalog` class that stored `Book` entities in an array and supported query methods including `findByIsbn()`. In Chapter 9, you learned that collection choice should be driven by operation profiles.

Revisit the `Catalog` design by answering all four parts:

**(a)** What operations does the `Catalog` need to support, based on the query methods you implemented in Chapter 5? List at least three.

**(b)** Write the operation profile for the most performance-critical operation — the one that is called every time a book is looked up, added, or checked out.

**(c)** What collection type from Chapter 9 would be more appropriate than an array for the `Catalog`? Justify your answer using the operation profile.

**(d)** What changes in the implementation of `findByIsbn()` when you switch from the Chapter 5 array to the Chapter 9 collection? Show the before and after versions.

A strong answer uses operation profile vocabulary from Chapter 9 and explicitly connects the Chapter 5 query requirements to the Chapter 9 collection choice.

---

**Exercise 12** (Tests: Ch 9 + Ch 8 — collection type and CSV persistence)

*This exercise connects Module 9 with Module 8.*

In Chapter 8, you wrote `saveToFile()` and `loadFromFile()` methods that iterated over a collection to write CSV lines and reconstructed the collection from CSV lines. In Chapter 9, you learned that different collection types have different iteration patterns and different construction requirements.

Consider changing the library catalog from `ArrayList<Book>` to `HashMap<String, Book>` (where the key is the ISBN string):

**(a)** Write the changed iteration code in `saveToFile()`. What is different about iterating a `HashMap` compared to an `ArrayList`?

**(b)** Write the changed reconstruction code in `loadFromFile()`. What additional step is required when adding each `Book` to the `HashMap` that was not required when adding to the `ArrayList`?

**(c)** Does the CSV format itself need to change? Explain why or why not.

A strong answer shows correct `HashMap` iteration (using `values()` or `entrySet()`), explains the `put(isbn, book)` reconstruction step, and correctly identifies that the CSV line format is unchanged.

---

## Tier 4 — Challenge

*(No answer key. Rubric only.)*

---

**Exercise 13** (Tests: multi-collection synchronization — BookRegistry design)

A library system maintains three parallel collections for `Book` objects:
- A `List<Book>` for ordered display
- A `HashMap<String, Book>` for lookup by ISBN
- A `HashSet<String>` of ISBNs for books currently checked out

All three must stay synchronized: when a book is added, removed, or checked out, all three collections must be updated together. Currently this synchronization is done by callers, which means it is easy to forget one update.

Design a wrapper class called `BookRegistry` that encapsulates all three collections and exposes only these public methods: `add(Book book)`, `remove(String isbn)`, `findById(String isbn)`, `isCheckedOut(String isbn)`, and `getAllSorted(Comparator<Book> comparator)`.

Your answer must address:

**(a)** The field declarations for all three internal collections

**(b)** The class invariant that `BookRegistry` must maintain (state it as a precise condition, not a vague description)

**(c)** The time complexity of each public method — which are O(1), which are O(n), and which are O(n log n)?

**(d)** What breaks if a caller modifies the `List<Book>` returned by `getAllSorted()` directly, and how would you prevent it?

**Rubric — a strong response will:**
- Declare all three fields with correct types (`List<Book>`, `HashMap<String, Book>`, `HashSet<String>`)
- State the invariant precisely: every `Book` in the List is also in the Map under its ISBN as key, and the Set contains exactly the ISBNs of checked-out books; no extra entries exist in any collection
- Correctly identify: `add()`, `remove()`, `findById()`, `isCheckedOut()` as O(1) average; `getAllSorted()` as O(n log n) due to sort
- Identify that returning the internal List directly allows a caller to add or remove elements from it, violating the invariant; propose returning a defensive copy (`new ArrayList<>(sorted)`) or an unmodifiable wrapper (`Collections.unmodifiableList(sorted)`)
- Note that `getAllSorted()` should sort a copy, not the internal list, to avoid permanently reordering the list

---

## Full Answer Key

*(Tiers 1–3 only)*

---

### Tier 1 Answers

**Exercise 1**
- `HashMap` lookup by key: **O(1)** average case. The key is hashed to a bucket index directly, so the lookup time does not grow as the number of entries grows.
- `ArrayList` search by value: **O(n)**. There is no index — the only way to find a matching element is to scan each element from the beginning until a match is found. In the worst case (no match, or match at the end), all n elements are examined.

In plain terms: a `HashMap` lookup takes roughly the same time whether the map has 10 entries or 10,000. An `ArrayList` search takes ten times as long with 10,000 elements as with 1,000.

---

**Exercise 2**
**False.**

A `Set` provides no index-based access — there is no `set.get(3)` method. Sets are unordered (in the case of `HashSet`) or sorted (in the case of `TreeSet`), but neither supports retrieval by position. What a `Set` does guarantee is fast membership testing: `set.contains(element)` runs in O(1) average time for a `HashSet`. The right use of a `Set` is answering the question "is this element present?" not "give me the element at position i."

---

**Exercise 3**
An operation profile describes: (1) the primary operation that will be performed on a collection (e.g., lookup by key, membership testing, ordered iteration), and (2) the performance requirement for that operation (e.g., O(1), O(log n)).

You should write it before choosing a collection because different collection types excel at different operations — no single collection is best at everything. Choosing first and profiling second leads to discovering a mismatch after code is written. Writing the operation profile first makes the choice a consequence of the requirement rather than a guess.

---

**Exercise 4**
`Comparable` is an interface implemented by a class to define its natural ordering. The class defines how instances of itself compare to each other via `compareTo()`. Use `Comparable` when a class has one obvious, stable ordering that makes sense in all contexts — for example, `Patient` sorted by patient ID.

`Comparator` is a separate object that defines an ordering from outside the class. Use `Comparator` when you need multiple orderings (e.g., sort `Doctor` by name in one view, by specialty in another), or when you cannot modify the class to add `compareTo()`. In a library system, `Book` might implement `Comparable` to sort by ISBN by default, but a display screen might use a `Comparator<Book>` to sort by title or author without changing the `Book` class.

---

**Exercise 5**
**False.**

An `ArrayList` stores elements in order by position. Looking up a student by ID requires iterating through the list until a match is found — O(n), not O(1). Membership testing (is this student already in the collection?) also requires a linear scan — O(n), not O(1). For O(1) lookup by ID, a `HashMap<String, Student>` is required. For O(1) membership testing, a `HashSet<String>` of student IDs is required. A single `ArrayList` cannot provide O(1) performance for either of these operations.

---

### Tier 2 Answers

**Exercise 6**

**(a)** Doctor lookup by ID:
- Operation profile: lookup by key (doctor ID), O(1) average
- Collection type: `HashMap<String, Doctor>` where the key is the doctor ID string
- Justification: `HashMap` provides O(1) average lookup by key, which is exactly the required operation.

**(b)** Appointments in chronological order:
- Operation profile: ordered iteration by date/time
- Collection type: `List<Appointment>` (sorted using a `Comparator<Appointment>` by date and time before display)
- Justification: `List` preserves insertion order and supports sorting; a `TreeSet` could maintain sorted order at insertion cost, but a `List` with explicit sort before display is simpler and sufficient.

**(c)** Active patient IDs — membership testing:
- Operation profile: membership testing by patient ID, O(1) average
- Collection type: `HashSet<String>` of patient ID strings
- Justification: `HashSet.contains()` runs in O(1) average time, which is exactly what fast membership testing requires; no ordering or positional access is needed.

---

**Exercise 7**

**(a)** Subtracting years can produce incorrect results due to integer overflow. A `Comparator` contract requires returning a negative number for less-than, zero for equal, and a positive number for greater-than. Subtraction only satisfies this contract if the difference fits in an `int`. Consider: year `2147483600` minus year `-100` overflows a 32-bit int and produces a negative number, incorrectly indicating that the larger year is smaller. The safe approach is to use `Integer.compare(a, b)`.

**(b)** The `NullPointerException` occurs because `Comparator.thenComparing(b -> b.getTitle())` calls `compareTo()` on the result of `getTitle()`. If `getTitle()` returns `null`, `compareTo()` is called on a null reference, throwing `NullPointerException`. The lambda does not provide null handling.

**(c)** Corrected comparators:
```java
Comparator<Book> byYear = Comparator.comparingInt(Book::getYear);

Comparator<Book> byYearThenTitle = byYear
    .thenComparing(Comparator.comparing(Book::getTitle, Comparator.nullsLast(String::compareTo)));
```
`Comparator.comparingInt()` uses `Integer.compare()` internally, avoiding overflow. `Comparator.nullsLast()` pushes null titles to the end and avoids the `NullPointerException`.

---

**Exercise 8**

**(a)** Stream pipeline:
```java
List<Enrollment> cs3200Enrollments = enrollments.stream()
    .filter(e -> e.getCourseId().equals("CS3200"))
    .sorted(Comparator.comparing(Enrollment::getStudentLastName))
    .collect(Collectors.toList());
```

**(b)** If `.sorted()` is called with no argument on a stream of `Enrollment` objects that do not implement `Comparable`, Java attempts to cast each element to `Comparable` at runtime. This throws a `ClassCastException` — not a compile-time error, because the type system does not enforce `Comparable` on the stream's generic type at compile time. The exception is thrown the first time two elements are compared during the sort, which is at `.sorted()` execution, not at `.collect()`.

---

**Exercise 9**

**(a)** Strongest point: the suggestion is readable and correct for very small datasets. A for-each loop with an equality check is simple to understand and debug, and for a system with a small number of students it works correctly.

**(b)** Performance problem: this is an O(n) linear scan. For a university with 20,000 students, each lookup examines up to 20,000 entries. If student lookup is called frequently (e.g., on every page load, every grade submission), the cumulative cost becomes significant. At 10,000 lookups per session against 20,000 students, this is 200 million comparisons vs. effectively 10,000 with a `HashMap`.

**(c)** Corrected recommendation using operation profile:
- Operation profile: lookup by student ID, O(1) average required
- Collection type: `HashMap<String, Student>` where the key is the student ID string
- Lookup code:
```java
HashMap<String, Student> studentDirectory = new HashMap<>();
// ... populate ...
Student found = studentDirectory.get(targetId);  // O(1) average
```
Write the operation profile first: "I need to look up students by ID frequently. This requires O(1) average performance." That profile points directly to `HashMap`.

---

**Exercise 10**

**(a) Check if a book is overdue by ISBN:**
Limitation of `ArrayList`: membership check by ISBN requires a linear scan (O(n)) — there is no index by ISBN. For every "is this book overdue?" query, the entire list must be examined.
Better collection: `HashSet<String>` of ISBNs of overdue books, providing O(1) average `contains()` lookup. The full `Book` objects can still be stored separately.

**(b) Display overdue books sorted by due date:**
Limitation of `ArrayList`: an unsorted `ArrayList` requires an explicit sort before display. If mutations (additions, removals) are frequent, the list must be re-sorted each time, which is O(n log n). The list itself does not maintain sort order.
Better collection: a `List<Book>` is appropriate here, but sorted using a `Comparator<Book>` by due date before display, or a `TreeSet<Book>` with a due-date comparator that maintains sorted order at insertion.

**(c) Count overdue books without iterating:**
Limitation of `ArrayList`: `list.size()` does return the count in O(1), so this operation is already efficient in an `ArrayList`. This is not a case where `ArrayList` fails — it is one of the few operations where it is adequate. No alternative is needed for count alone.

---

### Tier 3 Answers

**Exercise 11**

**(a)** The `Catalog` from Chapter 5 needs to support:
- `findByIsbn(String isbn)` — look up a specific book by ISBN
- `addBook(Book book)` — add a new book to the catalog
- `getAllBooks()` — retrieve all books for display or iteration
- Membership testing — check whether a book with a given ISBN already exists

**(b)** Operation profile for the most performance-critical operation (`findByIsbn`):
- Primary operation: lookup by ISBN (a string key)
- Performance requirement: O(1) average, since this is called on every checkout, return, and availability check

**(c)** A `HashMap<String, Book>` where the key is the ISBN string is more appropriate than an array. The operation profile requires O(1) lookup by key. Arrays require a linear scan (O(n)) to find a book by ISBN because they have no key index. A `HashMap` provides O(1) average lookup by key directly.

**(d)** Before (Chapter 5 array):
```java
public Book findByIsbn(String isbn) {
    for (Book book : books) {  // O(n) linear scan
        if (book.getIsbn().equals(isbn)) {
            return book;
        }
    }
    return null;
}
```

After (Chapter 9 HashMap):
```java
public Book findByIsbn(String isbn) {
    return catalog.get(isbn);  // O(1) average
}
```
The entire loop disappears. The ISBN is passed directly to `get()`, and the `HashMap` performs the lookup internally in O(1) average time.

---

**Exercise 12**

**(a)** Changed `saveToFile()` iteration:
```java
// ArrayList version (Chapter 8):
for (Book book : bookList) {
    writer.write(book.toCSV());
    writer.newLine();
}

// HashMap version (Chapter 9):
for (Book book : bookMap.values()) {
    writer.write(book.toCSV());
    writer.newLine();
}
```
The difference: `HashMap` is not directly iterable by value with a for-each. You must call `.values()` to get a `Collection<Book>` of the map's values, then iterate that. Alternatively, `.entrySet()` gives key-value pairs if you need the key as well, but since the ISBN is already in the `Book` object, `.values()` is sufficient.

**(b)** Changed `loadFromFile()` reconstruction:
```java
// ArrayList version (Chapter 8):
bookList.add(book);

// HashMap version (Chapter 9):
bookMap.put(book.getIsbn(), book);
```
The additional step is extracting the key (the ISBN) from the parsed `Book` object and using `put(key, value)` instead of `add(value)`. The `Book` object must be constructed from the CSV line first (identical to the ArrayList version), but then instead of appending to a list, it is inserted into the map under its ISBN key.

**(c)** The CSV format itself does not change. A CSV line represents a `Book` object's fields — `isbn,title,author,year` — and that representation is independent of which Java collection holds the objects. The CSV format is the object's serialization format; the collection is the in-memory access structure. Switching from `ArrayList` to `HashMap` changes how Java code iterates and retrieves `Book` objects, but it does not change what data a `Book` holds or how that data is written as text.

---

## Instructor Notes

**Common errors to watch for:**

- **Exercise 1:** Students often state that `HashMap` is "faster" without explaining why. Require O-notation and a plain-language explanation. Watch for students who say `HashMap` is O(1) "always" — the correct answer is O(1) **average**, with O(n) worst case when hash collisions degrade performance.

- **Exercise 3:** Students confuse operation profiles with Big-O notation in isolation. The profile has two parts: the operation type and the performance requirement. "O(1) lookup" is incomplete — "lookup by student ID in O(1)" is an operation profile.

- **Exercise 7b:** Students frequently say the `NullPointerException` is thrown "because the title is null." Require them to explain the mechanism: `thenComparing` invokes `compareTo()` on the result of the key extractor, and calling a method on `null` throws `NPE`. The fix is not to avoid null titles but to handle them in the comparator.

- **Exercise 7c:** Watch for students who use `Comparator.naturalOrder()` instead of `Comparator.nullsLast(String::compareTo)`. These are not equivalent — `naturalOrder()` does not handle null and will still throw `NPE`. Require explicit null handling.

- **Exercise 11:** Students who did not do the Chapter 5 Catalog exercise will struggle with part (a). If needed, allow them to describe what operations a catalog "obviously needs" rather than citing specific method names from their solution. The key insight in part (d) is that the entire for-loop disappears — students often want to keep some iteration logic.

- **Exercise 12:** The most common error is saying the CSV format must change to include the key. It does not — the ISBN is already a field in the CSV line. The key is extracted from the parsed `Book` object, not added to the file. Make this explicit in grading.

- **Exercise 13 (Challenge):** Most students correctly identify the three field types but state the invariant vaguely ("all three stay in sync"). Require a precise statement: the `List`, `Map`, and `Set` contain exactly the same books (no extras, no missing). The mutability issue with `getAllSorted()` is frequently missed — students return the internal list directly. Credit responses that propose `Collections.unmodifiableList()` or a defensive copy, and that also note the internal list should not be sorted in place.

**Suggested point distribution:** Tier 1: 5 pts each. Tier 2: 10 pts each. Tier 3: 15 pts each. Tier 4: 20 pts (rubric-graded).
