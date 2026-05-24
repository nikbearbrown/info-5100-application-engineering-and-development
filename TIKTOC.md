# TIKTOC.md — Full TOC Draft
## Programming with Java: An Object-Oriented Practicum
### Irreducibly Human Series · Northeastern University College of Engineering

**Author:** Nik Bear Brown · ni.brown@neu.edu · Bear Brown & Company
**Series:** Irreducibly Human: What AI Can and Can't Do
**Companion course:** INFO 5100 / EDGE (Coursera)
**Book type:** Course textbook (Kindle) — chapter = module, read in sequence
**Version:** 1.0 — Pre-proposal draft
**Status:** Research-ready

---

## Document Structure

1. Book Concept and Thesis
2. Learner Profile
3. Book Type and Deployment Specification
4. Field Positioning
5. Three-Act Learning Arc
6. Prerequisite Map
7. Assessment Structure
8. Chapter-by-Chapter TOC (15 modules including Module 0)
9. Chapter Anatomy Template
10. Case Study Strategy
11. Hard Topics, Contested Claims, Aging Risk
12. Market Positioning
13. Feature List
14. Out of Scope
15. Adoption Risk Register
16. Open Questions

---

# PART 1 — BOOK CONCEPT AND THESIS

## Book concept summary

> This book teaches **object-oriented software engineering — from
> first principles through GUI-based application design — to graduate
> engineers entering their first programming-intensive course**, by
> **building one business problem incrementally across all 14 modules
> while teaching, at the end of every module, exactly which parts of
> that problem to hand to an AI and exactly which parts require the
> engineer's own understanding, judgment, and verification**. It fills
> the gap left by language-reference textbooks (which teach syntax, not
> engineering) and generic AI-coding tutorials (which teach prompting,
> not debugging). It succeeds if the reader can **design, implement,
> and defend a complete OO application — and explain, for every AI-
> assisted step, what they verified and why they could not have
> delegated that verification**.

**One-sentence logline:**
A Java practicum that teaches object-oriented engineering and AI
collaboration simultaneously — because you can't verify code you
don't understand, and you can't understand code you never had to write.

## Central thesis

"This book argues that the productive use of AI in software development
requires genuine object-oriented understanding — not as a prerequisite
to learning AI tools, but as the very thing that makes AI assistance
safe to accept — which means that engineers who use AI without performing
the identification, design, and verification layers are producing
applications they cannot debug, and this matters because every production
defect in an AI-assisted codebase traces back to a delegation the
engineer made before they understood what they were delegating."

## Thesis test

The TOC reflects the thesis at every act:

- ACT ONE: The student writes Java by hand — syntax, structure, objects —
  before any AI tool is introduced. The identification layer (what does
  this code do?) is experienced before it is named. ✓
- ACT TWO: The student learns to read and design the OO structures that
  AI generates — inheritance, polymorphism, collections, event handling.
  AI is introduced progressively, always with a verification gate. ✓
- ACT THREE: The student builds a full GUI application with AI assistance,
  but the design decisions, the debugging judgment, and the final defense
  are irreducibly theirs. ✓

**Thesis test: PASS**

---

# PART 2 — LEARNER PROFILE

## Primary reader

A first-semester graduate student in an applied engineering or information
systems program — most likely coming from a non-CS undergraduate background
(biology, business, mechanical engineering, communications) — who has seen
some code but has never engineered a complete application. They have just
been handed a Java IDE and a problem statement and are trying to understand
what to do first.

**Specific person:** A first-year MS Information Systems student who
minored in statistics as an undergrad, has written Python scripts for
data analysis, and now needs to build a full business application in Java
as part of a course requirement. They tried using Claude to write the
code, got something that compiled, could not explain why it worked, and
are now stuck on the first modification the instructor asked for.

## Prior knowledge assumed

- Basic programming concepts (variables, loops, conditionals) in any language
- Some exposure to Python or R for data work
- Comfort with the command line at the level of navigating directories
- No prior Java required

## Prior knowledge NOT assumed

- Object-oriented design
- Java syntax
- IDE use beyond running pre-written scripts
- Debugging methodology
- Any prior use of AI coding assistants in a disciplined way

## Prior misconceptions

1. "If it compiles, it works" — compilation checks syntax; it does not
   check whether the program does what the requirements say
2. "AI writes better code than I would anyway" — AI writes code that
   looks correct; whether it behaves correctly under the actual
   requirements is a question only the engineer can answer
3. "Object-oriented design is a Java thing" — OO is a modeling discipline;
   Java is one language that enforces it
4. "Debugging means reading error messages" — error messages identify
   a symptom; debugging is diagnosing the cause

## Motivation type

Mixed: academic (course requirement, primary), professional (job need —
they will be expected to write and review code at work), and intellectual
(the student who chose engineering wants to build things). The course
requirement is primary for most students. The design: every module's
final project deliverable is a running, testable piece of their
semester-long business application — not a textbook exercise.

## Prerequisite map

| Prerequisite | Safe to assume? | If not: where addressed |
|---|---|---|
| Variables, loops, conditionals (any language) | Yes | — |
| Command-line navigation | Probably | Module 0 setup appendix |
| Java syntax | No | Modules 1–2 (primary instruction) |
| OO concepts | No | Modules 2–5 (primary instruction) |
| IDE installation (NetBeans) | No | Module 0 setup appendix |
| Debugging methodology | No | Module 4 (primary instruction) |
| AI tool use (any) | Probably | Module 1 frames it from scratch |

**Front-loading decision:** Java syntax and OO concepts are the two
prerequisites rated "No" that are not excluded. Both are addressed
as primary instruction beginning in Module 1 and Module 2 respectively.
IDE installation is handled in a pre-course setup appendix (Module 0)
with step-by-step screenshots. No assumed prior knowledge of Java
is required to begin Module 1.

---

# PART 3 — BOOK TYPE AND DEPLOYMENT SPECIFICATION

## Book type

**PRIMARY TYPE:** Course textbook (Kindle) — adopted for a 15-week
semester, module = week, read in sequence. Companion to INFO 5100 /
EDGE (Coursera). Chapter count: 15 course modules, Module 0 through Module 14.

**NOT:** Practitioner handbook (chapters are not self-contained tasks),
reference work (the out-of-scope section is too aggressive for a
reference), language specification (syntax coverage is selective,
not comprehensive).

## Deployment specification

**Primary adoption context:**
INFO 5100 / EDGE (Coursera) — Application Engineering and Development.
Graduate-level. One module per week. 15-week semester. College of
Engineering, Information Systems program.

**Secondary adoption context:**
Other first-programming courses in professional MS programs (business
analytics, data science, health informatics) that require application
development exposure. Professional development programs for analysts
who need to learn to build tools, not just use them.

**What the book is NOT designed for:**
CS undergraduate programs (too applied, not theoretical enough);
advanced Java courses (prerequisites too low); bootcamp-style programs
(depth per module is too high for a compressed timeline); stand-alone
reference use (sequence dependency is too high).

**How the TOC signals book type to a faculty reviewer:**
15 modules, Module 0 through Module 14, with a single business problem threaded from
Module 1 through Module 14. Three explicit act transitions. A final
project specified in Module 14 that requires a running GUI application.
A faculty member building a 15-week syllabus can map this TOC in under
ten minutes.

---

# PART 4 — FIELD POSITIONING

## The positioning statement — consolidated

The competitive landscape has a clean gap:

- Liang (*Introduction to Java Programming*) is comprehensive but
  author-centered — 1,400 pages, covers everything, teaches the
  field's structure, not the learner's build.
- Horstmann (*Core Java*) is the professional reference; it assumes
  the reader already programs.
- Generic "Java for beginners" Kindle books lack pedagogical
  architecture — they are syntax tours without OO design thinking.
- YouTube/Udemy tutorials are fragmented — no arc, no assessment,
  no single problem threading the curriculum.
- AI coding tutorials (GitHub Copilot docs, "Learn to Code with
  ChatGPT") teach prompting, not verification.

**The gap this book fills:** No course textbook teaches Java OO
engineering *and* the AI collaboration discipline *simultaneously*,
threading one business problem through every module, with explicit
phase gates at the boundary between what the AI handles and what
the student must own.

## Positioning statements by competitor

**vs. Liang, *Introduction to Java Programming*:**
"Unlike Liang, which provides comprehensive coverage of Java for
a CS-track student reading 1,400 pages, this book teaches graduate
engineers to design and build a complete OO application in 14 focused
modules — privileging depth of understanding over breadth of coverage,
and integrating AI collaboration discipline into every module."

**vs. generic "Java for beginners" Kindle books:**
"Unlike syntax-tour Java books, which teach students to write code
without teaching them to design systems, this book uses backward
design from a working application: every module's content is chosen
because the student needs it to build the next layer of their
semester project."

**vs. AI coding tutorials:**
"Unlike tutorials that teach students to prompt AI for code, this
book teaches students why they cannot safely accept AI-generated code
they do not understand — and provides the OO foundation that makes AI
assistance safe, verifiable, and productive."

---

# PART 5 — THREE-ACT LEARNING ARC

## The arc statement

This book takes the reader from **someone who has seen code but never
engineered a system** to **an engineer who can design, build, debug,
and defend a complete object-oriented GUI application — and who can
articulate, for every AI-assisted step, what required their own
judgment** by first establishing the foundational mechanics of Java
objects and classes (Act One), then building the OO design toolkit
— inheritance, polymorphism, collections, event handling — through
progressive layers of their semester project (Act Two), then applying
the full toolkit to a complete GUI business application with
disciplined AI collaboration throughout (Act Three).

## The pebble-in-the-pond opening

Module 1 gives the student a working Java program to run before they
write a single line. They modify it. It breaks. They encounter their
first compilation error and their first runtime error before the
vocabulary for either is introduced. Act One establishes what objects
are and why they are the right model for business problems. The
semester project is introduced in Module 1 as the single problem they
will solve across all 14 modules.

## Act One — Establish (Modules 1–4)

**Starting state:** The student can run a Java program someone else
wrote.
**Ending state:** The student can design a class, instantiate objects,
and trace what happens in memory when they do — and can explain which
of those steps an AI assistant can help with and which it cannot.
**Inciting question:** "My object has the right fields but the wrong
behavior. How do I figure out what's wrong?"
**Act One → Act Two transition:** The student can read a Java class
definition, explain what every component does, and write a test that
fails before they fix the bug.

## Act Two — Build (Modules 5–10)

**Starting state:** The student can design single classes but cannot
model relationships between them.
**Ending state:** The student can design a multi-class OO system,
implement it with inheritance and polymorphism, and manage collections
of objects — with AI assistance at the implementation layer and
human judgment at the design and verification layers.
**Hardest conceptual moment:** Module 7 (Polymorphism) — method
dispatch inverts the student's expectation about which method runs.
**Act Two → Act Three transition:** The student has a working
data model and business logic layer; they are ready to connect it
to a user interface.

## Act Three — Apply (Modules 11–14)

**Starting state:** The student has a working back end but no UI.
**Ending state:** The student has a running GUI application that
addresses the semester project's requirements, built with disciplined
AI assistance, debugged by the student, and defended in a final
presentation.
**The transfer test:** The final project requires the student to
add a feature the course never explicitly covered — applying the
OO principles to a novel extension of their own system.

## The CLAUDE.md across the arc

Every module includes a "Setting Up Your CLAUDE.md" section that
constrains how the student interacts with AI for that module's work.
The constraints escalate:

| Act | CLAUDE.md constraint level | What the student constrains |
|---|---|---|
| Act One (M1–4) | Diagnostic only | AI can explain code; cannot write it |
| Early Act Two (M5–7) | Scaffold only | AI can generate method stubs; student fills bodies |
| Late Act Two (M8–10) | Implementation assist | AI can implement to spec; student writes the spec |
| Act Three (M11–14) | Full collaboration | AI can propose; student designs, reviews, and owns |

The CLAUDE.md appendix ("How to Use Claude for Java") documents the
complete constraint system and explains why each constraint exists.

---

# PART 6 — PREREQUISITE MAP

## The business application thread

Every module builds on a single business problem introduced in Module 1.
Students choose from three domain options at the start of the course:
(A) a library management system, (B) a small business inventory tracker,
or (C) a simple healthcare appointment scheduler. All three thread
through the same OO design challenges at the same point in the arc.
Examples in the text use domain (A); exercises include (B) and (C)
variants.

## Prerequisite chain

| Module | Prerequisite capabilities | Load-bearing? |
|---|---|---|
| M1 | Basic programming concepts (any language) | — |
| M2 | M1: Java syntax basics, class/object concepts | Yes |
| M3 | M2: Object instantiation, method calls | Yes |
| M4 | M3: Multi-object programs, parameter passing | Yes |
| M5 | M4: Full debugging workflow | Yes |
| M6 | M5: Supply-side modeling, person/user modeling | Yes |
| M7 | M6: Inheritance basics | Yes |
| M8 | M7: Polymorphism | Yes |
| M9 | M8: Collections (List, Map) | Yes |
| M10 | M9: GUI basics (JavaFX) | No — standalone |
| M11 | M10: Event handling | Yes |
| M12 | M11: Full GUI application | Yes |
| M13 | M12: Collections + GUI integration | Yes |
| M14 | M1–M13: Everything | Yes — synthesis |

**The student who skips chapters test:** Every module from M2 onward
is load-bearing. Missing Module 4 (debugging) makes Module 5 onward
nearly impossible in practice. The Kindle format displays prerequisite
callouts at the start of each module.

---

# PART 7 — ASSESSMENT STRUCTURE

| Component | Weight | Modules |
|---|---|---|
| Weekly Lab Assignments (one per module) | 20% | M1–M14 |
| Weekly Quizzes (M2–M13) | 20% | M2–M13 |
| Spot Attendance/Participation | 10% | Throughout |
| Final Project (complete GUI application) | 50% | M14 (built across M1–M14) |

**AI Use Disclosure (every lab assignment):**
Each lab submission requires a one-paragraph AI Use Disclosure naming:
- Which parts of the assignment used AI assistance
- What prompt or query was sent to the AI
- What the student verified in the AI's output and how
- One thing the AI got wrong or that required correction

The disclosure is not optional. Submissions without it are returned.
This is the assessment-level enforcement of the book's thesis.

---

# PART 8 — CHAPTER-BY-CHAPTER TOC

---

## ACT ONE — ESTABLISH (Modules 1–4)

*What this act does: establishes what Java objects are, what the JVM
does, and what it means to debug rather than guess. The student writes
real code before they understand all of it — and learns to sit with
that discomfort productively.*

---

### MODULE 0 — Welcome

**One-line:** Install the JDK, NetBeans, and configure your first
Java project without losing a lab session to tooling.

**Not a graded module.** Reference material. Screenshots for each
operating system. Steps verified for the current semester's software
versions. CLAUDE.md setup walkthrough included here for the first time.

**Key sections:**
- JDK installation (Windows / macOS / Linux)
- NetBeans installation and project creation
- Running your first Hello World
- Verifying the Java version the course requires
- **First CLAUDE.md: the diagnostic-only constraint**
  (AI may explain; AI may not write)

---

### MODULE 1 — Fundamentals of Programming in Java

**One-line:** Students learn why objects — not procedures — are the right
mental model for business software, by running and breaking a working
application before they write one.

**Learning outcomes:**
1. (Understand) Explain why a business problem maps more naturally to
   objects than to a list of instructions.
2. (Apply) Modify a provided Java program and predict the effect before
   running it.
3. (Analyze) Distinguish a compilation error from a runtime error and
   name the different diagnostic processes each requires.
4. (Evaluate) Assess which parts of a simple Java modification task
   are safe to delegate to AI and which require the engineer's
   own understanding.

**Opening:** A working Java program that models a library's book
checkout — three objects, two methods, one bug. Students run it,
observe the wrong output, and are asked to explain what went wrong
before any vocabulary is introduced.

**Core content:**
1. The program structure: JVM, compilation, the class as a blueprint
2. Why the object model: business entities as objects, not records
3. Functional vs. component structures: what each hides
4. The SDK and NetBeans: what the IDE does for you and what it cannot
5. Running and reading output: stdout is not the application

**Worked example:** The library checkout program — one book, one
patron, one checkout transaction. Walk through from source to running
output. Introduce the bug. Trace the wrong output to its cause.

**Assessable exercises:**
1. (Apply) Modify the checkout program to handle two books. Predict
   the output before running.
2. (Analyze) Given three error messages, classify each as compilation
   or runtime and explain the diagnostic implication.
3. (Evaluate — AI Use Disclosure) Run the unmodified checkout program
   through Claude with the prompt "explain what this code does." Compare
   the explanation to your own reading. Where do they differ?

**Chapter closing:** The student has a running program. The next
question: what happens when you need ten books, not two?

---

### **HOW TO USE AI — Module 1**

**What AI does well here (Tier 1):**
- Explaining what an unfamiliar Java keyword means
- Translating a Java error message into plain language
- Generating a list of what a provided code block does, line by line
- Suggesting what search terms to use when you're stuck

**Concrete prompt that works:**
```
I am a first-week Java student. Here is a compilation error:
[paste error here]
Explain what caused it and what category of mistake this is
(syntax error, type mismatch, missing import, etc.).
Do NOT rewrite the code. I need to fix it myself.
```

**What AI cannot do here (Tiers 4–7):**
- Tell you whether your mental model of what the code does is correct
  (only running it and tracing the output can do that)
- Decide which of two modifications is the right one for YOUR business
  requirement (only you know the requirement)
- Verify that a fix is correct (only you can run it and check)

**The Phase Gate for Module 1:**
You may use AI to explain code you have already written or code that
was provided. You may NOT use AI to write new code for this module.
The boundary: if you are asking AI to produce Java you will submit,
you are on the wrong side of the gate. If you are asking AI to help
you understand Java you already wrote or read, you are on the right side.

**Your CLAUDE.md for Module 1:**
```
You are a Java tutor for a first-week student.
RULES:
- Explain code. Do not write code.
- When the student pastes code, describe what it does line by line.
- When the student pastes an error, name the error type and explain
  the cause. Do not provide a fix.
- If the student asks you to write Java code, respond:
  "I can explain the concept instead. What are you trying to do?"
- Never produce a complete method or class body.
```

---

### MODULE 2 — Methods, Arrays, and File Objects

**One-line:** Students learn to instantiate multiple objects from one
class and trace how Java manages them in memory.

**Learning outcomes:**
1. (Understand) Explain the distinction between a class and an object,
   using the blueprint/instance metaphor.
2. (Apply) Write a Java class with attributes and methods, and
   instantiate two distinct objects from it.
3. (Analyze) Trace variable values across two objects and explain
   why changing one does not change the other.
4. (Apply) Extend the semester project's first class with two
   additional attributes.

**Opening:** Three printouts — same person's name, three different
ages. Students are shown the Java code before they know how it works.
They are asked: where are the three ages stored?

**Core content:**
1. Java syntax: class files, classes, objects, attributes, methods
2. The reference variable and the object: two different things
3. Memory usage: stack vs. heap (conceptual, not implementation detail)
4. Multiple objects from one class: why this matters for a business system
5. The program structure: main(), method calls, output

**Worked example:** The library checkout extended — add a second
patron, show that both can have checked-out books simultaneously.
Trace what happens in memory when both PatronA and PatronB are
created from the same Patron class.

**Assessable exercises:**
1. (Apply) Write a Book class with four attributes. Instantiate three
   Book objects with different values.
2. (Analyze) Given code that modifies patronA.name, explain why
   patronB.name is unchanged.
3. (Apply) Add a Book class to the semester project.

**AI Use Disclosure:** Required. Same diagnostic-only constraint as M1.

**Chapter closing:** You can create objects. The next question:
how do you let the user interact with them?

---

### **HOW TO USE AI — Module 2**

**What AI does well here (Tier 1):**
- Explaining what `new` does in Java
- Describing the difference between a field and a local variable
- Generating a list of questions you should be able to answer
  about your own class before submitting

**Concrete prompt that works:**
```
I wrote this Java class: [paste your class]
Quiz me on it. Ask me five questions about what this code does.
Do not explain it to me — ask questions I have to answer.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether your class design matches YOUR business problem's
  requirements (only you know the requirements)
- Verify that the attributes you chose are the right ones for the
  application you are building
- Tell you whether your mental model of stack vs. heap is correct
  for this specific code (only tracing through the code yourself
  can build that model)

**The Phase Gate for Module 2:**
Same as Module 1: AI explains, student writes. New this week: you
may use AI to check your class after you have written it — ask it
to find attributes or methods that might be missing. But the first
draft must be yours.

**Your CLAUDE.md for Module 2:**
```
You are a Java tutor for a second-week student learning classes
and objects.
RULES:
- Explain what code does. Do not write new code.
- When shown a class definition, identify potential design issues
  without rewriting it.
- You may ask the student quiz questions about their own code.
- If asked to add a method or attribute to a class, explain what
  such a method or attribute would need to do — do not write it.
- Never produce a complete class body.
```

---

### MODULE 3 — Objects and Classes

**One-line:** Students learn to design user flows as navigation between
screens, connecting what the user sees to what the objects do.

**Learning outcomes:**
1. (Understand) Explain how a screen navigation flow maps to object
   state changes in the underlying model.
2. (Apply) Implement a two-screen Java application using CardLayout,
   passing one object between screens.
3. (Analyze) Trace the object lifecycle through a screen navigation
   flow and identify where state is stored at each step.
4. (Evaluate) Assess a screen flow design for whether it correctly
   reflects the underlying business process.

**Opening:** A library checkout printed on paper as a sequence of
screens — Search → Result → Checkout → Confirmation. Students are
asked: what object is being passed between these screens? What does
that object know at each step?

**Core content:**
1. User flows as screen navigation flows: actions, states, transitions
2. CardLayout in Java: how panels replace each other
3. Passing objects between screens: why references, not copies
4. Data types and variables: integers, strings, primitives vs. references
5. The separation of concerns: the screen shows; the object knows

**Worked example:** The library checkout — three screens (Search,
Result, Confirm). A Book object moves through all three. Trace what
fields are populated at each screen transition.

**Assessable exercises:**
1. (Apply) Implement a two-screen application where a Patron object
   is created on Screen 1 and displayed on Screen 2.
2. (Analyze) Given a four-screen flow diagram, identify which object
   carries state between each transition.
3. (Apply) Design the screen flow for your semester project's primary
   user task.

**AI Use Disclosure:** Required.

**Chapter closing:** You can display objects on screens. The next
question: how does your system know which object to display when
you have hundreds?

---

### **HOW TO USE AI — Module 3**

**What AI does well here (Tier 1):**
- Explaining how CardLayout works in Java
- Generating a stub for passing an object between two panels
  (you fill in the business logic)
- Translating a screen flow diagram description into a list of
  classes and methods the implementation will need

**Concrete prompt that works:**
```
I am building a two-screen Java application using CardLayout.
Screen 1 collects a user's name and age as inputs.
Screen 2 displays them.
Generate ONLY the CardLayout and panel-switching skeleton —
no input handling, no business logic, no data classes.
I will fill those in myself.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether your screen flow reflects YOUR business process
  (only you know what the user is trying to accomplish)
- Decide what data needs to travel between screens in your
  application (only you know the requirements)
- Verify that the object you are passing has the right state
  at the right screen (only running and testing can verify that)

**The Phase Gate for Module 3:**
You may use AI to generate layout scaffolding (the skeleton of
panels and navigation). You may NOT use AI to generate the business
logic — the decisions about what happens when a user action occurs.
The boundary: structure is delegatable; behavior is yours.

**Your CLAUDE.md for Module 3:**
```
You are a Java layout assistant.
RULES:
- Generate only structural/layout code (panels, CardLayout, navigation).
- Do not generate business logic, data models, or decision code.
- When asked for business logic, respond: "That's the engineer's
  decision. What do you want to happen when the user clicks?"
- Mark every generated method body with a TODO comment indicating
  what the student must implement.
- Never produce a complete working application.
```

---

### MODULE 4 — Basics of Object-Oriented Programming Part 2

**One-line:** Students learn a systematic debugging methodology —
hypothesis, isolation, test — using the IDE debugger and their own
reasoning, not error message reading alone.

**Learning outcomes:**
1. (Apply) Apply the three-step debugging workflow (hypothesize,
   isolate, test) to a program with a known-but-unexplained defect.
2. (Analyze) Distinguish between a symptom (wrong output), a proximate
   cause (the line that fails), and a root cause (the design decision
   that made the failure possible).
3. (Apply) Use the NetBeans debugger to set a breakpoint, step through
   code, and inspect object state.
4. (Evaluate) Assess which parts of a debugging task are appropriate
   to delegate to AI and which require the engineer's own reasoning.

**Opening:** A program that compiles, runs, and produces wrong output.
No error message. Students are asked: what would you try first?
Three approaches are collected. Then the systematic approach is introduced.

**Core content:**
1. Functions and methods: parameter passing, program control flow
2. The debugger: breakpoints, step-over, step-into, inspect
3. The debugging workflow: symptom → hypothesis → isolation → test
4. The difference between fixing and understanding: why fixing without
   understanding produces the next bug
5. AI and debugging: what AI can do, what it cannot, and why

**Worked example:** The library checkout with a bug in the
checkout logic — a book gets checked out to the wrong patron under
a specific sequence of operations. Walk through the full debugging
workflow from symptom to root cause.

**Assessable exercises:**
1. (Apply) Given a program with a hidden bug, find it using only
   the debugger — no trial and error, no AI. Document each step.
2. (Analyze) Given a program that was "fixed" by changing a return
   value without understanding the cause, identify the root cause.
3. (Evaluate) What is the minimum you must understand about a bug
   before it is safe to ask AI for a fix? Write your answer as a
   checklist.

**AI Use Disclosure:** Required. New constraint this module: the
disclosure must include what the student understood about the bug
before asking AI anything.

**Chapter closing:** You can find bugs. The next question: how do
you build a system where fewer bugs hide?

---

### **HOW TO USE AI — Module 4**

**What AI does well here (Tier 1):**
- Explaining what a specific Java error type means in general terms
- Describing what a stack trace is telling you about call sequence
- Generating a checklist of common causes for a given error category

**Concrete prompt that works:**
```
I have a Java program with this bug: [describe the symptom — wrong
output or behavior, NOT the code yet].
Before I show you the code, give me a checklist of five common
root causes for this category of bug in Java.
I will use the checklist to inspect my code myself before asking
you to look at it.
```

**What AI cannot do here (Tiers 4–7) — this is the critical module:**
- Debug your code for you. AI can identify a proximate cause
  (the line that fails) but will often miss the root cause (the
  design decision upstream). If you accept an AI fix without
  understanding the root cause, the same class of bug will recur.
- Know whether a fix is correct for YOUR system's requirements.
  AI fixes the code it sees. It does not know your requirements.
- Perform the plausibility audit: "Does this fix make sense given
  how the rest of the system works?" Only you can do that.

**The Phase Gate for Module 4 — the hardest gate in the course:**
You must complete Step 1 (hypothesize) and Step 2 (isolate) of the
debugging workflow before AI may be consulted. This means: you must
be able to state, in writing, what you think the bug is and where
you think it is before you show the code to AI. If you cannot state
a hypothesis, you are not ready to use AI on this bug yet.

AI consultation rule: show AI your hypothesis first. Ask AI whether
your hypothesis is plausible — not whether it is correct. Then test
the hypothesis yourself.

**Your CLAUDE.md for Module 4:**
```
You are a debugging methodology coach for a Java student.
RULES:
- Do not identify the bug in code the student pastes.
- Ask the student: "What is your hypothesis about the cause?"
  before engaging with any code.
- Once a hypothesis is stated, assess whether it is plausible —
  do not confirm or deny it.
- If asked to fix code directly, respond: "What is your hypothesis?
  Walk me through your reasoning first."
- You may explain what a stack trace or error message is indicating
  in general terms.
- Never provide a code fix until the student has stated a verified
  hypothesis with evidence.
```

---

## ACT TWO — BUILD (Modules 5–10)

*What this act does: constructs the OO design toolkit piece by piece.
Each module adds one structural concept and requires the student to
apply it to their semester project. AI constraints relax progressively
as the student's verification capability builds.*

---

### MODULE 5 — Inheritance and Polymorphism

**One-line:** Students learn to model the entities that provide
resources in a business system — the objects that exist before any
user interacts with them.

**Learning outcomes:**
1. (Apply) Design a supply-side object model for the semester project
   with at least three classes and their relationships.
2. (Analyze) Distinguish between objects that represent real-world
   entities, objects that represent relationships, and objects
   that represent transactions.
3. (Apply) Implement model relationships in Java as a complete,
   runnable application.
4. (Evaluate) Assess an AI-generated class design against the
   requirements the student specified.

**Opening:** A library's catalog — books exist before any patron
arrives. What does the catalog object know? What can it do? What
does it NOT know? The distinction between the supply-side model
and the user-facing model is introduced through a concrete example
where confusing them produces a wrong design.

**Core content:**
1. Simple arrays and indexing: storing collections of objects
2. While and for loops: iterating over collections
3. OO principles: Abstraction, Inheritance (introduced),
   Polymorphism (introduced), Encapsulation
4. Entity vs. relationship vs. transaction objects
5. The supply-side model: what exists before users arrive

**Worked example:** The library catalog — a Catalog class that
contains Book objects. The Book class designed by the student in
M2 is integrated. A search method. A full working application.

**Assessable exercises:**
1. (Apply) Add a Catalog class to the semester project. It must
   contain at least 5 pre-loaded objects.
2. (Analyze) Given an over-engineered class diagram, identify which
   classes are entities, which are relationships, and which are
   unnecessary.
3. (Evaluate — AI gate) Generate a class design for the supply side
   of your project using AI. Then assess it: which design decisions
   would you change and why?

**AI Use Disclosure:** Required. New this module: disclosure must
name one design decision in the AI's output that the student
disagreed with and explain why.

**Chapter closing:** Your system knows about its resources. The next
question: how do users authenticate and become part of the system?

---

### **HOW TO USE AI — Module 5**

**What AI does well here (Tier 1):**
- Generating a class stub from a written specification
- Suggesting method signatures for a described behavior
- Identifying missing methods in a class design the student wrote

**Concrete prompt that works:**
```
I am designing the supply-side model for a [library / inventory / 
appointment scheduling] system.

Here is my written specification of what the Catalog class
must do: [your spec — not a vague description, a list of
capabilities with inputs and outputs].

Generate a Java class stub with method signatures and field
declarations. No method bodies. Mark every design decision
you made with a comment explaining the alternative you
considered.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether a class design is correct for YOUR business problem
  (AI will generate a reasonable generic design; you must assess
  it against your specific requirements)
- Decide whether a class boundary is in the right place
  (that is a design judgment requiring knowledge of the whole system)
- Verify that the generated design will support the features you
  will need to add in Modules 6–10

**The Phase Gate for Module 5:**
Write your specification first. Specification means: for each class
you need, name it, list what it knows (fields) and what it can do
(methods), and describe the relationship to other classes. Only
then show it to AI. The spec is the gate. No spec, no AI.

**Your CLAUDE.md for Module 5:**
```
You are a Java class design reviewer for a graduate student.
RULES:
- Generate class stubs only when given a written specification.
- If given a vague description instead of a spec, respond:
  "I need a specification. For each class, tell me: what does
  it know (fields) and what can it do (methods)?"
- Generate stubs with empty method bodies and TODO comments.
- For every design decision, add a comment: "DESIGN DECISION:
  [what you chose] — ALTERNATIVE: [what else was possible]"
- Never generate a complete implementation.
```

---

### MODULE 6 — Basics of GUI Programming in Java

**One-line:** Students learn to model users and authentication as
first-class objects — not as a database lookup, but as a designed
part of the object system.

**Learning outcomes:**
1. (Apply) Implement a login process using a Person class and a
   UserAccount directory.
2. (Analyze) Explain why storing a password hash instead of a
   plaintext password is a design decision, not a security feature.
3. (Apply) Model the relationship between a Person object and a
   UserAccount object without conflating them.
4. (Evaluate) Assess the security implications of an AI-generated
   authentication implementation.

**Opening:** Two login systems — one that stores passwords in plain
text, one that stores hashes. The student is shown both. No security
vocabulary yet. They are asked: if someone reads your database,
what can they do with each?

**Core content:**
1. Java collections: List, Map, Set — when to use each
2. The Person class and the UserAccount class: different objects,
   different responsibilities
3. Password hashing: what it does and what it does not protect
4. The login process as an object interaction sequence
5. Separation of authentication from authorization

**Worked example:** The library checkout — patron login. A
PersonDirectory that stores UserAccount objects keyed by username.
The hash of the password stored, not the password. The login
process traced as object method calls.

**Assessable exercises:**
1. (Apply) Implement a LoginManager class that authenticates a
   user against a PersonDirectory.
2. (Analyze) Given a login implementation, identify three security
   implications — not vulnerabilities, implications. ("If X, then Y.")
3. (Evaluate) Ask AI to implement a login system without specifying
   the password handling requirement. Then assess what it produced.

**AI Use Disclosure:** Required. Security note added to standard form:
if AI generated authentication code, the disclosure must state which
security properties the student verified.

**Chapter closing:** Your system has users. The next question:
what can different users do?

---

### **HOW TO USE AI — Module 6**

**What AI does well here (Tier 1):**
- Generating the scaffolding for a Map-based user directory
- Explaining how `HashMap.containsKey()` and `HashMap.get()` work
- Listing the most common mistakes in Java authentication implementations

**Concrete prompt that works:**
```
I am implementing a simple user authentication system in Java.
Requirements:
- Users stored in a HashMap<String, String> where key=username,
  value=hashed password
- I will handle password hashing separately
- Login method takes a username and password, returns boolean

Generate only the class structure and method signatures.
For the login method body, write a comment explaining the
exact steps it must take — do not implement it.
I will implement the body myself.
```

**What AI cannot do here (Tiers 4–7) — security note:**
Assessing whether an authentication design is appropriate for
your use case requires understanding the threat model — who are
the adversaries, what access do they have, what are they trying
to do? AI does not know your threat model. AI-generated auth
code is often technically correct and contextually wrong.
Before accepting any AI-generated security-related code, you
must be able to answer: "If an attacker has X, what can they
do with this code?"

**The Phase Gate for Module 6:**
Authentication code requires a higher gate. Before AI writes any
authentication logic, you must write (in plain English) the answer
to: "If someone reads my user database, what can they do?" If you
cannot answer this, you are not ready to design authentication yet.

**Your CLAUDE.md for Module 6:**
```
You are a Java security-aware code reviewer.
RULES:
- Before generating any authentication-related code, ask:
  "What is your threat model? What happens if the user database
  is read by an attacker?"
- Do not generate authentication implementations until a threat
  model is stated.
- For all generated code, add a comment: "SECURITY ASSUMPTION:
  [what this code assumes about the environment]"
- If asked to store passwords (in any form) without a hashing
  requirement stated, ask: "Are you hashing the password before
  storage? If not, explain why."
- Never generate plaintext password storage code.
```

---

### MODULE 7 — Midterm Exam

**One-line:** Students learn why polymorphism is not a Java feature
but a design strategy — the ability to add new types without
changing existing code.

**Learning outcomes:**
1. (Understand) Explain what polymorphism produces at runtime —
   which method runs when you call a method on a supertype reference.
2. (Apply) Design an inheritance hierarchy for the order/transaction
   objects in the semester project.
3. (Analyze) Identify the design scenario where polymorphism eliminates
   a chain of if-else statements.
4. (Evaluate) Assess an AI-generated inheritance hierarchy against
   the Liskov Substitution Principle (introduced informally).

**Opening:** A checkout system with three types of transactions:
standard checkout, reserve, and renew. A chain of if-else statements
handles each. Then the same system redesigned with inheritance.
Students are asked: what changed? What got easier? What got harder?

**Core content:**
1. Java collections: sort API (Comparator, Comparable)
2. Superclasses and subclasses: the is-a relationship
3. Method overriding: why the subclass method runs
4. Polymorphism: one reference, many possible types
5. The open/closed principle: open for extension, closed for modification

**Worked example:** Transaction types in the library — Checkout,
Reserve, Renew all extend Transaction. A TransactionProcessor that
handles any Transaction without knowing its type. Adding a new
transaction type without modifying the processor.

**Assessable exercises:**
1. (Apply) Redesign the semester project's transaction handling using
   polymorphism. Remove all type-checking if-else chains.
2. (Analyze) Given an inheritance hierarchy, identify one case where
   a subclass violates the contract of its superclass.
3. (Evaluate) Ask AI to design an inheritance hierarchy for a
   described domain. Assess whether each subclass truly is-a
   of the parent.

**AI Use Disclosure:** Required. Disclosure must include: one design
decision in the AI's hierarchy that the student changed and why.

**Chapter closing:** Your system can process different transaction
types uniformly. The next question: how do you store and query
large collections of them?

---

### **HOW TO USE AI — Module 7**

**What AI does well here (Tier 1):**
- Generating an inheritance hierarchy from a written list of types
  and their shared/distinct behaviors
- Explaining why a specific method override would or wouldn't compile
- Producing a comparison of two design alternatives with trade-offs listed

**Concrete prompt that works:**
```
I am designing an inheritance hierarchy for transaction objects
in a [library / inventory / scheduling] system.

Transaction types and their unique behaviors:
- [Type A]: [what it does differently]
- [Type B]: [what it does differently]
- [Type C]: [what it does differently]

Shared behavior for all transactions:
- [shared behavior 1]
- [shared behavior 2]

Generate a class hierarchy. For each inheritance decision,
add a comment: "IS-A CHECK: [why TypeX truly is a Transaction]"
Flag any type where the is-a relationship is questionable.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether your inheritance hierarchy will support the features
  you haven't specified yet (only you know where the design is going)
- Evaluate whether your subclasses genuinely satisfy the superclass
  contract for YOUR system (LSP requires knowing the contracts, which
  are in your head, not AI's context)

**The Phase Gate for Module 7:**
Write the is-a check yourself first: for each subclass you propose,
write one sentence — "[Subclass] is a [Superclass] because [reason]."
If you cannot write the sentence convincingly, the hierarchy is wrong.
Then ask AI to check your reasoning.

**Your CLAUDE.md for Module 7:**
```
You are a Java OO design reviewer specializing in inheritance.
RULES:
- For every inheritance relationship the student proposes, ask:
  "Complete this sentence: '[Subclass] is a [Superclass] because...'"
- If the student cannot complete the sentence, do not generate code.
- For generated hierarchies, mark every questionable is-a relationship
  with: "IS-A WARNING: Consider whether [Subclass] truly is a [Superclass]"
- Explain the Liskov Substitution Principle in plain language
  when violations appear.
- Do not generate hierarchies based on vague descriptions.
  Ask for explicit is-a statements first.
```

---

### MODULE 8 — Abstract Classes and Interfaces

**One-line:** Students learn to design the full lifecycle of data
in a business application — create, read, update, delete — and
to implement it with file-based persistence.

**Learning outcomes:**
1. (Apply) Implement CRUD operations for the semester project's
   primary entity using CSV file storage.
2. (Analyze) Trace the data lifecycle from user input to file storage
   to object in memory to screen display.
3. (Apply) Handle file I/O exceptions without crashing the application.
4. (Evaluate) Assess an AI-generated data management implementation
   for data loss scenarios.

**Opening:** A library catalog that exists only in memory — restart
the program, lose all the data. Students are asked: what would you
need to add to make the data survive a restart? Three approaches
are listed. The trade-offs are discussed before any implementation.

**Core content:**
1. Java collections (List, Map, Set) — deeper treatment
2. File objects: reading from and writing to CSV files
3. CRUD as a design pattern: the four operations every persistent
   entity needs
4. Exception handling: what happens when the file doesn't exist
5. Data integrity: what can go wrong between memory and disk

**Worked example:** The library catalog with CSV persistence — load
on startup, save on shutdown, add/remove/update during operation.
A data loss scenario introduced deliberately: what happens if the
program crashes between an add and a save?

**Assessable exercises:**
1. (Apply) Add CSV persistence to the semester project's primary
   entity. Test by shutting down and restarting.
2. (Analyze) Identify two scenarios in your implementation where
   data could be lost or corrupted.
3. (Evaluate) Ask AI to implement CRUD for a described entity.
   Find at least one data loss scenario in the generated code.

**AI Use Disclosure:** Required. Disclosure must include: one data
loss scenario the student found in their own implementation (AI-assisted
or not) and how they addressed it.

**Chapter closing:** Your data survives restarts. The next question:
how do you present it through a visual interface?

---

### **HOW TO USE AI — Module 8**

**What AI does well here (Tier 1):**
- Generating CRUD method stubs for a described entity
- Producing CSV read/write boilerplate
- Listing common data loss scenarios for a described implementation

**Concrete prompt that works:**
```
I am implementing CSV-based persistence for a Java application.
Entity: [your entity name]
Fields: [list each field with its Java type]

Generate:
1. A method to write a List<[Entity]> to a CSV file
2. A method to read a CSV file into a List<[Entity]>
3. A TODO comment in each method marking where exception
   handling must be added

Do NOT implement exception handling — mark where it is needed.
Do NOT generate a complete application.
```

**What AI cannot do here (Tiers 4–7):**
- Know which data loss scenarios matter for YOUR application
  (some data loss is acceptable in some contexts; only you know
  what the requirements say about data durability)
- Decide the right error-handling strategy for your users
  (should a read failure crash? warn? silently recover?
  Only you know the user experience requirements)

**The Phase Gate for Module 8:**
Before using AI for data persistence code, write down the answers to:
1. What is the worst thing that can happen if a write fails?
2. What should the application do if the data file doesn't exist?
3. What is the maximum data loss acceptable to the user?
Only after answering these may AI write persistence code.

**Your CLAUDE.md for Module 8:**
```
You are a Java data persistence reviewer.
RULES:
- Before generating persistence code, ask:
  "What happens if the write fails? What should the application do?"
- Mark every place where an exception could occur with:
  "EXCEPTION RISK: [what can fail here] — STUDENT MUST HANDLE"
- Do not implement exception handling. Mark it.
- Flag every scenario where data could be lost or duplicated
  with: "DATA RISK: [describe the scenario]"
- Do not generate complete data persistence implementations.
```

---

### MODULE 9 — Event-Driven Programming

**One-line:** Students learn to sort, filter, and search collections
of objects — and to choose the right collection type for each task.

**Learning outcomes:**
1. (Apply) Implement sorting for a collection of domain objects
   using Comparator and Comparable.
2. (Analyze) Choose between List, Map, and Set for three different
   collection tasks and justify each choice.
3. (Apply) Implement search and filter operations on the semester
   project's collection of primary entities.
4. (Evaluate) Assess an AI-generated sorting implementation for
   correctness and performance implications.

**Opening:** A library search — 500 books, the patron wants them
sorted by title, then by author, then by year. The naive solution.
The better solution. The students are asked to predict the performance
difference before it is measured.

**Core content:**
1. Java sort API: Comparator, Comparable — when to use each
2. List vs. Map vs. Set: the data structure decision
3. Filtering with streams (introductory): declarative vs. imperative
4. Search implementation: linear search when it's fine, when it isn't
5. The collection choice as a design decision: the wrong choice
   now is a rewrite later

**Worked example:** The library catalog — sorting by three criteria,
filtering by availability, searching by partial title. The Map choice
for ISBN lookup. The List choice for ordered display.

**Assessable exercises:**
1. (Apply) Implement three sort orders for the semester project's
   primary entity.
2. (Analyze) Identify one collection in the semester project where
   the current choice (List, Map, or Set) is wrong. Explain why
   and what the correct choice is.
3. (Evaluate) Ask AI to implement a search function. Assess its
   time complexity for your expected data size.

**AI Use Disclosure:** Required.

**Chapter closing:** Your system can organize data. The next
question: how does the user see and interact with it?

---

### **HOW TO USE AI — Module 9**

**What AI does well here (Tier 1):**
- Generating a Comparator implementation for a described sort order
- Explaining the difference between `Comparable` and `Comparator`
  with examples
- Producing a summary table of List/Map/Set trade-offs

**Concrete prompt that works:**
```
I need to sort a List<[YourEntity]> by [field1] ascending, then
by [field2] descending when [field1] values are equal.

Generate a Comparator<[YourEntity]> that does this.
Add a comment explaining why chained comparison is needed.
Do not modify the entity class.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether a sort is correct for your business logic
  (sort correctness is a requirements question, not a code question)
- Decide the right collection type for your system's access patterns
  (that requires knowing how the data will be accessed, which is
  in your design, not AI's context)

**The Phase Gate for Module 9:**
Before asking AI to generate collection code, answer: "What are the
three most common operations on this collection?" List them. Then
choose your collection type based on the answer. Then ask AI to
implement it.

**Your CLAUDE.md for Module 9:**
```
You are a Java collections design reviewer.
RULES:
- Before generating collection code, ask:
  "What are the three most common operations on this collection?
  What is the expected size?"
- For every collection type used, add a comment:
  "COLLECTION CHOICE: Used [List/Map/Set] because [reason] —
  ALTERNATIVE: [what else was possible and why it was not chosen]"
- Flag O(n) operations on large collections with:
  "PERFORMANCE NOTE: This is O(n) — acceptable for [expected size]?"
- Do not generate code for unspecified requirements.
```

---

### MODULE 10 — Event-Driven Programming with Scene Builder

**One-line:** Students learn to connect the object model they have
built to a visual interface — understanding that the GUI is a view
of the model, not the model itself.

**Learning outcomes:**
1. (Apply) Build a basic JavaFX application that displays data from
   a domain object.
2. (Understand) Explain the separation between the model (objects),
   the view (JavaFX scene), and the controller (event handling).
3. (Apply) Use JavaFX layout panes, UI controls, and shapes to
   display a list of domain objects.
4. (Evaluate) Assess the readability and maintainability of a
   GUI implementation against the model-view-controller principle.

**Opening:** The library catalog shown in two ways — a console dump
of Book objects, and a JavaFX table view of the same objects. The
code for each. Students are asked: what changed? What stayed the same?

**Core content:**
1. GUIs, JavaFX: the scene graph and its structure
2. Panes, UI controls, shapes: the building blocks
3. Property binding: connecting an object's value to a display
4. Layout panes: how the screen organizes itself
5. Scene Builder: using the visual designer and understanding
   what it generates

**Worked example:** The library catalog in JavaFX — a TableView
displaying Book objects. A search bar that filters the table.
The model is unchanged; only the view is new.

**Assessable exercises:**
1. (Apply) Add a JavaFX interface to the semester project's catalog
   view. The underlying model must be unchanged.
2. (Analyze) Identify one place in your GUI where model logic
   has leaked into the view. Describe how to separate it.
3. (Evaluate) Ask AI to generate a JavaFX screen for a described
   model. Identify where the AI violated the model-view separation.

**AI Use Disclosure:** Required. New this module: GUI code is
high-AI-assistance territory. The disclosure must explicitly state
how much of the JavaFX code was AI-generated and what the student
verified.

**Chapter closing:** Your system has a visual interface. The next
question: how does the user tell it what to do?

---

### **HOW TO USE AI — Module 10**

**What AI does well here (Tier 1):**
GUI boilerplate is one of the highest-value AI assistance areas in
this course. JavaFX scene setup, TableView configuration, and layout
code are highly repeatable and well-represented in AI training data.

**Concrete prompt that works:**
```
I have a Java class: [paste your model class — fields and getters only]

Generate a JavaFX TableView that displays a List<[YourClass]>
with one column per field.

Requirements:
- No event handling code
- No controller logic
- Only the TableView setup and column configuration
- Use PropertyValueFactory for each column

I will add event handling in the next module.
```

**What AI cannot do here (Tiers 4–7):**
- Know which columns matter to YOUR users (that is a UX design
  decision requiring knowledge of who uses your application)
- Ensure the GUI matches your application's conceptual model
  (only you can verify that what is displayed matches what
  the objects actually contain)
- Decide the right layout for your specific workflow
  (layout is a UX decision requiring knowledge of your user's tasks)

**The Phase Gate for Module 10:**
GUI code from AI must be run and tested before submission. The test:
display real data from your model (not hardcoded strings) and
verify that every displayed value matches the object's actual field
value. If you cannot trace a displayed value back to a field in
your model, you do not understand the GUI code well enough to submit it.

**Your CLAUDE.md for Module 10:**
```
You are a JavaFX layout assistant.
RULES:
- Generate layout and display code only.
- Do not generate event handlers, business logic, or data models.
- For every UI component that displays data, add a comment:
  "DATA SOURCE: This displays [fieldName] from [ClassName]"
- Mark every place where the student must connect the display
  to their model with: "STUDENT: Connect this to your model here"
- If asked to generate a complete working JavaFX application,
  respond: "I'll generate the view layer. You connect it to
  your model. What model class am I displaying?"
```

---

## ACT THREE — APPLY (Modules 11–14)

*What this act does: stops giving well-defined problems and gives
the student the kind of problems they will actually encounter —
incomplete requirements, competing constraints, and the need to make
defensible design decisions. AI assistance is at its highest level;
the design judgment requirement is also at its highest.*

---

### MODULE 11 — Generics

**One-line:** Students learn to connect user actions to application
behavior using JavaFX event handling — and to maintain the
model-view separation under the pressure of deadline.

**Learning outcomes:**
1. (Apply) Implement event handlers for the primary user actions
   in the semester project.
2. (Analyze) Trace the complete path from a user click to a model
   state change to a view update.
3. (Apply) Use inner classes and lambda functions for event handling.
4. (Evaluate) Assess an event-driven implementation for handler
   methods that violate the model-view separation.

**Opening:** A button that does everything — one handler method that
validates input, updates the model, formats the output, updates
three UI components, and writes to a file. The student is asked to
count the responsibilities. Then the same functionality correctly
decomposed.

**Core content:**
1. Event-driven programming: the event loop model
2. Handlers: registering, implementing, inner classes
3. The KeyEvent class and keyboard handling
4. Lambda functions: when to use them for event handling
5. The single-responsibility principle applied to handlers

**Worked example:** The library checkout flow — button click triggers
checkout, updates patron record, updates book status, refreshes the
table view. Each step in a separate method with a single responsibility.

**Assessable exercises:**
1. (Apply) Implement event handling for three user actions in
   the semester project.
2. (Analyze) Find one event handler in your implementation that
   has more than one responsibility. Decompose it.
3. (Evaluate) Ask AI to generate a complete event handler for a
   described user action. Count its responsibilities.

**AI Use Disclosure:** Required.

**Chapter closing:** Your application responds to users. The next
question: how do you make it respond to more users with more
complex data?

---

### **HOW TO USE AI — Module 11**

**What AI does well here (Tier 1):**
- Generating event handler registration boilerplate
- Translating a described action sequence into a method call chain
- Identifying handler methods with multiple responsibilities

**Concrete prompt that works:**
```
I have a JavaFX button that, when clicked, should:
1. [First action — specific, named]
2. [Second action — specific, named]
3. [Third action — specific, named]

Generate an event handler that calls THREE SEPARATE methods —
one per action. Do not implement the method bodies.
Add a TODO comment in each method body specifying what it must do.

I will implement each method body myself.
```

**What AI cannot do here (Tiers 4–7):**
- Know the right decomposition of responsibilities for YOUR
  application's architecture (that requires understanding the whole
  system, which is in your head)
- Decide what should happen on validation failure for YOUR
  users (that is a UX and requirements decision)

**The Phase Gate for Module 11:**
Before writing any event handler, write the action sequence in plain
English: "When the user clicks [button], the application should [1],
[2], [3]." Each item in the sequence becomes one method call.
This written sequence is the spec. AI works from the spec.

**Your CLAUDE.md for Module 11:**
```
You are a JavaFX event handling assistant.
RULES:
- Before generating any event handler, ask for a written action
  sequence: "List each thing that should happen, in order,
  when this event fires."
- Generate handlers that call separate methods — one per action.
  Never put multiple actions in a single handler body.
- Add "RESPONSIBILITY: [what this method does]" to every method stub.
- Mark every place where model state changes with:
  "MODEL UPDATE: [what changes and to which object]"
- Do not implement method bodies. Generate stubs with TODO comments.
```

---

### MODULE 12 — Recursion

**One-line:** Students learn to use Scene Builder to design complex
interfaces while maintaining a clean boundary between the visual
design and the application logic.

**Learning outcomes:**
1. (Apply) Design a multi-screen interface using Scene Builder for
   the semester project's primary workflow.
2. (Analyze) Explain how Scene Builder-generated FXML relates to
   the JavaFX code it replaces.
3. (Apply) Connect a Scene Builder-designed interface to a Java
   controller using `@FXML` annotations.
4. (Evaluate) Assess a Scene Builder interface design against
   the user flow designed in Module 3.

**Opening:** The semester project's Module 3 screen flow — drawn
on paper in Module 3, implemented in JavaFX code in Module 10.
Now: what would it take to redesign the layout for a different
user? Scene Builder answers this question visually.

**Core content:**
1. Scene Builder: the visual FXML editor
2. FXML: what it is, what it generates, when to read it
3. The `@FXML` annotation and controller injection
4. Connecting visual components to controller logic
5. When to use Scene Builder and when to write JavaFX directly

**Worked example:** The library checkout interface redesigned in
Scene Builder — the same controller, new layout. The FXML generated
by Scene Builder read back against the hand-written JavaFX from M10.

**Assessable exercises:**
1. (Apply) Redesign one screen of the semester project in
   Scene Builder. The controller is unchanged.
2. (Analyze) Read the FXML generated by Scene Builder and
   identify the elements that correspond to code you wrote in M10.
3. (Evaluate) Ask AI to generate an FXML layout for a described
   interface. Verify that every declared element has a corresponding
   controller connection.

**AI Use Disclosure:** Required. Scene Builder generates code;
AI generates code. The disclosure must clearly distinguish which
parts were generated by each tool.

**Chapter closing:** You can design interfaces visually. The next
question: how do you design interfaces for many types of data?

---

### **HOW TO USE AI — Module 12**

**What AI does well here (Tier 1):**
- Generating `@FXML` controller stubs from an FXML file
- Explaining what a specific FXML element produces in the scene
- Translating a screen description into an FXML structure

**Concrete prompt that works:**
```
I have the following Scene Builder-designed interface: [paste FXML]

Generate the Java controller class that connects to this FXML.
Requirements:
- Declare every `fx:id` as an `@FXML` field
- Generate method stubs for every `onAction` handler
- Add a comment to each stub: "HANDLER FOR: [what UI element
  triggers this]"
- Do not implement any handler logic

I will implement the handlers myself.
```

**What AI cannot do here (Tiers 4–7):**
- Know whether the interface design serves YOUR users' workflow
  (visual design is a UX judgment, not a code question)
- Verify that the controller connections are correct for YOUR model
  (only running and testing can verify that)

**The Phase Gate for Module 12:**
For every `@FXML` element in your controller: before submitting,
trace it to the FXML element it connects to, run the application,
and verify the element appears and responds correctly. If you
cannot trace every field and handler, the connection is not verified.

**Your CLAUDE.md for Module 12:**
```
You are a JavaFX FXML-to-controller connector.
RULES:
- Generate controller stubs from FXML only when FXML is provided.
- For every @FXML field, add: "CONNECTS TO: [fx:id in FXML]"
- For every handler stub, add: "TRIGGERED BY: [UI element]"
- Do not implement handler logic. Stub only.
- If asked to design a complete interface without FXML,
  respond: "I'll work from your FXML or your Scene Builder design.
  Which do you have?"
```

---

### MODULE 13 — Collections and Iterators

**One-line:** Students learn to write tests for their own code and
use Java's advanced collection operations — and discover that
untested code is code whose correctness you are guessing at.

**Learning outcomes:**
1. (Apply) Write unit tests for three methods in the semester project
   using JUnit.
2. (Analyze) Explain why a test that passes does not prove correctness —
   it proves the tested behavior.
3. (Apply) Use lambda functions to replace simple loop patterns in
   collection operations.
4. (Evaluate) Assess AI-generated tests for what they do and do not
   cover.

**Opening:** A method that works correctly on Monday. On Tuesday a
new feature is added. The method breaks. Nobody notices until the
demo. Students are asked: how would a test have caught this?

**Core content:**
1. Unit testing: JUnit, test methods, assertions
2. What tests can and cannot prove
3. Test-driven thinking: writing the test before the code
4. Lambda functions: functional interfaces, method references
5. Advanced collections: streams, filter, map, collect

**Worked example:** The library catalog's search method — tested
with five cases: empty catalog, one result, multiple results,
no result, null input. Each test written before the method is
confirmed working. One test that fails, revealing a bug.

**Assessable exercises:**
1. (Apply) Write unit tests for five methods in the semester project.
   At least two tests must fail initially (revealing bugs).
2. (Analyze) For one of your tests, explain what it does NOT prove.
3. (Evaluate) Ask AI to generate unit tests for one of your methods.
   Identify the cases it missed.

**AI Use Disclosure:** Required. Disclosure must include:
one test case the AI missed that the student added.

**Chapter closing:** Your application is tested. The final
question: how does it all come together?

---

### **HOW TO USE AI — Module 13**

**What AI does well here (Tier 1):**
- Generating test method stubs for described behaviors
- Suggesting edge cases the student may not have considered
- Generating lambda equivalents for a described loop

**Concrete prompt that works:**
```
I have this Java method: [paste method signature and description only]

List 8 test cases for this method. For each case, specify:
- Input
- Expected output
- Why this case is interesting (boundary, normal, error)

Do NOT write the JUnit test code. I will write the tests myself
from your list.
```

**What AI cannot do here (Tiers 4–7) — testing critical note:**
AI-generated tests test what the AI thinks the method should do.
If the AI misunderstood your requirements (common), the tests will
pass even when the method is wrong. The only tests that prove YOUR
method meets YOUR requirements are tests written by someone who
understands the requirements. That is you.

**The Phase Gate for Module 13:**
For every AI-generated test: read it and answer — "Is this testing
the behavior I care about, or the behavior AI assumed I cared about?"
If you cannot answer this, do not submit the test.

**Your CLAUDE.md for Module 13:**
```
You are a test case design assistant.
RULES:
- Do not write JUnit test code. Generate test case descriptions only.
- For each test case, state: input, expected output, and
  the behavior category (normal, boundary, error, null).
- After generating cases, ask: "Are there business rules in your
  requirements that would add cases I haven't considered?"
- If asked to write complete unit tests, respond:
  "I'll describe the cases. You write the tests — that's where
  you verify the method does what YOU require, not what I assumed."
- Never generate tests for requirements that haven't been stated.
```

---

### MODULE 14 — Lists, Stacks, Queues, and the Final Project

**One-line:** Students complete, defend, and present a full GUI
business application — and demonstrate, for every AI-assisted
decision, what required their own engineering judgment.

**Learning outcomes:**
1. (Create) Complete and present a working GUI application that
   meets the semester project requirements.
2. (Evaluate) Apply the three-question AI audit to every AI-assisted
   component of the final application.
3. (Create) Demonstrate the application's operation and explain any
   three design decisions in response to examiner questions.
4. (Evaluate) Identify three places in the application where the
   requirements explicitly prohibited AI delegation — and verify
   they were handled by the student.

**Opening:** What does "done" look like? The final project rubric
presented before any student work begins. The examiner's three
questions are named: What does this component do? Why did you
design it this way? What would you change if you had more time?

**Core content:**
1. Ecosystem design: data stores, external dependencies, deployment
2. Advanced topics: multithreading (introductory), memory management
3. The final project AI Use Disclosure (higher bar — see below)
4. The three-question audit as a defense preparation tool
5. Code review as a professional practice: what you owe the next
   engineer who reads your code

**Assessment:**
Final Project (50% of course grade). Requires:
- A running GUI application demonstrating the primary business workflow
- Full source code with AI Use Disclosures in commit comments
- A written reflection: three AI-assisted decisions and what the student
  verified in each
- A live demonstration with examiner questions

**Final project AI Use Disclosure (higher bar):**
Must name three decisions across the full application that required
engineering judgment no AI tool could supply — variable specification,
design rationale, or testing judgment — with evidence from the code.

**Chapter closing:** The application is complete. The final
appendix, "How to Use Claude for Java," documents everything this
course taught about AI collaboration as a reference for professional
practice.

---

### **HOW TO USE AI — Module 14**

**This is a synthesis module.** All constraints from Modules 1–13
remain active. The CLAUDE.md for the final project combines
constraints from all prior modules. The student writes it themselves
as the first deliverable of Module 14.

**What AI does well here (all Tier 1 from prior modules):**
Review Modules 1–13 AI sections. Everything on the AI-appropriate
list from prior modules remains appropriate. Additionally:
- Generating integration code that connects components already written
- Producing documentation from code the student wrote
- Identifying inconsistencies across the codebase

**The three-question AI audit (applied to every component):**
Before the final submission, apply this audit to every AI-assisted
component:
1. Can I explain what this component does without referring to
   the AI's explanation?
2. Can I explain why I designed it this way — and would I make
   the same decision again?
3. Can I trace every non-trivial behavior in this component to
   either a test that covers it or a reason it was not tested?

If any answer is "no," the component is not ready to submit.

**The Phase Gate for Module 14 — the final gate:**
The CLAUDE.md the student writes for their final project is itself
assessed. It must reflect the constraint discipline developed across
the course. A CLAUDE.md that says "do whatever I ask" is a project
that has not met the course's learning objectives. A CLAUDE.md that
says "help me verify what I built" is a project that has.

**Your CLAUDE.md for Module 14 (student-written — assessed):**
No template provided. The student writes this based on what they
have learned across the course. The rubric for the CLAUDE.md:
- Does it specify what AI may and may not do for this project?
- Does it require AI to mark every design decision?
- Does it protect at least three categories of engineering judgment
  from delegation?
- Is it specific to THIS application, not generic?

---

# PART 9 — CHAPTER ANATOMY TEMPLATE

All 14 modules follow this structure:

1. Module overview (1 paragraph — what the student will build
   by the end of this module, not what they will learn about)
2. Prerequisites (named capabilities from prior modules)
3. Learning objectives (Bloom's level explicit)
4. Opening case (running, broken, or incomplete code — not a
   definition; something the student can run and observe)
5. Core content sections (4–6), each: concept → worked example
   → application to semester project
6. Mid-module checkpoint (ungraded; a question or small exercise
   that surfaces confusion before the main lab)
7. Lab assignment (the module's assessable deliverable — always
   an addition to the semester project)
8. **HOW TO USE AI** section (what AI does well this module,
   one concrete prompt, what AI cannot do, the phase gate,
   the CLAUDE.md for this module)
9. AI Use Disclosure form (structured — see assessment section)
10. Module summary (capabilities gained, stated as things the
    student can now DO in their project)
11. Key terms (5–10, plain language, Java-specific where relevant)
12. Bridge question (one question that raises what the next module
    answers)
13. Further reading (2–3 sources with one-sentence annotation)
14. CLI Quick Reference (the command-line operations introduced
    or used this module, with syntax and examples)

**Enforcement:** A draft module missing items 4, 7, 8, or 9 is
an incomplete draft. Do not advance to peer review without resolving it.

---

# PART 10 — CASE STUDY STRATEGY

## The single-thread approach

Unlike most OO textbooks that use a different example per chapter,
this book threads one business problem across all 14 modules:
the library management system (Domain A), with parallel problems
for inventory (Domain B) and scheduling (Domain C).

**Why:** The student's OO design challenges compound across modules.
The bugs they introduce in Module 2 appear in Module 5. The design
decisions they make in Module 7 constrain what is possible in Module 11.
This is how real software works.

## Case escalation

Act One cases: single class, clear right answer.
Act Two cases: multiple classes, trade-offs between designs.
Act Three cases: full system, no single right answer — the student
must make and defend decisions.

## AI case strategy

Every module's "HOW TO USE AI" section uses a concrete prompt
from the module's domain — not a generic prompt, a prompt written
for the library/inventory/scheduling system the student is building.
This is deliberate: AI prompting is a skill that requires domain
knowledge. A vague prompt produces vague code. The case strategy
teaches prompting discipline through domain specificity.

## Sourcing

Every case in this book is either:
- Derived from the course's lab sequence (labeled "course lab")
- Illustrative (labeled "illustrative" — not a real system)

No cases are presented as real systems without citation.

---

# PART 11 — HARD TOPICS, CONTESTED CLAIMS, AGING RISK

## Hard modules

**Module 4 (Debugging):** The hardest module to teach and the most
important. The core difficulty: debugging requires tolerating not
knowing — an uncomfortable state that students relieve by either
guessing or asking AI. The phase gate in this module is the hardest
gate in the course. A drafter who has not taught debugging in person
will write this module wrong.

**Module 7 (Polymorphism):** Method dispatch is counterintuitive.
The commonly taught explanation ("the actual type determines which
method runs") is technically correct and pedagogically insufficient.
Requires a worked example where the student predicts incorrectly
before understanding.

**Module 10–11 (GUI/Events):** JavaFX has steep environmental setup
friction. Module 10 requires version-specific setup instructions
that change annually. Highest aging risk in the course.

## Contested claims

| Claim | Status | Book's position |
|---|---|---|
| AI makes programming education obsolete | Disputed | "AI requires programming understanding — you can't verify what you don't understand" |
| OO design is outdated | Disputed | Functional and OO are both taught; OO is the course's primary paradigm for business modeling |
| Students should use AI from day one | Disputed | Act One establishes understanding before assistance; this is not anti-AI, it is pre-AI |
| Testing is optional for course projects | Disputed in practice | Module 13 makes testing required and explains why |

## Aging risk summary

| Content type | Risk | Review cadence |
|---|---|---|
| JavaFX setup instructions | High | Before each offering |
| Specific AI tool references (Claude, Copilot) | High | Before each offering |
| CLAUDE.md format | Medium | Before each offering |
| Java syntax content | Low | On major Java version changes |
| OO design principles | None | Stable |
| Debugging methodology | None | Stable |

---

# PART 12 — MARKET POSITIONING SUMMARY

**The gap this book fills:** No course textbook for a graduate
first-programming course teaches Java OO engineering AND the AI
collaboration discipline simultaneously, with a single project
threading all modules and explicit phase gates at every AI boundary.

**Market size estimate:**
INFO 5100 / EDGE (Coursera) is the primary adoption. Secondary:
other MS programs requiring an application development course —
estimated 50–100 additional adoptions per year at steady state.
Kindle format lowers adoption friction relative to print textbooks.

---

# PART 13 — FEATURE LIST SUMMARY

| Feature | Priority | Notes |
|---|---|---|
| 14-module architecture | ESSENTIAL | — |
| Single business problem thread | ESSENTIAL | Domains A/B/C |
| HOW TO USE AI section per module | ESSENTIAL | Core thesis delivery |
| CLAUDE.md per module | ESSENTIAL | Progressive constraint system |
| AI Use Disclosure form | ESSENTIAL | Assessment enforcement |
| Lab assignments (14) | ESSENTIAL | — |
| Final project spec | ESSENTIAL | — |
| Module 0 setup appendix | ESSENTIAL | — |
| CLAUDE.md appendix (How to Use Claude for Java) | IMPORTANT | Synthesis of all 14 CLAUDE.mds |
| CLI Quick Reference per module | IMPORTANT | — |
| Domain B/C parallel exercises | IMPORTANT | |
| Instructor manual | IMPORTANT* | Required for non-author adoption |
| Kindle-optimized formatting | IMPORTANT | Code blocks, navigation |
| Exercise bank (beyond lab assignments) | VALUABLE | — |
| Video walkthroughs (lab setup) | ASPIRATIONAL | — |

*Instructor manual is ESSENTIAL for adoption by any faculty member
who is not the author.

---

# PART 14 — OUT OF SCOPE

Permanently excluded (no reopen condition without structural revision):

| Topic | Reason |
|---|---|
| Spring / Spring Boot | Enterprise frameworks require OO mastery as prerequisite — second course material |
| Databases and SQL | Covered in adjacent INFO courses; CSV persistence sufficient for this course |
| Android development | Deployment target too different from the course's GUI focus |
| Web development (servlets, REST) | Second course material |
| Design patterns (Gang of Four) | Named patterns introduced informally; formal treatment is graduate-level OO follow-on |
| Concurrency beyond introductory | Module 14 introduces threads conceptually; deep concurrency is second course |
| Kotlin or other JVM languages | Java only; language-switching distracts from OO design focus |
| Advanced AI topics (LLMs, APIs) | AI tools are used; AI internals are not covered |

All exclusions acknowledged in Module 0 with pointers to follow-on courses.

---

# PART 15 — ADOPTION RISK REGISTER

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| 1 | JavaFX setup friction derails Module 10 | High | High | Module 0 appendix; verified setup scripts |
| 2 | Students use AI to bypass Act One entirely | High | High | AI Use Disclosure; lab design requires handwritten code |
| 3 | CLAUDE.md format changes between editions | Medium | Medium | CLAUDE.md appendix is updateable without chapter revision |
| 4 | Instructor reluctance to enforce AI gate | Medium | High | Requires instructor manual with enforcement guidance |
| 5 | Domain A (library) feels dated to some students | Low | Low | Domains B/C available; domain choice at Module 1 |
| 6 | Java version changes break code examples | Low | Medium | Version-pinned examples; annual review |
| **7** | **No instructor manual at launch** | **High** | **High** | **BLOCKER for non-author adoption — prioritize** |

---

# PART 16 — OPEN QUESTIONS

| # | Question | Stakes | Decision deadline | Owner |
|---|---|---|---|---|
| 1 | Kindle formatting for code blocks — what is the best practice for long Java snippets in Kindle? | Reader experience; accessibility | Before manuscript | Author |
| 2 | Should CLAUDE.md examples use Claude-specific syntax or be tool-agnostic? | Longevity; adoption across AI tool landscape | Before Module 1 draft | Author |
| 3 | How are Domain B/C exercises developed — author or volunteer contributors? | Production timeline | Before manuscript drafting | Author |
| 4 | Instructor manual: separate volume or integrated? | Production planning; pricing | Before proposal | Publisher |
| 5 | AI Use Disclosure form: standardized across the series (Irreducibly Human) or course-specific? | Series coherence | Before Module 1 draft | Author + series editor |
| 6 | Assessment weights: do the EDGE/Coursera gradebook weights match the book's stated weights exactly? | Adoption alignment | Before course launch | Author + EDGE team |

---

*Full TOC Draft v1.0 — compiled from all phase inputs*
*All phases complete: Vision (i1–i4), Learning Architecture (l1–l3),*
*Chapter Architecture (c1–c4), Scope & Market (m1–m4)*
*One high-priority blocker before adoption by non-author faculty: Risk 7 (instructor manual)*
*Research-ready: pass the chapter research prompt against this file*
