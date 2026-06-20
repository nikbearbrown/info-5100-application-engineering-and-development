# Module 4 — Basics of Object-Oriented Programming Part 2: Further Reading

This chapter teaches debugging as causal diagnosis — forming a hypothesis before touching a line of code, isolating evidence with a breakpoint, and tracing from symptom to root cause. What it does not cover is how to apply that workflow at scale: programs with multiple interacting classes, bugs that cross method boundaries, and the design choices that make bugs structurally harder to introduce in the first place. These resources extend the hypothesis-isolate-test loop to those professional contexts and give you the cognitive vocabulary to talk about what you are doing when you debug.

Read the Key resource before Exercise 4 or the lab submission — it directly supports writing the hypothesis and root-cause explanation the exercise requires. Choose one Recommended resource based on where your understanding feels shakiest: pick the Zeller if you want a more rigorous treatment of the hypothesis loop itself, pick the Sedgewick if you want to see the same debugging discipline applied inside well-structured Java code. You do not need to read both. The Further item is optional and takes roughly two hours; skip it unless you are curious about the research behind why developers debug the way they do.

### Key

**Effective Java, Third Edition** — Joshua Bloch, 2018 (Addison-Wesley)
*Scope: Item 17 ("Minimize mutability") and Item 15 ("Minimize the accessibility of classes and members"), pages 80–93 and 73–80.*
I included this because the chapter's bridge question — "how do you design a system with fewer hidden bugs?" — is exactly what these two items answer. Item 17 explains why shared mutable state is the structural source of sequence-dependent bugs like the one in the library checkout exercise: when objects can be modified after creation and their references can be shared across methods, a field can silently hold a stale or wrong value with no announcement. Item 15 shows the access-control mechanism that limits how widely a field can be reached. Read Item 17 first, then Item 15. After reading, return to the checkout bug you diagnosed in this module and identify which of the two design principles, if applied to `currentPatron`, would have made the bug structurally impossible rather than merely detectable. This is the thinking Exercise 9 (Challenge) asks you to make explicit before Module 5.

### Recommended

**Why Programs Fail: A Guide to Systematic Debugging** — Andreas Zeller, 2nd ed., 2009 (Morgan Kaufmann)
*Scope: Chapter 2 ("Tracking the Problem"), pages 17–42.*
This chapter by Zeller formalizes the hypothesize-isolate-test workflow this module teaches informally. Where the module names three steps, Zeller names the same loop as the "scientific method applied to debugging" and works through the conditions under which a hypothesis is well-formed versus a restatement of the symptom — the distinction Exercise 1 tests directly. Read pages 17–30 carefully (the conceptual argument), then skim pages 30–42 (the tool discussion, which uses a different debugger than NetBeans but the principles transfer). After reading, compare Zeller's definition of a "failure" versus a "defect" to the module's symptom/root-cause distinction and write one sentence on whether they are equivalent. The book is available through most university library systems.

**Introduction to Programming Using Java, 9th Edition** — David J. Eck, 2022 (free online at math.hws.edu/javanotes)
*Scope: Section 3.3 ("Introduction to Error Handling") and Section 4.3 ("Parameters, Variables, and Scope"), pages 113–122 and 145–154 in the PDF.*
I included this because the chapter assumes you can read a reference chain — follow a variable from one method into another and identify where its value changes — but does not systematically explain how Java passes object references versus primitive values. Eck's Section 4.3 explains that mechanism from first principles, which is the prerequisite for forming a correct hypothesis about a bug that crosses method boundaries. Read Section 4.3 first; if the explanation of pass-by-value for references is not yet solid, this is the gap to close before the lab. The resource is freely available online, no login required.

### Further

**Debugging: The 9 Indispensable Rules for Finding Even the Most Elusive Software and Hardware Problems** — David J. Agans, 2002 (AMACOM)
*Scope: Chapters 1–5 ("Understand the System" through "Change One Thing at a Time"), pages 1–108.*
*Level note: This is a practitioner-level book written for working engineers, not a textbook. It assumes you have already formed and tested at least a few hypotheses on real programs and felt the difference between guessing and diagnosing.* Prerequisites: you should be comfortable with the module's full three-step loop — not just knowing what a breakpoint is, but having used it to confirm or refute a hypothesis at least once. The payoff over the Recommended tier is scope: Zeller formalizes the logic; Agans illustrates the psychological failure modes that cause experienced developers to abandon the logic under pressure (the "it should work" trap, the "I just changed one thing" rationalization, the "let's just try this" reflex that this module teaches you to resist). If you read this after the lab — after you have a real debugging session to reflect on — Chapters 3 and 5 in particular will map directly onto moments in your own session where you almost stopped forming hypotheses and started guessing. Widely available in print; some library systems carry it electronically.

---

> **Assessment connection:** The Key resource (Bloch, *Effective Java*, Item 17) directly supports Exercise 9 (Challenge), which asks you to name at least one Java language feature or design pattern that would make sequence-dependent bugs structurally impossible and explain the mechanism. Item 17's argument for immutability is one correct answer to that question, and reading it before writing your response will let you test your current thinking against a practitioner-level treatment rather than reasoning from scratch.
