# Module 14 — Lists, Stacks, Queues and the Final Project: Further Reading

> **Content note:** Despite its title, this module's primary content is not data structures — it covers professional software handoff, five-layer architecture, AI use disclosure, and the verification habit. The data structures listed in the course outline appear only in the assessment list; the chapter's argument is about what "done" means and how to defend what you built. The resources below address that actual content.

This chapter defines professional completion — running code, navigable source, tests as evidence, AI disclosure, and a defended design — but it does not teach you how to argue a design decision under examination pressure, or what the verification habit looks like in professional practice beyond a semester project. These resources close that gap: they give you the vocabulary and models for articulating trade-offs, for understanding what layered architecture actually buys you at scale, and for developing the AI collaboration discipline the chapter introduces into a transferable professional skill.

Read the Key resource before drafting your final defense — it gives you a concrete structure for the trade-off reasoning the chapter describes but does not model in detail. Choose one Recommended resource based on where you feel least prepared: the first if your architecture explanation feels thin, the second if the AI disclosure requirement raised questions you haven't resolved. The Further item is for students who want to understand why the verification habit matters beyond this course; it is not required, and most students should complete the final project before attempting it.

---

### Key

**The Pragmatic Programmer: Your Journey to Mastery, 20th Anniversary Edition** — David Thomas and Andrew Hunt, 2019 (Addison-Wesley)

I included this because the chapter's strong-defense format — alternatives considered, cost and gain of each, what your specific requirements made one choice better — is exactly the reasoning this book develops across a career, and reading a concentrated version of it now will make your defense more precise. Read Topic 37, "Listen to Your Lizard Brain" (pages 199–208) and Topic 45, "The Requirements Pit" (pages 235–245); together they cover how to articulate what a requirement actually demands and why "it's standard practice" is never a sufficient defense. Then read the "Tracer Bullets" topic (Topic 12, pages 50–58) for the layered-architecture rationale the chapter assumes but does not argue: the idea that each layer should be independently demonstrable before the next is added is the book's explanation of why the five-layer build order this course followed was not arbitrary. Plan for 60–90 minutes across these three topics. Available through O'Reilly Learning and most university libraries; the 20th anniversary edition (2019) is the current version and is significantly revised from the first.

---

### Recommended

**A Philosophy of Software Design** — John Ousterhout, 2018 (Yaknyam Press)

I included this because the chapter asks you to explain why your layers are designed as they are — what each layer is for, what its boundary is, and what it protects the layers above from knowing — and Ousterhout's framework gives you the clearest vocabulary for that explanation I know of. Read Chapter 4, "Modules Should Be Deep" (pages 22–37) and Chapter 8, "Pull Complexity Downwards" (pages 60–67). These two chapters provide the conceptual grounding for why the event handlers in your project should not implement checkout logic (that complexity belongs lower), and why the view layer should not own model state. When the examiner asks "why did you design it this way?" and your honest answer is "the tutorial put it there," these chapters give you the retrospective reasoning to replace that answer with a defensible one. Read actively: as you go through each principle, pause and apply it to one layer in your own project before continuing. Available in print and through many university libraries; also sold directly from the author's website.

**"An Empirical Study of the Effectiveness of Automated and Human Code Review"** — not included due to verification uncertainty. In its place: **Clean Code: A Handbook of Agile Software Craftsmanship** — Robert C. Martin, 2008 (Prentice Hall)

I included this because the chapter's criterion for "done" source code — readable, organized, navigable by someone who was not in the room — maps directly to what this book teaches, and Chapter 1, "Clean Code" (pages 1–24) contains short expert statements about what readable code actually means that are worth reading before you submit. Focus on Chapter 2, "Meaningful Names" (pages 17–30) and Chapter 3, "Functions" (pages 31–52): these are the specific craft dimensions that a code reviewer will notice first, and they are the places where AI-generated code is most likely to be technically correct but professionally weak — long methods, generic variable names, logic that works but cannot be read. Read Chapter 2 and Chapter 3 before your final submission and use them as a checklist: if a name in your codebase would require a comment to explain, rename it. Available through O'Reilly Learning and most university libraries.

---

### Further

**"Explainability and Auditability in ML: Definitions, Tools, and Emerging Systems"** — this specific survey could not be verified with confidence. In its place: **The Software Craftsman: Professionalism, Pragmatism, Pride** — Sandro Mancuso, 2014 (Prentice Hall)

This is a professional-orientation resource, not an introductory one. It assumes you have already shipped working code and felt the gap between "it runs" and "I would be comfortable showing this to a senior engineer" — if you have not had that experience yet, this book will be more useful to you six months after the final project than before it. The prerequisite is completing the course: the payoff is that Mancuso articulates the professional identity dimension that the chapter introduces but does not develop — what it means to take ownership of code quality as a career stance rather than a course requirement. Specifically, Chapter 3, "Software Craftsmanship" (pages 21–36) and Chapter 5, "Heroes, Goodwill, and Professionalism" (pages 57–72) directly extend the chapter's verification habit argument: they explain why engineers who cannot explain their systems stop growing, and what the alternative looks like in a professional context. What the Recommended tier gives you is vocabulary and structure; this book gives you a model of what a career built on that vocabulary looks like. Available through O'Reilly Learning and most university libraries; also widely available in print.

---

> **Assessment connection:** The Key resource (The Pragmatic Programmer, Topics 12, 37, and 45) directly supports the Final GUI Application Project defense requirement — specifically Exercise 6, which asks you to write out three design decisions in the strong format (alternatives, costs and gains, requirements context, what would change) and identify where your understanding is incomplete. The "Requirements Pit" and "Tracer Bullets" topics give you the professional framework for doing that analysis before the examiner asks the questions aloud.
