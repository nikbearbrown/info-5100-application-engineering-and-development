# Appendix: Claude Code for Java

This appendix is a rough working guide for using Claude Code in INFO 5100. It is meant to travel with every module. Keep it open while you work.

Claude Code is powerful because it can work inside a codebase. It can read files, search files, suggest edits, make edits, and run commands when you permit it. That is exactly why this course treats it carefully. A tool that can change your project can help you move faster. It can also help you create code you cannot explain.

The rule for the course is simple:

> Claude Code may help only after you have enough understanding to verify what comes back.

If you cannot explain the requirement, trace the behavior, test the result, or reject a plausible wrong answer, you are using Claude Code too early.

## What Claude Code Is For In This Course

Use Claude Code as a tutor, reviewer, scaffold builder, and second reader. Do not use it as the engineer of record.

Good uses:

- Explain a Java error message after you paste the exact text.
- Ask quiz questions about a class you already wrote.
- Generate layout or controller scaffolding after you supply the design.
- Suggest debugging hypotheses after you state your own first.
- Review a class for responsibility leaks.
- Suggest test cases after you describe intended behavior.
- Find inconsistencies across files before the final project defense.

Bad uses:

- "Write the assignment for me."
- "Fix this bug" before you have a hypothesis.
- "Design my classes" before you have named what each class knows and does.
- "Generate my authentication system" before you have stated the threat model.
- "Make the GUI work" before you can trace model state to view state.
- "Write my tests" before you know what behavior the tests should prove.

Claude Code can reduce friction. It cannot remove your responsibility.

## The Three Things You Must Write Before Asking

Before you ask Claude Code for help, write three short statements:

1. **Requirement:** What should the program do?
2. **Artifact:** Where should that behavior live? Name the class, method, handler, file, test, or FXML element.
3. **Evidence:** What would prove the answer is acceptable?

Example:

```text
Requirement: A patron can check out an available book.
Artifact: CheckoutTransaction.process() changes Book.available and Patron.borrowedBooks.
Evidence: After checkout, the book is unavailable, the patron list contains the book,
and a second checkout attempt fails with a clear message.
```

Now Claude Code has something to work against. Without those three statements, it will guess. The guess may be fluent. That is the danger.

<!-- → [TABLE: Claude Code readiness checklist — columns: item, question to answer, example answer, what happens if missing; rows: requirement, artifact, evidence, current module phase gate, forbidden AI action, verification method.] -->

## Project Setup

Claude Code uses project context. In a real project, that context can include a `CLAUDE.md` file, settings, and optional custom commands.

A simple course project may eventually look like this:

```text
my-info5100-project/
  CLAUDE.md
  .claude/
    settings.json
    commands/
      explain-error.md
      review-class.md
      suggest-tests.md
  src/
    main/
      java/
  test/
    java/
  README.md
```

The exact tool setup may change before the course runs. Follow the current course setup instructions. Treat any installation or command detail in this appendix as something to verify for the current semester. [verify]

## The Course CLAUDE.md

The project `CLAUDE.md` is not a magic shield. It is an instruction file. It tells Claude Code how to behave in this project. A weak file says, "help me with Java." A useful file says what Claude may do, what it may not do, and what evidence the student must produce.

Start with this:

```text
You are assisting a graduate Java student in INFO 5100.

The goal is not to finish the code as quickly as possible.
The goal is to help the student understand, build, debug, test, and defend
their own object-oriented Java application.

Rules:
- Explain before generating.
- Ask for missing requirements instead of guessing.
- Mark every design decision you make.
- Do not silently choose architecture, data structures, security behavior,
  persistence behavior, GUI workflow, or test meaning.
- If you generate code, include what I must verify before accepting it.
- Never let plausible Java substitute for verified Java.
```

Then add the current module's phase gate.

## Phase Gates Across The Course

The course relaxes AI assistance as your verification skill grows.

| Modules | Constraint level | Claude Code may do | You must own |
|---|---|---|---|
| 0-2 | Diagnostic only | Explain errors, quiz you, clarify terms | First code, class structure, object tracing |
| 3-4 | Scaffold and coach | Generate layout skeletons, explain debugging categories | Business behavior, bug hypothesis, root-cause reasoning |
| 5-7 | Design review | Generate stubs from written specs, critique hierarchies | Class boundaries, is-a reasoning, inheritance validity |
| 8-9 | Implementation assist | Generate persistence boilerplate, comparators, collection code | Data-loss decisions, collection choice, access-pattern rationale |
| 10-12 | GUI assist | Generate view scaffolds, FXML/controller stubs, event registration | User workflow, model-view separation, handler responsibility |
| 13-14 | Synthesis assist | Suggest test cases, review inconsistencies, draft documentation | Assertions, final architecture, project-specific Claude rules, defense |

<!-- → [FIGURE: Claude Code phase gate ladder from Module 0 diagnostic-only use through Module 14 full collaboration, with each rung showing what Claude may do and what the student must own.] -->

## Module Rules

### Module 0: Setup

Claude Code may explain setup errors. Before asking, collect:

- operating system
- JDK version
- `javac` version
- NetBeans version
- full error message

Do not let Claude move you to a different IDE or invent a different course version.

### Module 1: Object Model

Claude may explain provided Java code line by line. It may not write new submitted code.

Use:

```text
Explain what this Java code does line by line.
Do not rewrite it.
After explaining, ask me three questions to check whether I understand it.
```

### Module 2: Multiple Objects

Claude may quiz you on a class you already wrote. It may identify possible design issues. It may not write the first class body.

Use:

```text
Here is my Book class.
Ask me five questions that test whether I understand fields, methods,
constructors, and object instances.
Do not rewrite the class.
```

### Module 3: User Interaction

Claude may generate CardLayout or navigation scaffolding only after you provide the screen flow. It may not decide business behavior.

Before asking, write:

```text
Screen 1:
User action:
Object involved:
State before:
State after:
Next screen:
```

### Module 4: Debugging

This is the hardest gate.

Claude may not identify or fix the bug before you state your hypothesis. You must first provide:

- symptom
- suspected cause
- where you isolated it
- evidence from running, tracing, or the debugger

Use:

```text
Symptom: [what I observed]
Hypothesis: [what I think is causing it]
Isolation evidence: [where I checked]

Is this hypothesis plausible?
Do not fix the code yet.
Ask me what evidence I should collect next.
```

### Module 5: Supply-Side Modeling

Claude may generate class stubs only from a written specification.

For each class, write:

```text
Class:
What it knows:
What it does:
What it must not do:
Related classes:
```

Ask Claude to generate stubs with empty method bodies and design-decision comments.

### Module 6: Person And Authentication

Claude must not generate authentication code before you state the threat model.

Write first:

```text
If someone reads my user data file, what can they do?
What should they still not be able to do?
What password information, if any, will be stored?
```

Claude must not generate plaintext password storage.

### Module 7: Polymorphism

Claude may review an inheritance hierarchy only after you write is-a statements.

```text
CheckoutTransaction is a Transaction because...
ReserveTransaction is a Transaction because...
RenewTransaction is a Transaction because...
```

If you cannot finish the sentence, you do not have an inheritance design yet.

### Module 8: CRUD And Persistence

Before Claude generates persistence code, answer:

```text
What happens if the file does not exist?
What happens if a read fails?
What happens if a write fails halfway through?
How much data loss is acceptable?
```

Claude may write CSV boilerplate. You own the data-loss policy.

### Module 9: Collections

Before Claude chooses `List`, `Map`, or `Set`, answer:

```text
What are the three most common operations?
What is the expected size?
Is order required?
Is uniqueness required?
Is lookup by key required?
```

Claude may suggest code only after the access pattern is clear.

### Module 10: JavaFX Views

Claude may generate view code. It may not generate model logic or event-handler behavior.

Require comments like:

```text
DATA SOURCE: This column displays Book.title.
STUDENT VERIFY: Run with real Book objects, not hardcoded strings.
```

### Module 11: Events

Before asking for a handler, write the action sequence:

```text
When the user clicks [button], the application should:
1.
2.
3.
```

Claude should generate a handler that calls separate methods. One action, one method.

### Module 12: Scene Builder And FXML

Claude may generate controller stubs from FXML. It must map every `fx:id` and handler.

Ask:

```text
Here is my FXML.
Generate controller fields and handler stubs only.
For every field, write CONNECTS TO: [fx:id].
For every handler, write TRIGGERED BY: [UI element].
Do not implement handler logic.
```

### Module 13: Testing

Claude may suggest test cases. It should not write the JUnit code before you state intended behavior.

Ask:

```text
Method behavior: [plain-English behavior]
Inputs:
Expected output:
Business rule:

List test cases only.
For each case, name input, expected output, and category:
normal, boundary, error, null, or regression.
Do not write JUnit code.
```

### Module 14: Final Project

You write the final project `CLAUDE.md`. It is assessed. It must be specific to your application.

It must name:

- what Claude may do
- what Claude may not do
- which design decisions you own
- which files or behaviors require special care
- how you will verify every AI-assisted component

## Permissions And Sensitive Files

Claude Code can be configured with project and user settings. Settings can control permissions, tool behavior, environment variables, and file access. In a classroom project, the most important idea is simple: do not give an AI tool access to secrets or files you do not want read.

If your project ever has API keys, credentials, private data, or `.env` files, those files should be denied or excluded according to current Claude Code settings guidance. This course project should not require real secrets.

Student rule:

> If you would not paste the file into a public classroom chat, do not expose it to Claude Code without explicit instructor guidance.

## Custom Slash Commands

Claude Code supports slash commands. You can think of a slash command as a reusable prompt stored in the project.

Useful course commands:

```text
/explain-error
/quiz-class
/review-hypothesis
/review-class-design
/suggest-test-cases
/draft-ai-disclosure
/final-defense-audit
```

Example command file:

```text
.claude/commands/review-hypothesis.md
```

Possible content:

```text
Review my debugging hypothesis.
Do not fix the code.
Tell me whether the hypothesis is plausible,
what evidence would strengthen it,
and what I should inspect next.
```

Use commands to preserve the course gates. Do not create commands that bypass them.

## The Three-Question AI Audit

Before accepting any AI-assisted component, answer:

1. Can I explain what this component does without using Claude's explanation?
2. Can I explain why it is designed this way, including the alternative I rejected?
3. Can I trace the non-trivial behavior to a test, debugger trace, inspection step, or explicit reason it was not tested?

If any answer is no, the component is not ready.

## AI Use Disclosure

Every lab needs a disclosure. Use this template:

```text
I used Claude Code for:

Prompt or command used:

Claude's useful contribution:

What I changed or rejected:

How I verified the accepted part:

One thing I still own:
```

Good disclosure:

```text
I used Claude Code to suggest boundary test cases for Catalog.searchByTitle.
It suggested empty catalog, no match, one match, and multiple matches.
I rejected the null-input behavior because our requirement says null search text
should be treated as an empty string, not as an exception.
I wrote the JUnit tests myself and verified that two failed before I fixed the method.
I still own the search requirement and the interpretation of what counts as a match.
```

Weak disclosure:

```text
I used Claude to help with the code.
```

That is not a disclosure. It is a confession that the process is not visible.

## Final Project Claude File Template

Use this as a starting point, then make it specific.

```text
Project:
Domain:
Main workflow:

Claude may help with:
- explanations of existing code
- scaffolds for view/controller wiring
- suggestions for test cases
- consistency checks across files

Claude may not decide:
- domain model boundaries
- authentication behavior
- data-loss policy
- collection choices
- final architecture
- what counts as satisfying the requirement

For every generated or revised code block, include:
- requirement being addressed
- design assumption
- verification step
- possible failure mode

If my prompt is vague, ask for the missing requirement instead of guessing.
If I ask for a complete solution, give me the smallest scaffold that lets me
do the engineering work myself.
```

## Closing Rule

Claude Code can make the work faster. It cannot make the work yours.

The work becomes yours when you can say:

- this is what I asked for
- this is what came back
- this is what I checked
- this is what I rejected
- this is why the final design is defensible

That is the standard for this course.
