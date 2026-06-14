# Module 9 — Event-Driven Programming: Wonder Edition
## Companion Chapter
> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Event-Driven Programming," this chapter covers Java Collections (List, Map, Set), operation profiles, Comparators, Comparable, and the stream filter pipeline.

---

## The Strange Question

A library stores fifty thousand books. Two students write lookup code. Student A iterates a list and checks each ISBN. Student B calls a single method on a map. Both programs return the correct book. Both pass the unit tests.

Why does one of them get fired at scale?

---

## First Intuition

Most people assume a collection is a container. A list holds books. A map holds books. A set holds books. They are all boxes. The question is which box you feel like using today. The familiar one is fine. Lists are flexible. Lists compile. Lists run.

Under this model, the choice of collection type is a style preference, like variable naming. You can use a list for everything and get on with the real work.

> **Planning Metacognitive Prompt:** Before reading further, write down your prediction. If a list and a map both store the same books and both return the correct result for a lookup, what — if anything — could actually go wrong with using the list? Be specific. What would have to be true for the difference to matter?

---

## The Surprise

But something is different between the two programs, and it is not visible in the output.

Student A's program examines each book in sequence until it finds the matching ISBN. With fifty books, the loop runs at most fifty times. With fifty thousand books, it runs at most fifty thousand times. The number of steps grows with the size of the collection. Double the library; double the worst-case lookup time.

Student B's program does not scan. It computes a position directly from the ISBN and retrieves the value. With fifty books, the operation takes a fixed number of steps. With fifty thousand books, it takes the same fixed number of steps. The size of the collection does not change the cost.

Both programs are correct. Their correctness is identical. Their behavior under scale is not.

> **Monitoring Metacognitive Prompt:** Does this surprise you, or did your earlier prediction already anticipate it? If you predicted it, what made you confident? If it surprises you, what assumption in your First Intuition turned out to be false?

The surprise is not resolved yet. The question is not just "which is faster." The question is what it means for a collection to encode an assumption about how you will use it — and why that encoding is invisible until the collection is large.

---

## The Hidden Structure

A collection is not a container. It is a performance contract.

Each Java collection type makes specific operations cheap and other operations expensive. `List` makes iteration and indexed access cheap. Lookup by value — "find the element matching this key" — costs O(n): the worst case scales linearly with the size. `Map` makes keyed lookup cheap: O(1) on average, regardless of size. Its cost is that it imposes no iteration order over entries. `Set` makes membership testing cheap: O(1) on average. Its cost is that elements carry no index and no guaranteed order.

The choice of collection is a decision about which operations deserve O(1) performance. That decision cannot be undone after the rest of the code is written around it. A `List` used as a lookup table compiles, runs, and produces correct output — until the collection is large enough to expose the O(n) cost. By then, the rest of the code may depend on `List` semantics, and migration is expensive.

> **Misconception Checkpoint:** It is tempting to think that correctness guarantees good performance — if the code returns the right answer, the implementation is fine. But correctness and performance are independent properties. A program can be completely correct and unacceptably slow. The correct model holds that collection type determines the performance contract, not the output. Two programs can agree on every answer while disagreeing dramatically on cost.

---

## Try Looking At It This Way

Consider a physical library's reference desk.

A new librarian arrives and stores all call slips in a single stack. Any patron request requires the librarian to flip through the stack from the top until the matching slip appears. This always produces the correct slip. With ten patrons, the delay is negligible. With ten thousand patrons, the delay is not.

An experienced librarian uses a card catalog: a set of drawers organized by the first letter of the patron's name, then alphabetically within that letter. Any patron request requires the librarian to open the correct drawer and locate the slip directly. This also always produces the correct slip. With ten patrons or ten thousand, the number of physical steps is nearly the same.

Now map this to Java collections.

The stack of call slips corresponds to a `List`. The operation is sequential scan. The cost grows with the number of elements. The card catalog corresponds to a `Map`. The operation is direct retrieval by key. The cost is roughly constant regardless of size.

Both mechanisms store the same data. Both return correct results. Their structures encode different assumptions about which operation will be performed most often and how large the collection will grow.

The feature mapping: patron name corresponds to the key in a `Map`. The call slip corresponds to the value. The drawer corresponds to the hash bucket. The alphabetical drawer organization corresponds to the hash function that converts a key into a position.

**Boundaries of this analogy:** A physical card catalog is alphabetically ordered, so range queries ("give me all patrons whose names start with S") are natural. Java's `HashMap` is not ordered — it sacrifices ordering for O(1) lookup. A `TreeMap` preserves key order at the cost of O(log n) operations. The analogy also does not capture how `Set` differs from `Map`. A `Set` is like a registry that records only which patron names are present, not what they checked out.

---

## Where The Analogy Breaks

The card catalog analogy breaks at duplicates and ordering.

A physical card catalog can hold two slips for the same patron name, one behind the other. A `Map` cannot: each key maps to exactly one value. If you insert a second value under the same key, the first is overwritten. The catalog drawer has no equivalent of this constraint.

The analogy also implies that lookup involves some physical traversal — opening a drawer, flipping past a few slips. Java's `HashMap` lookup ideally involves no traversal at all: the hash function computes the slot directly. The drawer metaphor suggests O(log n) behavior; the actual behavior is O(1) average case.

Do not use the card catalog to reason about hash collision behavior or worst-case HashMap performance.

---

## Small Discovery

The following data comes from a different domain: a city's parking enforcement department. Read it and look for a pattern before answering the question below.

| Lot ID | Citation lookups per day | Data structure used | Average lookup time (ms) |
|--------|--------------------------|---------------------|--------------------------|
| A-14   | 12,000                   | sorted array scan   | 47                       |
| B-02   | 12,000                   | hash table          | 2                        |
| C-07   | 850                      | sorted array scan   | 44                       |
| D-11   | 850                      | hash table          | 3                        |
| E-09   | 50                       | sorted array scan   | 41                       |
| F-03   | 50                       | hash table          | 2                        |

Look at the lookup time column. Notice what changes and what does not as the lookup volume increases.

Now predict: if a seventh lot, G-01, uses a sorted array scan and receives 120,000 lookups per day, what would you expect its average lookup time to be — and why?

---

The lookup time for the array scan lots is roughly constant around 44 ms regardless of whether the lot handles 50 or 12,000 lookups per day. The time per lookup does not depend on how many lookups there are — it depends on how many records are in the array being scanned.

This is the key distinction: lookup count per day and lookup cost per operation are different variables. The sorted array scan pays its cost for each lookup regardless of how many lookups are requested. The hash table pays a smaller cost per lookup, regardless of volume.

If G-01 uses a sorted array scan for a collection of the same size as the other lots, its average lookup time would be approximately 44 ms — the same as the other scan-based lots. Volume does not change per-operation cost.

What would change the lookup time is the size of the array being scanned, not the number of queries.

---

## What This Changes

A reader who has worked through this chapter can now explain why two programs with identical outputs can have entirely different scalability properties. They can name the primary operation a collection must support and use that name to select the collection type — rather than defaulting to the familiar one. They can read a `Comparator` chain and identify what ordering rule it encodes, and they can explain why the rule exists as a named object rather than as inline comparison logic.

The question that comes next: collections organize data in memory. But a user does not see memory — they see a screen. The sorted, filtered `List<Book>` is not visible until it is bound to a display component. How does a collection become a view? And when the collection changes — a book is checked out, a new title is added — how does the view learn about the update without receiving a direct reference to the underlying data?

That is the model-view problem. It is where the next module begins.

---

## Wonder Questions

1. A `HashMap` lookup is O(1) average case. But "average case" hides something. What event converts a `HashMap` lookup into O(n) worst case — and under what real-world conditions might an attacker deliberately cause that event?

2. `Comparable` allows only one natural ordering per class. But a book has many plausible natural orders: by title, by author, by ISBN, by publication year. What principle should guide which ordering gets to be "natural" — and is that principle intrinsic to the object, or is it always a convention?

3. The stream pipeline `filter().sorted().collect()` does not modify the source collection. This is described as safe and clean. But what happens to memory when the source collection has one million elements, the filter keeps nine hundred thousand, and the operation is called repeatedly on every user interaction?

4. `Set` eliminates duplicates automatically. But "duplicate" requires a definition of equality. If two `Book` objects have the same ISBN but different author spellings due to a data entry error, are they duplicates? What mechanism in Java controls this definition — and what breaks silently when that mechanism is implemented incorrectly?

5. The chapter recommends choosing a collection type by operation profile before writing code. But in practice, requirements change: a collection built for iteration later acquires a performance-critical lookup requirement. What is the cost of migrating from `List` to `Map` after the rest of the system is already written against `List` semantics — and what design patterns exist to reduce that migration cost?

> **Precision Summary**
>
> **What this concept is:** The principle that collection type encodes an operation performance contract. `List` makes iteration O(n) and lookup O(n). `Map` makes keyed lookup O(1). `Set` makes membership testing O(1). `Comparator` is a named, external ordering rule that separates the sort criterion from the objects being sorted.
>
> **What it explains:** Why two correct programs can have radically different scalability. Why choosing `List` for everything is a performance risk, not a style choice. Why a sorting rule should be expressed as a named object rather than inline comparison logic.
>
> **What it does NOT mean:** It does not mean `List` is wrong. `List` is the right type when the primary operation is ordered iteration. It does not mean AI-generated comparators are unsafe — they are appropriate for mechanical expression of a rule the developer has already specified. It does not mean correctness and performance are the same property.
>
> **What comes next:** The sorted, filtered collection must be bound to a display component. When the collection changes, the display must update. That problem — separating the data model from the view and propagating changes between them — is the subject of the next module.
