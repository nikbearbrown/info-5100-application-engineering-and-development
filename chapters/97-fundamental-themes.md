# Appendix: Fundamental Themes

*These are not rules. They are the shape of the thinking the course has been building.*

---

A course about Java is not really about Java. Java is the material — the particular language whose compiler enforces certain things and permits others, whose runtime behaves in ways we can trace and predict, whose library gives us specific tools with specific contracts. But the course uses Java to build something harder to name and harder to test: a way of thinking about programs as systems of responsibility, about correctness as something you must argue for rather than assume, about tools — including AI tools — as things that extend your capability without replacing your judgment.

The themes in this appendix are not review. They are the architecture underneath the syntax. If you absorbed only the Java, you learned to operate a language. If you absorbed these, you learned to think like an engineer.

---

## You Cannot Verify What You Do Not Understand

This is the hardest theme and the most important one, so I want to start with what it is not saying.

It is not saying that you must understand everything before you use it. That would make all software development impossible. Every program uses libraries whose implementation you have not read, runs on hardware whose circuitry you could not trace, depends on operating system behavior whose source you have never opened. Understanding is always partial. The question is whether your partial understanding is sufficient for the verification task you are responsible for.

What the theme is saying is this: when you accept a component — a class, a method, a piece of AI-generated code — as part of your system, you inherit responsibility for its behavior in your context. You cannot discharge that responsibility by pointing to the source of the component. "AI wrote it" is not a verification. "It compiled" is not a verification. "It ran once and produced the right output" is barely a verification. Verification means you can explain what the component does, why it does it that way, what inputs produce what outputs, and what happens when the assumptions underlying the design are violated.

Here is the specific failure mode the course is designed to prevent. A student receives AI-generated code for a checkout method. The code compiles. The demo works. The student does not fully understand why the loop terminates in the edge case, or what happens when the patron reference is null, or whether the list being modified is the original or a copy. The student does not know these things, but the code looks correct, and looking correct is reassuring.

Then the edge case arrives. The null reference appears. The copy-vs-original distinction matters. The code fails in a way the student cannot diagnose because the mental model they needed to diagnose it was never built. The AI produced output. The student accepted output. Nobody built the model.

The discipline the course teaches is the discipline of closing that gap: not refusing to use AI, but refusing to accept output as a substitute for understanding. Every module asks the student to trace, explain, and defend the code they submit — not because the instructor doubts the code, but because the ability to trace, explain, and defend is the understanding. It is not a test of understanding. It is the understanding itself.

---

## Objects Model Responsibilities

The object model is not a Java peculiarity. It is a way of carving up the problem.

Every business system is made of entities with identity — this patron, not patrons in general; this book, not books in general — with state that belongs to that entity, and with behavior that operates on that state. The object-oriented design move is to make that structure explicit in code: not to store patron data in a list somewhere and borrow-limit logic in a procedure somewhere else, but to put both inside the `Patron` class, where the logic can enforce the limit on the data it directly controls.

The key word is *responsibility*. A class is not a convenient organizational unit for related functions. It is a statement about what one kind of thing knows, what one kind of thing can do, and what one kind of thing must never be asked to do. A `Book` knows its title and availability. It can be checked out and returned. It must not know about the GUI. A `Patron` knows its name and borrowed-books list. It can borrow and return books, enforcing its own limits. It must not know about the persistence layer.

These "must nots" are as important as the "knows" and "cans." When a class absorbs responsibilities it should not hold, the design degrades in a specific way: the class becomes load-bearing structure for decisions it was never designed to carry. A `Book` that knows what color to display its title in cannot be used in a headless context. A `Patron` that calls the database directly cannot be tested without a running database. The responsibilities that should have lived elsewhere are now locked inside an object that will have to be modified every time those external concerns change.

The practical discipline is the question you ask before writing any method: whose responsibility is this? Not "where is it convenient to put this" but "what object owns this knowledge and this behavior?" If the answer is unclear, it is often because the design has not yet named an entity that should own it — which is a design problem to solve, not a hint to pick a convenient home.

---

## Debugging Is Causal Reasoning

A debugger is a tool for seeing intermediate state. It is not a replacement for a theory.

The mistake most developers make when debugging is beginning with the output. The output is wrong. They look at the output. They look at the code near where the output is produced. They change something. They run again. If the output changes in the right direction, they feel progress. If it does not, they change something else.

This is not debugging. This is search with worse odds than a coin flip, because the changes are not random — they are influenced by the wrong mental model that produced the bug in the first place.

Debugging begins with a hypothesis. A hypothesis is a falsifiable claim about the state of the program at a specific point in execution. Not "something is wrong with the checkout" but "the `currentPatron` reference holds the wrong object at the point of assignment, because the reference was not reset between transactions." That claim names an object, a field, a moment, and a mechanism. It can be checked with a breakpoint and an inspection. It can be confirmed or refuted.

The hypothesis forces a crucial move: you must form a model of the program's causal structure before you can form a hypothesis about where it breaks. Where does this data come from? What methods touch it? What are the possible paths from initialization to the point of failure? This is reading code as a causal system — not as syntax, not as intent, but as a sequence of state transformations whose actual behavior can diverge from intended behavior at specific points.

When the hypothesis is confirmed, you have found the proximate cause. The deeper question is: what made this divergence possible? A reference that was supposed to be temporary was shared. A precondition was assumed rather than enforced. A method modified state it should have read. The root cause is upstream, often far from the symptom. Following the causal chain from symptom to proximate cause to root cause is the intellectual work of debugging. The debugger provides the evidence. The reasoning provides the path.

AI can help with both parts. It can explain error messages accurately. It can suggest what kind of root cause produces a given symptom. What AI cannot do is hold your specific program's causal model in its head — because AI does not know your specific program the way you do after having built it module by module. The hypothesis must come from you.

---

## AI Use Requires Phase Gates

The course does not prohibit AI. It structures AI use by the student's current verification capacity.

This structure is not arbitrary. It follows from the first theme: you cannot verify what you do not understand. In the early modules, the student does not yet have the vocabulary, the mental models, or the debugging capacity to verify AI-generated Java for correctness, let alone for design quality. Permitting unrestricted AI use at that stage would produce correct-looking code whose correctness the student cannot assess. The student would submit it, the demo would work, and the understanding that is the real deliverable of the module would not exist.

So the early modules permit AI for explanation — understanding what code does — while requiring the student to write new code themselves. As the student builds vocabulary and verification capacity, the boundary shifts. Later modules permit AI for scaffolding, then for candidate implementations that the student evaluates and revises. The final modules permit collaboration: AI as a thinking partner for design questions the student has enough background to evaluate.

The logic is the same as any apprenticeship. A carpenter's apprentice does not start on the client's furniture. They start on practice joints, where the stakes of failure are low and the learning is high. They earn the right to do more consequential work by demonstrating that they can evaluate their own work — that they know what good looks like and can recognize when they have produced it. Unrestricted delegation from day one would skip the stage where the student builds that evaluative capacity, which is the stage that matters.

The phase gates in this course are that apprenticeship structure made explicit. Each module states exactly what AI may do and what the student must do themselves. The constraint is not about distrust of AI. It is about the sequence in which skills must be built so that AI can eventually be used at full power, with the judgment to know when it is right and when it is not.

---

## The Project Is One System

This theme is the one most likely to seem obvious and be violated.

The semester project is not fourteen sequential labs. It is one application, built in fourteen increments. Every design decision made in Module 2 is still present in Module 14. Every weak boundary, every shortcut, every class that absorbed responsibilities it should not have — those decisions compound over the life of the project in ways that feel invisible until they are not.

Here is what compounding looks like. A student designs the `Patron` class in Module 2 to hold a list of book titles instead of `Book` references, because it seemed simpler at the time. In Module 4, they debug a problem where the patron's list and the library's catalog are out of sync after a return — which is traceable directly to the string-vs-reference decision. In Module 8, they implement persistence and discover that the title-based approach forces them to do a string-lookup on every load, which is slow and breaks when title strings are inconsistent. In Module 10, they try to display the patron's borrowed books in the GUI and discover that they cannot get availability status from a title string without querying the catalog again. The decision compounds at every layer.

The inverse is also true. A student who designs `Patron` correctly in Module 2 — with `Book` references, with a `borrow()` method that enforces the limit, with clear responsibility boundaries — finds that Module 4's debugging is about something else, Module 8's persistence is straightforward, and Module 10's GUI wires up cleanly. Good design compounds as well as bad.

This is why the modules do not ask "does the lab work?" as the primary question. They ask "can you explain the design choice and trace its implications?" Because the lab working is local evidence. The design choice is what travels through every subsequent module.

---

## Tests Are Evidence, Not Magic

A passing test proves one thing: on this specific setup, with these specific inputs, the method produced output that matched the stated requirement, at the time the test was run.

That is a real claim. It is not a small claim. Before the test existed, the claim was unverifiable without running the program manually and checking by hand. After the test exists, the claim is verifiable automatically, by anyone, at any point in the future. The test has externalized a judgment that was previously internal and ephemeral. That is genuine progress.

But the claim is limited in specific ways that matter. A passing test does not mean the method handles all inputs correctly — only the inputs the test supplied. It does not mean the method handles the same inputs correctly after the surrounding code changes — only that it handled them correctly when the test was written. It does not mean the method's behavior is correct in the full system — only that the method's behavior is correct in the isolated setup the test creates.

These limits are not arguments against testing. They are arguments for thinking carefully about what you are testing and what you are leaving untested. The five-case taxonomy — normal, empty, no-match, boundary, invalid input — is a heuristic for covering the cases where implementations most commonly fail. It is not a proof that all cases are covered. No finite set of tests can be.

The more durable value of tests is not the individual passing tests. It is the regression barrier they create over time. Every test that existed before a change is a claim that existed before a change. If the change breaks a claim, a test fails. The failure is information: the change touched something that mattered. Without the test, the change would have been invisible. The regression would have been discovered at the demo, or after the demo, or not at all.

---

## The Final Defense Is The Point

The final defense is not a presentation. It is a demonstration of ownership.

There is a specific thing the defense reveals that no submission can: whether the student can respond to an unexpected question about their own system. Not a question they prepared for. A question that requires them to trace an unfamiliar path through code they wrote, to explain a design choice they made without having rehearsed the explanation, to identify what AI decided and what they decided and why the distinction matters.

This is not a performance. It is a probe. The course's thesis is that a student who built the system module by module, who traced every behavior back to a requirement, who debugged by forming hypotheses rather than by guessing, who accepted AI output only after verifying it against their own understanding — that student can answer questions they have not practiced, because the understanding is theirs. The system is theirs.

The student who assembled the system from AI-generated components without building the underlying model has a different experience of the defense. The code looks the same. The running application may be identical. But the questions surface the gap between the appearance of ownership and the thing itself.

This is not a trap. The defense is not designed to catch people out. It is designed to make visible what is otherwise invisible: whether the understanding exists. Every module in the course was building toward this. The checkpoints, the AI use disclosures, the verification requirements, the requirement to trace behavior to artifacts — those were all practice for the defense. Practice for the moment when you have to say, without notes, without AI, without rehearsal: here is what this does, here is why I built it this way, here is what I would change if the requirement changed, here is what I know and here is what I still do not fully understand.

The last sentence is the Feynman test. If you can say "here is what I still do not fully understand" with specificity — naming the thing, naming why it is hard, naming what you would need to learn to resolve it — you understand the rest well enough. Vague confidence is the mark of the student who has not looked carefully. Specific uncertainty is the mark of the student who has.

---

These seven themes are not a checklist to complete. They are habits of mind that compound over time, the way good design decisions compound over the life of a project. They are available to you now because you have spent a semester applying them — sometimes well, sometimes poorly, sometimes without recognizing that you were applying them at all.

The Java will change. The frameworks will change. AI tools will change faster than either. The habits are the durable thing. Take them.
