# Module 1: Fundamentals of Programming in Java

*The program compiles. That is the beginning of the problem, not the end.*

---


## EDGE Course Outline Alignment

**Module 1: Fundamentals of Programming in Java**

### Learning Objectives (LOs)

- Understand computation and programming.
- Review fundamentals of programming in Java.
- Write Java programs with basic syntax, including variables, I/O, Strings, control flow, conditions, methods, arrays, and file I/O.

### Applied Industry Skills

- Applied Industry Skills

### Topics / Lessons / Material

- Variables
- Data Types
- Control flow and conditions
- if-else statements
- While loops
- For loops
- Comments
- Basic design principle
- Lab 1

Here is the situation. A library has books. Books get borrowed. Books come back. This is not a complicated idea — humans have managed it with index cards since before computers existed. But when you sit down to write the software, something happens. You find yourself asking: where does the borrowing live?

That question turns out to be the whole subject of this module.

Let me show you what I mean. Suppose you write the program the obvious way — the way almost everyone writes their first program. You have a list of books. You have a list of patrons. You have a procedure that takes a book and a patron and records the loan. The procedure runs. The output looks right. The program compiles cleanly and executes without throwing an error.

Then a patron returns a book. You write another procedure. Then a patron tries to borrow a book that's already out. You write a check. Then you need to know how many books a patron currently has. You write a query. By the time the library can do five things, you have fifteen procedures, and none of them live anywhere in particular. They are draped across the program like clothes on a chair.

Now a requirement changes. The library decides that a patron may not borrow more than three books at a time. Where do you make that change? The honest answer is: everywhere and nowhere. The rule doesn't live in one place because the patron doesn't live in one place. The patron is just a name in a list.

This is the problem that object-oriented programming was designed to solve. Not to make programs shorter. Not to make them run faster. To give things — real things, business things, things with identity and state and behavior — a place to live in the code.

---

## What An Object Actually Is

The word "object" sounds like jargon, so let me say what it means without using the word.

A patron of the library is a specific person. That person has a name. That person has a list of books they currently have checked out. And that person can do things: borrow a book, return a book, be asked how many they have. The name and the list are the person's *state* — information that belongs to this patron and no other. The borrowing and returning and counting are the person's *behavior* — things this patron can do.

Now here is the crucial point: the state and the behavior belong together. You cannot meaningfully ask "how many books does this patron have?" without also having access to the list of borrowed books. They are not separate facts that happen to be related. They are one thing. The patron is one thing.

An object is that idea made executable. A Java class is the template — the description of what a patron is and what a patron can do. A Java object is a specific patron created from that template. When you write `new Patron("Maria")`, you are not allocating memory (though you are doing that too). You are creating an entity with identity, with state that belongs to it, and with behavior that operates on that state.

This is why the procedure approach breaks down. Procedures operate on data that lives somewhere else. Objects carry their own data and provide the only legitimate door through which that data can be touched. You do not update a patron's borrowed-books list directly. You ask the patron to borrow a book, and the patron's own behavior handles the update. This boundary is not aesthetic preference. It is the mechanism by which a rule like "no more than three books" can live in exactly one place: inside the patron.

<!-- → [SCOPE | Figure 1 | IMAGE: procedural model vs. object model — two panels showing where behavior lives; left panel shows free-floating procedures acting on external data stores, right panel shows objects encapsulating their own state and behavior | CONTENT: left panel: three labeled procedure boxes (checkOut, returnBook, getBorrowedCount) pointing to a separate patron data store; right panel: single Patron object containing name field, borrowedBooks list, and borrow/return/count methods | EXCLUSIONS: compiler internals, memory allocation, UML class diagram syntax, inheritance, interfaces, access modifiers, garbage collector, JVM details] -->

*Figure 1.1 — Procedural vs. object model: where behavior lives*

---

## The Library Program, Looked At Carefully

Here is what the library checkout program actually contains. There is a `Book` class. A book knows its title. A book knows whether it is currently available. A book can be checked out, which makes it unavailable, and returned, which makes it available again.

There is a `Patron` class. A patron knows a name. A patron holds a list of the books currently borrowed. A patron can borrow a book (if the book is available and the patron has not hit the limit), and can return a book.

There is a `Library` class, or something that plays that role, which holds the collection of books and the collection of patrons and provides the operations the front desk would actually perform.

None of this is exotic. The structure follows directly from the business domain. A library has books. A library has patrons. Books get borrowed and returned. If you read this description and the code side by side, you should be able to point to the class for each noun and the method for each action.

Now I want to show you what happens when you change one line.

Suppose the checkout operation, instead of calling `book.checkOut()` on the specific book being borrowed, accidentally calls it on the wrong object — the patron, say, or a different book. The program still compiles. Java does not know that you meant to call it on the right book. Java only knows whether the call is syntactically legal, which it may well be. The program runs. Output appears. And the output is wrong in a way that can be subtle: the right patron is attached to the wrong book, or a book is marked unavailable without being in anyone's possession.

This is not a compilation error. This is a runtime error — a mismatch between what the code does and what the requirement says it should do. Compilation checks form. The requirement checks meaning. These are entirely different things, and the distance between them is where most real bugs live.

---

## Two Kinds of Wrong

Let me be precise about this distinction because it matters for the rest of the course.

A *compilation error* means Java rejected your code before running it. The code is grammatically illegal — a missing semicolon, a method called on a type that doesn't have that method, a variable used before it is declared. Java can detect these mechanically. They are analogous to a sentence that is grammatically incoherent: "The book borrowed patron the." You know immediately that something is wrong without having to understand what the sentence was supposed to mean.

A *runtime error* means Java accepted your code but something went wrong during execution. A `NullPointerException` is the classic example: you asked an object to do something, but the object turned out not to exist — you had a variable that held nothing, and then you called a method on the nothing. The code looked fine to Java at compile time. Only when it ran did the problem appear.

But there is a third kind of wrong that is more dangerous than either: the program runs, produces output, and the output is incorrect without signaling that it is incorrect. No exception. No red text. Just wrong answers. This is what happens when a patron ends up with the wrong book attached to their record. The program's behavior diverges from the requirement, quietly, and you will not know unless you look.

The discipline this course is teaching — reading code against a requirement, tracing behavior back to design intent, verifying that what runs is what was specified — exists entirely because this third kind of wrong is possible. If Java could detect all errors, verification would be automated. It cannot. The engineer's judgment is the only tool that works here.

<!-- → [SCOPE | Figure 2 | IMAGE: three-zone horizontal spectrum showing compilation error → runtime error → silent wrong behavior, ordered left to right by increasing danger and decreasing detectability; each zone names who or what catches it | CONTENT: zone 1 (compilation error): labeled Java compiler catches, example — missing semicolon; zone 2 (runtime error): labeled JVM catches at execution, example — NullPointerException; zone 3 (silent wrong behavior): labeled only engineer catches, example — wrong patron attached to wrong book | EXCLUSIONS: specific Java exception hierarchy, stack traces, debugger tools, IDE error panels, test frameworks, assert statements, logging] -->

*Figure 1.2 — Three kinds of wrong: detectability decreases left to right, danger increases*

---

## Where AI Fits Into This Picture

You will use AI tools in this course. This is not a course about avoiding AI. It is a course about understanding what AI can and cannot do, and holding the verification responsibility in the right place.

Here is what AI does well in this module: it explains. You can paste a Java method and ask what it does, and a good AI will walk you through it accurately. You can paste an error message and ask what caused it, and a good AI will identify the likely source. These are genuine capabilities. Use them.

Here is what AI cannot do: it cannot know your requirement. It does not know what the library checkout program is supposed to do in your version of the project. It knows what Java is and how it works. It does not know whether the patron object should hold a list of `Book` references or a list of book titles or a list of loan records. That is a design decision that connects to your specific requirement, and AI will guess — plausibly, confidently, and sometimes incorrectly.

The problem is not that AI guesses. Every good tool makes inferences. The problem is that AI's guesses look exactly like its correct answers. The output arrives with the same confidence, the same clean formatting, the same explanatory prose. If you cannot distinguish the correct answer from the plausible-but-wrong answer on your own, you cannot use AI safely. You are not using a tool. You are delegating judgment you have not yet developed.

This is the AI boundary for Module 1: AI may explain code and error messages you already have. AI may not write new Java code that you will submit.

The reason is not punitive. The reason is that the ability to write new code for this project requires understanding the requirement, which requires understanding the business domain, which is exactly what this module is teaching. If you skip that development by delegating the writing to AI, you have not learned the thing the module teaches. You have produced output. Those are different.

The verification responsibility stays with you. When AI explains something, you should be able to restate the explanation in your own words, without copying AI's phrasing. If you cannot, the explanation has not landed yet — which is information about what you still need to learn, not a problem to be solved by asking AI to explain it again differently.

| concept | Java artifact | what AI may do | what the student must verify | evidence before submission |
| --- | --- | --- | --- | --- |
| with | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. |

---

## Reading Code As A Business Model

The skill this module is actually building is not a Java skill. It is a reading skill.

Here is what I mean. When you look at the `Book` class, you are not only looking at a Java construct. You are looking at a claim about what a book *is* in the library's world. A book has a title. A book has an availability state. A book can transition between available and checked-out. These are business facts that someone decided were relevant, and the class is how those decisions were encoded.

When you look at the checkout method, you are looking at a business process. Who initiates it? The patron? The librarian? What are the preconditions — does the book need to be available? Does the patron need to be in good standing? What happens if a precondition fails? The method's signature and body answer these questions, or fail to answer them, and the failures are exactly where the bugs live.

Reading code this way — as a business model, not as syntax — is the foundation of everything that follows in this course. Every module adds a new capability to the semester project. Every capability is a business requirement translated into Java artifacts. Your job, each time, is to hold both in your head simultaneously: what the business needs, and whether the code actually provides it.

This is not a natural skill. It requires practice. The practice begins here, with a program you did not write, running in a domain you understand (library checkout), producing behavior you can predict. You change one line. You predict what changes in the output. You run it. You compare. Where your prediction was wrong, you have found the thing you do not yet understand.

That gap — between prediction and outcome — is where learning lives. AI cannot close it for you. AI can only make the gap invisible, which is not the same thing.

<!-- → [SCOPE | Figure 3 | IMAGE: three-question verification loop — triangular cycle connecting business behavior, Java artifact, and evidence of correctness; arrows show the direction of the verification process | CONTENT: node 1 — "What does this program do?" (business behavior); node 2 — "Which Java artifact is responsible?" (class/method/field); node 3 — "What would prove it's correct?" (evidence/test); directed arrows connecting all three in a cycle | EXCLUSIONS: specific test framework syntax, JUnit, assertion libraries, CI/CD pipeline, code coverage tools, UML, formal verification methods] -->

*Figure 1.3 — The verification loop: three questions, applied to every piece of running code*

---

## The Module's Single Capability

Every module in this course adds exactly one concrete capability to the semester project. This module's capability is: reading running code as a business model before writing new code.

That sounds abstract, so let me make it concrete.

By the end of this module, you should be able to take the library checkout program, read it carefully, and then answer three questions in writing:

First: what business behavior does this program implement? Not "it has a `Book` class and a `Patron` class," but: what can the library *do* with this software that it could not do without it?

Second: which specific Java artifact — which class, which method, which field — is responsible for each piece of that behavior? You should be able to point. Not gesture. Point.

Third: what would count as evidence that the behavior is correct? Not "it compiles" and not "it ran." What specific test or trace or output would demonstrate that the checkout operation actually connected the right patron to the right book?

When you can answer all three questions for the library version, you can answer them for inventory management and healthcare scheduling too — because the design shape is the same. The domain changes. The objects get new names. The business rules are different. But the relationship between requirement, Java artifact, and verification evidence follows the same logic.

That is the object model at work. Not as a definition to memorize. As a design principle you can apply.

| Item | Meaning |
| --- | --- |
| "What business behavior does this program implement?", "Which Java artifact is responsible?", "What evidence would prove correctness?" | A concrete checkpoint for applying the chapter concept. |
| intended as a reproducible worksheet, not decoration | A specific, evidence-linked version that readers can verify. |

---

## What You Are About To Build

The semester project is a real application in a domain you will choose. The library, the inventory system, the healthcare scheduler — these are three paths through the same curriculum. The concepts are identical. The Java is identical. The domain is different.

Each module adds one capability. This one adds the ability to read running code as a business model. The next module adds the ability to manage many objects of the same type — what happens when the library has not one book but five thousand. The module after that adds relationships between objects — what it means for a patron to *hold* a book, not just know about it.

By the end of the course, you will have built a working application with persistence, a user interface, and the ability to handle the kinds of failures that real business software encounters. Each piece will be yours. You will be able to explain it, debug it, and extend it — because you built it from the ground up, one module at a time, with AI as an explainer and yourself as the engineer.

That is the goal. This module is the foundation. The foundation is a question: what is the borrowing, and where does it live?

---

## Exercises

**Warm-up**

1. Open the library checkout program and locate the `checkOut()` method. Write one sentence describing what it does in business terms — not Java terms. Then write one sentence describing which object owns that method and why that ownership is not arbitrary. *(Tests: reading code as a business model; identifying which Java artifact carries a behavior.)*

2. The `Patron` class holds a list of borrowed books. What Java type would you expect that list to be? What would it mean — in business terms — if that field were `null` when a patron is first created versus empty? Write your answer before running or asking AI anything. Then check. *(Tests: distinguishing state from the absence of state; predicting behavior before observing it.)*

3. Classify each of the following as a compilation error, a runtime error, or silent wrong behavior. For each, write one sentence explaining how you would detect it: (a) calling `patron.checkOut(book)` when `Patron` has no method named `checkOut`; (b) calling `book.checkOut()` on a variable that holds `null`; (c) calling `book.checkOut()` on the correct object but recording the loan under the wrong patron. *(Tests: distinguishing the three kinds of wrong.)*

**Application**

4. Change one line in the checkout program so that a book is marked unavailable but not added to the patron's borrowed list. Predict the output before running. Run it. Where did your prediction match reality, and where did it diverge? Write a one-paragraph explanation of the divergence. Do not ask AI for help until after you have written the explanation. *(Tests: changing code, predicting effects, tracing silent wrong behavior back to its source.)*

5. Translate the library checkout model to your chosen domain (inventory or healthcare scheduling). Identify the three objects that correspond to `Book`, `Patron`, and `Library`. For each, name one piece of state and one behavior. Write this as a short prose paragraph, not a list. *(Tests: transferring the object model across domains; naming state and behavior in business terms.)*

6. Using the AI boundary defined in this module, write a prompt asking AI to explain an error message from the checkout program. Then write a second prompt that violates the boundary by asking AI to write new checkout code. Explain in one sentence why the second prompt falls outside the boundary — not that it violates a rule, but what understanding it would prevent you from developing. *(Tests: applying the AI boundary; articulating the reasoning behind it, not just the restriction.)*

**Synthesis**

7. A classmate argues: "If the program compiles and the output looks right on the first test, the implementation is correct." Write a two-paragraph response. The first paragraph should give a specific scenario from the library domain where this reasoning fails. The second paragraph should describe the minimum evidence you would need before accepting an implementation as correct. *(Tests: integrating the three-kinds-of-wrong framework with the verification standard; distinguishing "looks right" from "is correct.")*

8. The `Patron` class currently enforces the three-book limit inside the `borrow()` method. A teammate suggests moving that check to the `Library` class instead, so the library decides what patrons may do rather than patrons deciding for themselves. Write a short argument for each approach. Then state which you would choose and what the deciding factor is. *(Tests: evaluating design choices about where behavior lives; applying the object model as a design principle, not just a definition.)*

**Challenge**

9. The bridge question at the end of this module asks: what happens when the system needs many objects? Before reading the next module, write your best answer. What problems do you anticipate? What would the library software need to do differently if it held five thousand books instead of three? There is no correct answer yet — the point is to make your current understanding explicit so you can compare it to what Module 2 actually teaches. *(Points toward collections, iteration, and the design choices that come with managing many objects of the same type.)*

---

## Bridge

You can run one object. What happens when the system needs many?

---

## Key Terms

- **class** — the template that describes what an object is and what it can do; in the semester project, a class corresponds to a business entity with identity, state, and behavior.
- **object** — a specific instance created from a class; when you write `new Book("Dune")`, you have one object with its own state.
- **state** — the data an object holds about itself; a `Book`'s availability and title are its state.
- **behavior** — the operations an object can perform; a `Book`'s ability to be checked out and returned is its behavior.
- **compilation error** — a rejection by Java before the program runs; the code is syntactically illegal.
- **runtime error** — a failure during execution; the code was syntactically legal but something went wrong while it ran.
- **stdout** — standard output; the stream where `System.out.println()` writes; in this course, the first and most reliable window into what a running program is actually doing.

---

## Assessments

| Assessment | Type | Credit status | Group or Individual | Alignment note |
| --- | --- | --- | --- | --- |
| Optional Lab - Fundamentals of Programming | Practice | For-Credit | Individual | Practice basic syntax and control flow in a small Java program. |
| Optional Exercise: Java Program with Three Integers | Practice | For-Credit | Individual | Write and trace a simple input/process/output program. |
| Discussion - Reflection on Java Program with Three Integers (Graded) | Community | For-Credit | Individual | Explain what the program did and where mistakes appeared. |
| Optional Exercise: Program that asks User for Decimal Value | Practice | For-Credit | Individual | Practice input, data types, and numeric output. |
| Optional Exercise: do-while Loop | Practice | For-Credit | Individual | Practice loop structure and termination conditions. |

*Please label your assignments as Group or Individual.*


## Further Reading

- *Java Language Specification* and Java SE API documentation — use for language and library facts.
- Robins, Rountree, and Rountree, "Learning and Teaching Programming" — use for common novice difficulties and why some errors are harder to see than others.
- Peng et al. and Vaithilingam et al. — use for cautious, empirically grounded claims about AI coding assistance and the verification risks that attend it.

---

## CLI Quick Reference

```bash
java --version
javac --version
# Run from your project directory when checking environment and compiled output.
```

---

---
# CAJAL SCOPE OUTPUTS
*Run /scope on any of these to regenerate or refine. These are working briefs, not finished Illustrae-ready prompts — paste each figure description into /scope for the full three-block output.*

---

## Figure 1 — Procedural vs. object model [CRITICAL]

**ILLUSTRAE PASTE BLOCK**

Single-column figure, 89mm width, flat vector, white background. Two side-by-side panels separated by a vertical dividing line. Left panel labeled "Procedural model": three rectangular procedure boxes (checkOut, returnBook, getBorrowedCount) arranged vertically, each with an arrow pointing rightward to a single shared data rectangle labeled "Patron data." Arrows are standard single-headed activation arrows in Bluish Green #009E73. Right panel labeled "Object model": one large rounded rectangle representing a Patron object containing three internal regions — a name field, a borrowedBooks list, and a row of three method labels (borrow, return, count). No arrows exit the object boundary. Structural containers in Sky Blue #56B4E9 for the Patron object boundary; internal regions in light gray. Procedure boxes in Vermillion #D55E00. Dividing line in Black #000000 at 0.5pt. All strokes 1pt. Unannotated vector output — no text labels baked in.

**FULL SCOPE PROMPT**

[S - SPECIFICATION]
Single-column, 89mm width, vector output, white background, flat illustration style. No text labels in generated image — request unannotated output for manual annotation in Illustrae or Illustrator.

[C - CONTENT]
Left panel (procedural model): three procedure boxes (checkOut, returnBook, getBorrowedCount) arranged vertically, each with a rightward arrow to one shared patron data rectangle. Right panel (object model): one Patron object boundary enclosing name field, borrowedBooks list region, and three method labels. Vertical divider separating panels.

[O - ORGANIZATION]
Horizontal two-panel layout, panels equal width, separated by a 1pt vertical rule at center. Left panel flows top-to-bottom (procedures → data store). Right panel shows spatial containment (methods and state inside object boundary). No arrows cross the panel boundary.

[P - PRESENTATION]
Okabe-Ito palette. Procedure boxes: Vermillion #D55E00. Shared data store: light gray. Object boundary (Patron): Sky Blue #56B4E9. Internal regions within object: light gray. Activation arrows: Bluish Green #009E73, single-headed, 1pt stroke. Divider: Black #000000, 0.5pt. White background. No gradients, no drop shadows.

[E - EXCLUSIONS]
Compiler internals, memory allocation diagrams, UML class diagram notation, inheritance arrows, interface declarations, access modifiers (public/private), garbage collector, JVM internals, constructor syntax, any downstream classes (Book, Library), multiple patron instances, array notation.

**NEGATIVE PROMPT**

text labels, words, gibberish letters, titles, captions, decorative borders, realistic 3D textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, skeletal chemical structures, hand-drawn styles, sketch lines, human figures, colorful cell backgrounds, non-cellular debris, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion, UML notation, inheritance arrows, dashed access modifier lines, constructor brackets, array syntax, multiple instances, memory address labels

---

## Figure 2 — Three kinds of wrong [CRITICAL]

**ILLUSTRAE PASTE BLOCK**

Single-column figure, 89mm width, flat vector, white background. Horizontal three-zone spectrum, left to right: zone 1 (compilation error), zone 2 (runtime error), zone 3 (silent wrong behavior). Zones separated by vertical dividers. An upward-pointing danger arrow runs along the bottom of all three zones, increasing in stroke weight left to right to indicate increasing danger. A downward-pointing detectability arrow runs along the top, decreasing in stroke weight left to right to indicate decreasing detectability. Each zone contains one icon region: zone 1 a compiler-symbol shape in Sky Blue #56B4E9, zone 2 a crash/halt shape in Orange #E69F00, zone 3 a question-mark shape in Vermillion #D55E00. Small label region below each icon for manual annotation. White background, 1pt strokes, no gradients.

**FULL SCOPE PROMPT**

[S - SPECIFICATION]
Single-column, 89mm width, vector output, white background, flat illustration style. No text labels in generated image — unannotated for manual annotation.

[C - CONTENT]
Three equal-width horizontal zones separated by vertical 1pt dividers. Bottom: a single horizontal arrow spanning all three zones, increasing in visual weight left to right (thin at left, thick at right) — danger gradient. Top: a single horizontal arrow spanning all three zones, decreasing in visual weight left to right — detectability gradient. Zone 1 icon: compiler/halt symbol shape. Zone 2 icon: runtime crash/exception shape. Zone 3 icon: silent/question-mark shape indicating no visible signal. Each zone has a blank label region below its icon.

[O - ORGANIZATION]
Strict left-to-right horizontal layout. Zones equal width. Danger arrow below all zones, pointing right. Detectability arrow above all zones, pointing left (or showing decrease rightward). Icons vertically centered in each zone. Label regions at bottom of each zone.

[P - PRESENTATION]
Zone 1 icon: Sky Blue #56B4E9. Zone 2 icon: Orange #E69F00. Zone 3 icon: Vermillion #D55E00. Zone backgrounds: progressively darker light gray left to right (lightest in zone 1, medium in zone 2, slightly darker in zone 3). Danger arrow: Black #000000. Detectability arrow: Blue #0072B2. All strokes 1pt. White background. No gradients, no drop shadows.

[E - EXCLUSIONS]
Specific exception class names (NullPointerException etc.), stack trace formatting, IDE error panels, debugger UI, test framework syntax, assert statements, logging frameworks, code snippets, Java syntax of any kind, specific library checkout example code, patron/book variable names.

**NEGATIVE PROMPT**

text labels, words, gibberish letters, titles, captions, decorative borders, realistic 3D textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, skeletal chemical structures, hand-drawn styles, sketch lines, human figures, colorful cell backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion, code text, IDE interface elements, terminal windows, stack traces

---

## Figure 3 — The verification loop [IMPORTANT]

**ILLUSTRAE PASTE BLOCK**

Single-column figure, 89mm width, flat vector, white background. Three rounded rectangular nodes arranged in a triangle (top center, bottom left, bottom right). Directed arrows connecting all three nodes in a clockwise cycle. Top node represents business behavior question. Bottom-left node represents Java artifact identification. Bottom-right node represents evidence of correctness. Each node has a distinct icon region above a blank label area for manual annotation. Arrows in Bluish Green #009E73, 1pt stroke, single-headed. Node fills: top node in Orange #E69F00 (lightest shade), bottom-left in Sky Blue #56B4E9 (lightest shade), bottom-right in Bluish Green #009E73 (lightest shade). White background, no gradients, no drop shadows.

**FULL SCOPE PROMPT**

[S - SPECIFICATION]
Single-column, 89mm width, vector output, white background, flat illustration style. No text labels in generated image — unannotated for manual annotation.

[C - CONTENT]
Three rounded rectangular nodes in triangular arrangement: top-center (business behavior), bottom-left (Java artifact), bottom-right (evidence/correctness). Three directed arrows forming a closed clockwise cycle: top → bottom-right → bottom-left → top. Each node has a blank label region. Small icon region within each node: top node — document/requirement icon shape; bottom-left — code bracket icon shape; bottom-right — checkmark/verification icon shape.

[O - ORGANIZATION]
Equilateral triangle layout, top node centered horizontally, bottom two nodes symmetrically placed. Arrows hug the outside of the triangle (not crossing center). Clockwise direction. Equal spacing between nodes. Generous internal padding within each node.

[P - PRESENTATION]
Top node fill: Orange #E69F00 at 15% opacity. Bottom-left node fill: Sky Blue #56B4E9 at 15% opacity. Bottom-right node fill: Bluish Green #009E73 at 15% opacity. Node strokes: matching color at full opacity, 1pt. Arrows: Bluish Green #009E73, 1pt, single-headed. White background. No gradients, no drop shadows.

[E - EXCLUSIONS]
Specific test framework syntax, JUnit annotations, assertion library names, CI/CD pipeline elements, code coverage percentages, UML notation, formal verification symbols, specific library checkout variable names, patron/book class names, any Java syntax, multiple verification loops, sub-questions within nodes.

**NEGATIVE PROMPT**

text labels, words, gibberish letters, titles, captions, decorative borders, realistic 3D textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, skeletal chemical structures, hand-drawn styles, sketch lines, human figures, colorful cell backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion, code syntax, terminal output, test runner UI, UML class notation
