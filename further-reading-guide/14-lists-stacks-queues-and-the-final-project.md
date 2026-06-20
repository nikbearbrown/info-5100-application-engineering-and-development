## Further Reading — Lists, Stacks, Queues, and the Final Project

> **Content note:** Despite the title "Lists, Stacks, Queues, and the Final Project," this chapter's primary content is not data structures. It covers professional software handoff, five-layer architecture, AI use disclosure and audit, and the verification habit. The data structures named in the course outline appear only in the assessment list; the chapter's argument is about what "done" means and how to defend what you built. This guide addresses the actual chapter content.

This chapter defines professional completion — running code, navigable source, tests as evidence, AI disclosure, and a defended design — but it does not teach you how to argue a design decision under examination pressure, or what the verification habit looks like beyond a semester project. Those are live debates in professional practice: what counts as sufficient evidence that code is correct, who is responsible for AI-generated decisions, and what separates an architecture that survives requirement changes from one that does not. These resources give you vocabulary and models for all three.

Read the Key resource before drafting your final defense — it provides the concrete trade-off reasoning structure the chapter describes. For Recommended, choose the first if your architecture explanation feels thin, the second if you want a craft-level checklist before submission. The Further item is for students who want to understand the professional identity argument the chapter implies but does not make; it is not required, and most students will get more from it after completing the project than before.

---

### Key

**The Pragmatic Programmer: Your Journey to Mastery, 20th Anniversary Edition** — David Thomas and Andrew Hunt, 2019 | ISBN 978-0135957059 | Available through O'Reilly Learning and most university libraries.

I included this because the chapter's strong-defense format — alternatives considered, cost and gain of each, what your specific requirements made one choice better — is exactly the reasoning this book develops, and reading a concentrated version of it now will make your defense more precise. Read Topic 37, "Listen to Your Lizard Brain," and Topic 45, "The Requirements Pit"; together they cover how to articulate what a requirement actually demands and why "it's standard practice" is never a sufficient defense. Then read Topic 12, "Tracer Bullets," for the layered-architecture rationale the chapter assumes but does not argue: the idea that each layer should be independently demonstrable before the next is added is the book's explanation of why the five-layer build order this course followed was not arbitrary. Plan for 60–90 minutes across these three topics. The 20th anniversary edition (2019) is significantly revised from the first and is the current version.

> Supports: Final GUI Application Project defense — specifically Exercise 6, which asks you to write out three design decisions in the strong format (alternatives, costs and gains, requirements context, what would change) and identify where your understanding is incomplete.

---

### Recommended

**A Philosophy of Software Design** — John Ousterhout, 2018 | ISBN 978-1732102200 | Available in print and through many university libraries; also sold directly from the author's website at web.stanford.edu/~ouster/cgi-bin/book.php.

I included this because the chapter asks you to explain why your layers are designed as they are — what each layer is for, what its boundary is, and what it protects the layers above from knowing — and Ousterhout's framework gives you the clearest vocabulary for that explanation. Read Chapter 4, "Modules Should Be Deep," and Chapter 8, "Pull Complexity Downwards." These two chapters provide the conceptual grounding for why the event handlers in your project should not implement checkout logic — that complexity belongs lower — and why the view layer should not own model state. When the examiner asks "why did you design it this way?" and your honest answer is "the tutorial put it there," these chapters give you the retrospective reasoning to replace that answer with a defensible one. Read actively: as you work through each principle, pause and apply it to one layer in your own project before continuing.

**Clean Code: A Handbook of Agile Software Craftsmanship** — Robert C. Martin, 2008 | ISBN 978-0132350884 | Available through O'Reilly Learning and most university libraries.

I included this because the chapter's criterion for "done" source code — readable, organized, navigable by someone who was not in the room — maps directly to what this book teaches, and the relevant chapters are short enough to use as a pre-submission checklist. Focus on Chapter 2, "Meaningful Names," and Chapter 3, "Functions": these are the specific craft dimensions a code reviewer will notice first, and they are the places where AI-generated code is most likely to be technically correct but professionally weak — long methods, generic variable names, logic that works but cannot be read. Use this as a literal checklist before your final submission: if a name in your codebase would require a comment to explain, rename it. Read Chapters 2 and 3 in sequence; the rest of the book extends the same principles and can be returned to after the course.

---

### Further

**The Software Craftsman: Professionalism, Pragmatism, Pride** — Sandro Mancuso, 2014 | ISBN 978-0134052502 | Available through O'Reilly Learning and most university libraries.

This is specialist professional-orientation literature, not a student text, and it is written for practitioners who have already shipped working code and felt the gap between "it runs" and "I would be comfortable showing this to a senior engineer." If you have not had that experience yet, this book will reward you more six months after the final project than the week before it. The prerequisite is completing the course with the verification habit the chapter describes already internalized — without that foundation, Mancuso's arguments will feel abstract rather than recognizable. What the Recommended tier gives you is vocabulary and structure for the design conversation; this book gives you a model of what a career built on that vocabulary looks like in practice. Chapter 3, "Software Craftsmanship," and Chapter 5, "Heroes, Goodwill, and Professionalism," directly extend the chapter's AI audit and verification arguments into a professional identity frame — they explain why engineers who cannot explain their systems stop growing, and what the alternative looks like across a career, not just a semester.
