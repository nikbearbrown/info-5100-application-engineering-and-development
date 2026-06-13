# Module 14 — Final Project: Professional Handoff and Design Defense
## Exercise Set

**Learning Objectives**
1. Document and defend design decisions with explicit trade-off reasoning
2. Conduct three-question AI audits on AI-assisted components
3. Explain the five-layer architecture and assign components correctly
4. Reflect honestly on design decisions with specific counterfactuals

**Core Concepts:** five-layer architecture (supply / transaction / persistence / view / event), professional handoff (running code / source / tests / AI disclosures / design defense), three-question AI audit, strong vs. weak defense structure, code review vocabulary, verification habit

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1.** (Tests: recall — five-layer architecture)
Name the five layers of the architecture from this chapter. For each, write one sentence describing its responsibility. Use the library checkout system as your domain — every sentence should name a concrete example from that system.

**Exercise 2.** (Tests: true/false — AI disclosure sufficiency)
True or False — then explain your answer in 2–3 sentences:

> "Saying 'I used an AI to help write this class' is sufficient AI disclosure for a professional handoff."

**Exercise 3.** (Tests: vocabulary — three-question AI audit)
What are the three questions in the AI audit? Write each question as a sentence. Then explain in 2–3 sentences why "What did you verify?" is the most important of the three.

**Exercise 4.** (Tests: vocabulary — weak vs. strong design defense)
What is the difference between a weak defense and a strong defense? Give a concrete example of a weak answer and a strong answer to the question: *"Why did you use a `HashMap` for your catalog?"*

**Exercise 5.** (Tests: true/false — definition of project completion)
True or False — then explain your answer in 2–3 sentences:

> "A project is complete when the code runs and produces correct output."

---

## Tier 2 — Application

*(Tests: layer assignment, AI audit, design defense, AI interaction, reflection)*

**Exercise 6.** (Tests: five-layer assignment — library system components)
A library system has these components: `Book` entities, `Checkout` transaction records, CSV save/load methods, a `TableView` display for the book list, and button click handlers.

Assign each component to the correct layer. For each assignment, explain in one sentence why it belongs there — not just what the layer is named.

**Exercise 7.** (Tests: AI audit — concrete verification evidence)
A student used an AI to write the `BookRepository.saveToFile()` method. Write a complete three-question AI audit for this component:

- (a) What did you ask the AI?
- (b) What did you verify about the AI's output? (Specify the concrete verification evidence — not "I tested it" but: what test, with what inputs, producing what specific output?)
- (c) What design decisions did you make that the AI could not make for you?

Write this as a student would write it for a professional handoff document. Be specific.

**Exercise 8.** (Tests: design defense — structured, trade-off reasoning)
You chose to store your appointment catalog in a `HashMap<String, Appointment>` keyed by appointment ID. Write a strong defense:

- (a) What alternatives did you consider and reject?
- (b) What are the costs and gains of using a `HashMap`?
- (c) What specific requirement drove this choice?
- (d) What would change your decision if requirements changed?

Your defense should be 150–200 words and follow the structure from Exercise 4.

**Exercise 9.** (Tests: AI interaction — AI approval is not a human defense)
A student preparing their final defense asks an AI: *"Review my code and tell me if my design is good."* The AI responds with a detailed review praising the architecture and suggesting two minor improvements. The student uses this as their defense: *"My AI reviewed my code and said it's well-designed."*

- Identify what the student has and has not established.
- Write a one-paragraph explanation (4–6 sentences) of why AI approval is not a substitute for a human design defense.

**Exercise 10.** (Tests: reflection — weak vs. strong, explicit counterfactual)
Answer this reflection question as a student who has completed a library checkout system: *"What is one design decision you would change if you were starting over, and why?"*

Write both:
- A **weak answer** (2 sentences)
- A **strong answer** (4–6 sentences)

Then write one sentence explaining what makes the strong answer strong.

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration, named prior chapters explicitly)*

**Exercise 11.** (Tests: synthesis — Ch 14 + Ch 13, tests in a professional handoff)
In Ch 13, you learned that tests provide limited proof — they verify specific behaviors under specific inputs. In Ch 14, tests are one required component of a professional handoff.

Explain:
- (a) What role do tests play in a professional handoff beyond "proving correctness"?
- (b) What does a regression test from Ch 13 demonstrate to a reviewer that a coverage-count test (e.g., "I wrote 20 tests") does not?
- (c) Write one sentence describing a test that would be more compelling in a handoff than "Test 14: returns the correct book."

A surface answer says "tests show the code works." A strong answer frames tests as documentation of intent and design decisions, uses regression vocabulary from Ch 13 correctly, and writes a test description tied to a specific requirement or known failure mode.

**Exercise 12.** (Tests: synthesis — Ch 14 + Ch 6, LoginManager defense using threat-model reasoning)
In Ch 6, you designed a `LoginManager` using threat-model reasoning — identifying what an attacker could exploit and what your design prevents. In Ch 14, a strong defense requires stating alternatives and trade-offs explicitly.

Write a strong defense of your `LoginManager` design:
- (a) Name two alternative approaches you considered (e.g., plaintext passwords, session tokens, OAuth delegation)
- (b) State the security trade-off of each alternative — what it protects against and what it leaves exposed
- (c) Explain what specific requirement drove your final choice
- (d) State what new requirement would cause you to reconsider your current design

A surface answer describes the LoginManager. A strong answer names real security alternatives, applies threat-model vocabulary from Ch 6, connects the final choice to a stated requirement, and frames the design as a reasoned decision under constraints — not the only correct answer.

---

## Tier 4 — Challenge

*(No answer key. Rubric only. Open-ended architectural analysis.)*

**Exercise 13.** (Tests: architecture adaptation — five-layer model in a new domain)
The five-layer architecture (supply, transaction, persistence, view, event) was designed for a library checkout application. Consider adapting it to a fundamentally different domain: a real-time multiplayer word game where players submit words, the system validates them against a dictionary, and scores are updated live for all players.

Identify:
- (a) Which layers map directly from the library system to the word game, and why
- (b) Which layers require significant redesign, and what specifically changes
- (c) What new layer or architectural concern the five-layer model does not address in this domain
- (d) What the most difficult single architectural decision would be and why

There is no single correct answer — the quality of reasoning matters more than the conclusion.

**Rubric — what distinguishes a strong response:**
- Specifically maps or rejects each of the five layers with a reason (not just "it applies" or "it doesn't")
- Identifies a genuine architectural gap that the five layers do not address — not just a renamed layer
- Names the hardest decision and explains *what makes it hard* (competing constraints, unknown requirements, technical limitation)
- Demonstrates awareness that architecture serves requirements, not the other way around — the library architecture was not universally optimal; it was optimal for those requirements

---

## Full Answer Key — Tiers 1–3

### Exercise 1
Five layers with library examples:

1. **Supply layer** — holds the domain entities that exist independently of transactions. Example: `Book` objects in a `BookCatalog`.
2. **Transaction layer** — records events that change system state. Example: `CheckoutRecord` objects that track which patron has which book and when.
3. **Persistence layer** — saves and loads state to durable storage. Example: `CatalogRepository.saveToCSV()` and `loadFromCSV()`.
4. **View layer** — displays data to the user. Example: the `TableView<Book>` screen showing available books.
5. **Event layer** — responds to user actions and delegates to other layers. Example: the checkout button handler that calls `model.checkout()` and then updates the view.

### Exercise 2
**False.** "I used an AI" is a disclosure of tool use, not an audit. A professional handoff requires the reviewer to understand: what the AI was asked, what the AI produced, what was verified, and what design decisions the developer made independently. Without this detail, the reviewer cannot assess whether the AI-generated code is trustworthy, whether it fits the system's constraints, or whether the developer understands how it works.

### Exercise 3
The three questions:
1. What did you ask the AI?
2. What did you verify about the AI's output?
3. What design decisions did you make that the AI could not make for you?

"What did you verify?" is the most important because AI-generated code can be plausible-looking and still be wrong for the specific context, non-idiomatic, or fragile under edge cases. Verification is the point where the developer takes ownership. Without verification evidence, the AI audit is not a quality check — it is just a log of prompts.

### Exercise 4
**Weak defense:** "I used a `HashMap` because it's fast."

**Strong defense:** "I considered an `ArrayList` and a `TreeMap`. An `ArrayList` gives O(n) ISBN lookup, which becomes slow as the catalog grows. A `TreeMap` gives O(log n) lookup and maintains sorted order, which I didn't need — my sorted display is generated separately. I chose `HashMap` because my dominant operation is ISBN lookup (called on every checkout and return), and O(1) average-case lookup fits that profile. If I needed sorted iteration as a primary operation, I would switch to a `TreeMap` or maintain a parallel sorted list."

The weak answer names a benefit without comparing alternatives or tying it to a requirement. The strong answer names what was considered, what was rejected and why, what requirement drove the decision, and what would change it.

### Exercise 5
**False.** A project is not complete when code runs correctly — that describes functional completion, not professional completion. Professional completion includes: documented design decisions so a successor can maintain and extend the code, tests that demonstrate the known behaviors and provide regression safety, and disclosure of AI contributions so reviewers can assess which parts were independently reasoned. Running correctly is the floor, not the ceiling.

### Exercise 6
| Component | Layer | Reason |
|---|---|---|
| `Book` entities | Supply | Books exist independently of any transaction; they are supply-side entities |
| `Checkout` transaction records | Transaction | Checkouts represent events that change state; they are the record of what happened |
| CSV save/load methods | Persistence | Their entire purpose is durable storage — they have no behavior other than reading and writing |
| `TableView` display | View | TableView renders data for the user; it has no business logic |
| Button click handlers | Event | Handlers respond to user actions and delegate to other layers — that is the event layer's purpose |

### Exercise 7
Sample complete AI audit for `BookRepository.saveToFile()`:

**(a) What I asked the AI:**
"Write a Java method that saves a list of Book objects to a CSV file, where each Book has isbn, title, and author fields. The file should overwrite the existing file if it exists."

**(b) What I verified:**
I ran the method with a catalog of three books (`isbn: 978-0451524935, title: 1984, author: Orwell`; `isbn: 978-0743273565, title: The Great Gatsby, author: Fitzgerald`; `isbn: 978-0061120084, title: To Kill a Mockingbird, author: Lee`). I then opened the output file `catalog.csv` and confirmed all three rows were present with correct field order and comma separation. I also ran my `loadFromCSV()` method on the saved file and verified the round-trip preserved all three ISBNs, titles, and authors. I tested saving an empty catalog and confirmed the output file was created with zero data rows (not missing the file entirely).

**(c) Design decisions I made that the AI could not make:**
The AI did not know that our CSV format requires a header row (`isbn,title,author`) for compatibility with the load method. I added the header. The AI also did not know that our file path is relative to the project root rather than a user-specified path — I hardcoded the path after the AI generated a parameter. Finally, the AI used `PrintWriter` with default encoding; I changed it to explicitly use UTF-8 because some book titles contain non-ASCII characters.

### Exercise 8
Sample strong defense:

I considered three alternatives for storing appointments: an `ArrayList<Appointment>`, a `TreeMap<String, Appointment>`, and a `LinkedHashMap<String, Appointment>`.

An `ArrayList` requires iterating the entire list for every lookup by appointment ID, giving O(n) performance that degrades as appointments accumulate. A `TreeMap` provides O(log n) lookup and maintains alphabetical key order, but my application does not require appointments to be sorted by ID — I sort by date for display separately. A `LinkedHashMap` preserves insertion order, which would be useful if the display order needed to match entry order, but that was not a requirement.

I chose `HashMap<String, Appointment>` because the dominant operations are lookup by appointment ID (on every booking, cancellation, and modification) and containment checks. These are O(1) average-case with a `HashMap`. The cost is no guaranteed iteration order, which I address with a separate sorted list in the view layer.

If a requirement emerged to always display appointments in ID order without a separate sort step, I would switch to `TreeMap`.

### Exercise 9
**What the student has established:** That an AI, when asked to evaluate the code's quality, produced a positive evaluation. That is all.

**What the student has not established:** Whether the AI's assessment is accurate for this specific system and its requirements. Whether the student understands the design. Whether the design handles the domain's edge cases correctly. Whether the AI had access to the requirements, test results, or context that a human reviewer would need.

**Why AI approval does not substitute for a human defense:** A design defense is not a quality certification — it is a demonstration that the designer understands the decisions they made, the trade-offs they accepted, and the assumptions the design depends on. An AI cannot know which design decisions were genuinely hard choices under constraints and which were defaults. A human reviewer asking "why did you choose a HashMap?" is asking the designer to demonstrate that understanding — an AI's praise cannot substitute for that demonstration. Furthermore, an AI asked "is this good?" has an optimistic response bias; it does not know what "good" means in the context of this instructor's rubric, this team's constraints, or this application's requirements.

### Exercise 10
**Weak answer:**
I would change how I stored my books. I picked the wrong data structure and it caused problems.

**Strong answer:**
I stored books in an `ArrayList<Book>` because it was the first data structure I learned and I did not think about lookup performance until my catalog had 200 books and searches became slow. If I were starting over, I would store books in a `HashMap<String, Book>` keyed by ISBN from the beginning, because ISBN lookup is the operation that every other feature — checkout, return, search — depends on. The cost of switching mid-project was refactoring eight methods that used list index operations. The lesson is that the choice of primary data structure for a domain entity shapes the entire codebase — that decision deserves more analysis upfront than I gave it.

**What makes the strong answer strong:** It names the specific decision, the specific consequence, the specific alternative, and the specific lesson — with enough detail that a reader learns something. The weak answer names a regret without explaining it.

### Exercise 11
(a) Tests in a professional handoff serve as documentation of intent: they show what behaviors were considered important enough to verify explicitly. This tells a future maintainer what the original developer expected the system to do — not just what it currently does. Tests also function as a safety net for future changes, communicating "this worked before your change; if it breaks now, you introduced a regression."

(b) A regression test from Ch 13 demonstrates that a specific bug was found, understood, and fixed — and that the system is now protected against that failure recurring. A coverage count ("I wrote 20 tests") only shows quantity. A reviewer cannot tell from the count whether the tests cover the cases that actually fail in production, or whether they all test the same happy path 20 times.

(c) "Verifies that a patron who has already been suspended cannot check out a new book — this test was written after a live bug where suspended patrons were not blocked during concurrent checkouts."

### Exercise 12
Sample strong LoginManager defense:

(a) Two alternatives considered:
- **Plaintext password comparison:** Store passwords as strings, compare directly on login.
- **Delegated authentication (OAuth-style):** Redirect login to an external identity provider; store only a user token.

(b) Security trade-offs:
- **Plaintext:** Simple to implement. Exposed to every threat in the model: if the storage file is read by an attacker, all passwords are compromised immediately. Provides no protection for users who reuse passwords across systems.
- **OAuth delegation:** Eliminates password storage risk entirely. Requires a network connection and an external service — not feasible for a standalone desktop application with no internet requirement. Also adds dependency risk: if the identity provider is unavailable, no one can log in.

(c) What drove the final choice: The system is a standalone desktop application with no network requirement. The threat model (Ch 6) identified the primary risk as file-level access to the credential store. I implemented hashed passwords (SHA-256 with a per-user salt) to address that specific threat without requiring network infrastructure.

(d) What would change the decision: If the system were deployed as a web application with multiple users logging in from different machines, the threat model changes significantly — session fixation, token theft, and credential stuffing become relevant. At that point, delegating to an established identity provider would be the correct choice regardless of implementation complexity.

---

## Instructor Notes

**Common student errors in this module:**

1. **Weak defenses:** The most common error is answering "Why did you use X?" with "Because it's fast" or "Because I learned it in class." The corrective practice: require students to name at least one alternative they did not choose and explain why. A defense that does not address alternatives is not a defense — it is a description.

2. **AI audit without verification evidence:** Students write "I tested it" in the audit but cannot specify what test, with what inputs, and what the output was. Exercise 7 targets this specifically. The framing: if you cannot describe your verification specifically, you did not verify — you assumed.

3. **Conflating "AI approved" with "reviewed":** Exercise 9 targets the increasingly common pattern of using AI praise as a defense. The corrective: an AI does not know the requirements, the constraints, or the rubric. Its praise is not evidence of quality relative to any of those.

**Sequencing recommendation:** Run Exercise 10 (reflection) before students submit their projects — as a pre-submission reflection. Students who answer it honestly often identify an improvement they can still make. Students who give a weak answer in the exercise tend to give weak defenses in the presentation.

**Tier 3 notes:** Exercise 11 requires Ch 13 regression vocabulary. Students who did not internalize "regression test = protection against known failure recurring" will say "tests prove correctness" — which Exercise 11 explicitly asks them to move past. Exercise 12 requires Ch 6 threat-model vocabulary. Students who completed Ch 6 with shallow threat models will struggle to name real security trade-offs here. If Ch 6 was not completed, substitute: "Design a defense for your choice of whether to store patron data in memory or in a file."

**Tier 4 note:** The strongest responses to Exercise 13 will identify concurrency as the genuine architectural gap — the five-layer model was designed for single-user sequential interactions. Real-time multiplayer introduces simultaneous state changes, which the event layer was not designed to handle. Accept any well-reasoned gap (real-time communication protocol, state synchronization, server-side authority model) as long as it is distinct from the five layers and explained with specificity. Reject "it needs a database layer" without further justification — persistence is already one of the five layers.
