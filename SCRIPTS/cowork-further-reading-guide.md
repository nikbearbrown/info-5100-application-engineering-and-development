# Further Reading Guide — Design Guidelines

Guidelines for writing Further Reading Guides that accompany textbook chapters
or course modules. Based on research in instructional design, library science,
OER development, and reading motivation. Empirical findings are distinguished
from practitioner consensus where the evidence allows.

Two assessment rounds on 13 generated guides identified recurring failures that
have been incorporated into these guidelines as explicit rules.

---

## What a Further Reading Guide Is

A further reading guide is a curated, annotated set of resources that extends
a chapter's learning beyond what the main text covers. It is not a bibliography
(which records sources used), not a reference list (which supports claims made),
and not a syllabus reading list (which is required). It is an invitation to go
deeper — and it must earn that engagement rather than assume it.

A further reading guide is distinct from an annotated bibliography. An
annotated bibliography is an academic task: a researcher demonstrating mastery
of a literature. A further reading guide is an instructional tool: an
instructor building a scaffold for a student who has not yet mastered the
field. The tone, structure, and selection logic are different in every
dimension.

Reading lists — and further reading guides as a sub-type — are not neutral
appendices. Katharine Schucan Bird's 2020 article in Higher Education describes
them as "representation devices": they shape what students think matters, how
they allocate effort, and which voices and knowledge traditions are made visible.
A guide composed entirely of works by one demographic, institution, or decade is
not just a diversity gap — it is a claim about whose work counts. This means
curation is always a value-laden act, and designers should treat it as one.

Empirical data on engagement is instructive. A large-scale RLMS evaluation at
the University of Huddersfield found that 76.6% of students used reading lists
"a lot" or "sometimes," and 87.4% rated them useful — but 32% of students
requested better curation, and 61% demanded digital formats over print. The gap
between perceived usefulness and actual engagement closes when guides are
annotated, connected to assessments, and written with framing that explains why
each resource was chosen. A guide without annotation is almost always ignored.

One counterintuitive finding: students often regard supplementary reading guides
as more important for their learning than lecturers do (Brewerton, 2014). Some
students were unsure how to use reading lists; others were unaware they existed.
**Discoverability and usage clarity are quality criteria**, not just content
quality. A guide that is not easy to find, or that does not tell students how
to use it, has failed before a student reads the first entry.

---

## When Not to Write a Further Reading Guide

Do not create a further reading guide if:
- The chapter's learning objectives are fully met by the main text and
  exercises — a guide that adds nothing signals that reading further is noise
- You cannot verify that resources are accessible to all students (paywalled
  with no institutional access, broken links, non-accessible formats)
- You are filling space rather than extending a genuine knowledge gap
- The module is a welcome module, orientation unit, midterm exam, or appendix
  with no substantive content to extend — writing a guide for one of these
  produces a guide whose only function is to signal that every module has one

For modules where the chapter title does not match the chapter's actual
content (see §Title-Content Drift below), do not write a guide for the title —
write it for what the chapter actually teaches.

---

## Title-Content Drift

Some chapters carry titles inherited from a course outline or syllabus that no
longer matches what the chapter actually covers. This is not a further reading
guide problem — it is an upstream problem. The correct fix is to rename the
chapter. A content mismatch notice inside the further reading guide is a
temporary patch, not a solution.

**Rule:** If the chapter title and the chapter content are substantially
different, include a content mismatch notice in the guide. Use this format:

> **Content note:** Despite the title "[module title]," this chapter covers
> [actual content]. This guide addresses the actual chapter content.

Apply a low threshold: if the chapter's primary concept is not what the title
names, add the notice. When in doubt, add it.

**Do not omit the notice because the mismatch is "obvious."** A student
arriving via a course outline labeled "Recursion" and finding a guide about
JavaFX injection needs that orientation sentence. The notice costs one line.
Missing it costs the student their orientation.

**Log title-content mismatches** for upstream repair. Content notes in guides
should be treated as a queue of chapter renames that need to happen, not as
permanent features of the guide.

---

## Integration and Publication

A further reading guide that is not visible in the student's workflow does not
exist pedagogically. This is the single most underestimated quality criterion.

**Integrate into the book build or LMS, not as standalone files.** Guides
stored as isolated files that do not appear in the compiled textbook, the LMS
course navigation, or the weekly module structure are not read. The split-
attention effect (CLT) applies at the course level: students who must switch
context to find a resource lose momentum and often abandon the search.

**Minimum viable integration:**
- If the textbook is a compiled document: include the guide as a section at the
  end of each chapter, not as a separate file that must be navigated to
  independently
- If the textbook uses an LMS: embed the guide inside the weekly module, not in
  a separate "Resources" folder at the course level
- If both: do both

**Publish before the semester begins**, not the week of the chapter. Students
who need alternative formats (large print, screen-reader-compatible PDFs, audio)
need lead time to request them. Publishing early also allows students to begin
reading before the week it is formally assigned — which matters for students
managing heavier course loads.

**Check visibility** as part of the pre-semester review: can a student who has
never seen the course find the guide in under two clicks from the module page?

---

## Structure

### Three-Tier Priority System

Organize every guide into exactly three tiers. Label them explicitly. Students
need to know which items are load-bearing and which are exploratory.

| Tier | Label | Purpose | Bloom's Level | Quantity |
|------|-------|---------|--------------|----------|
| 1 | **Key** | Directly supports meeting core learning outcomes; skipping it leaves a gap | Remember / Understand | 1–2 items |
| 2 | **Recommended** | Extends and deepens the chapter's main concept; worth reading before a project | Apply / Analyze | 2–3 items |
| 3 | **Further** | Exploratory, stretch, or professional orientation | Evaluate / Create | 1–2 items |

The Bloom's column is a design constraint, not a label to print. Key resources
must be accessible to a student who just finished the chapter. Further resources
may challenge and can assume more background — but that must be stated.

**Do not exceed 3–5 total resources per module.** Lists beyond this trigger
avoidance (Cognitive Load Theory). Fewer, better-chosen resources consistently
outperform comprehensive lists.

### Designing for two lanes

A well-designed guide implicitly serves two types of students: those who need
reinforcement (confidence-building lane: Key + Recommended) and those ready for
specialist work (stretch lane: Further). Without labeling the stretch lane
explicitly, a difficult Further-tier resource is not read as "this is optional
and hard" — it is read as "this whole guide is not for me," and the student
abandons the entire guide. Label it explicitly. State the prerequisite and the
payoff before the annotation begins.

### Organization within tiers

Five schemes have support in the literature:

| Scheme | Best for | Evidence strength |
|--------|----------|------------------|
| Core vs. optional extension | Any guide; gives permission not to read everything | Strong |
| By subtopic | Chapters covering multiple conceptual branches | Strong |
| By week / session | Guides feeding seminar or lab preparation | Strongest empirical support |
| By level (intro / intermediate / specialist) | Heterogeneous cohorts | Instructional-design logic |
| By function (overview / theory / debate / methods / primary source) | Advanced modules | Practitioner-supported |

Do not organize by resource type without thematic grouping inside each type.
That structure forces students to make relevance judgments the guide should
already have made.

**Label consistency is a quality criterion.** Siddall's empirical work shows
that terms like "core," "recommended," and "background" fail when instructors
define them differently across modules. Students wanted a common standard.
Whatever labels you choose, define them once in the course introduction and
apply them identically everywhere.

---

## Framing Text

The guide's opening determines whether a student reads on or closes the tab.
Gain-framed language ("this will expand your ability to...") outperforms
loss-framed language ("failure to read this will result in...") for optional
materials. Write a narrative opening of 100–150 words — not a bullet list, not
a sentence. It must do two distinct things:

### 1. Motivate

Name the knowledge gap the chapter left open and what the student gains from
closing it. Frame the discipline as alive — present it as an ongoing
conversation, not a settled body of facts. Students who believe a field is
static have no reason to read further.

Do not write: "The following resources provide additional information on the
topics covered in this chapter." This sentence creates no motivation.

Do not use the word "optional" without explaining the gain. Students read
"optional" as "skip this."

### 2. Instruct

Tell students how to use the guide: what each tier means and what they are
expected to do. Should they read only the Key item? All core items? Choose one
Recommended item based on their project focus? Students who cannot answer
"what am I supposed to do with this?" default to not starting.

Example:

> "Read the Key resource before the project milestone. Choose one Recommended
> resource based on which concept you found least clear in the chapter. The
> Further item is for students who want to go beyond the project requirement —
> it assumes familiarity with [X] and will take about 90 minutes."

Motivation and usage instruction are different jobs. Both must be present.

---

## Annotation

Every resource must have an annotation. A bare citation is functionally
equivalent to no citation — students have no basis for deciding whether to
engage with it.

### Three required elements

Each annotation must address all three in this order:

1. **Ontological value** — What is this resource's contribution, and where does
   it sit in the broader conversation? Foundational, contested, recently revised?
   This gives the student context before they start reading.

2. **Pedagogical connection** — How does it connect to the chapter's concepts
   or assessments? "Chapter 3, pages 44–61, directly extends the authentication
   model in Module 6" is a connection. "This is useful" is not. Name the
   specific concept, exercise, or assessment it supports.

3. **Strategic guidance (directional scaffolding)** — What should the student
   do with this resource? "Review Section 2 for methodology, focus on Section 5
   for the findings" is strategic guidance. "Read this carefully" is not.
   Students who receive no reading strategy skip resources that require more
   than a skim.

### Further tier: three additional required elements

Every Further-tier annotation must also include:

4. **Level note** — Explicit statement of difficulty: "This is specialist
   literature written for practitioners, not a student text." Do not embed
   this in prose — make it visually identifiable so students scanning for
   difficulty signals can find it.

5. **Prerequisite** — What the student must already understand before this
   resource rewards them. "Assumes you are comfortable with [named concept]"
   is a prerequisite. "Some background in X" is too vague to be actionable.

6. **Payoff** — What specifically does this give that the Recommended tier
   does not? A student who skips the Further item must know what they are
   trading away.

These three elements should be woven into a cohesive annotation, not formatted
as three separate labeled paragraphs. Fragmenting the annotation into "**Level
note:**", "**Prerequisite:**", "**Payoff:**" blocks makes the resource count
ambiguous (readers mistake the labels for additional resources) and reads as
a form, not prose. The information must be there; the labels are optional.

### Presentation: one cohesive unit

Present the citation, annotation, and access information as a single visual
unit. Never separate the citation from its annotation with a section break,
blank line, or different page. CLT's split-attention effect degrades learning
when students must mentally integrate information distributed across space.

### Length

100–150 words per annotation is the empirically grounded target. A JMIR Medical
Informatics study (2024) found human-written annotations average 90 words and
score significantly higher on readability than AI-generated annotations (Flesch
score 15.3 vs. 5.76). Concise, readable annotations outperform longer denser
ones. Go up to 200 words only when the resource requires a conceptual buffer
(a dense empirical paper with specialist vocabulary) — and in that case include
a glossary of key terms.

Quality test: an annotation that could describe a different resource equally
well has failed. Removing the resource title should still leave a reader
knowing exactly what was recommended.

### Voice

Write in first person where the instructor chose the resource. "I included this
because the chapter skips the failure-mode analysis this article covers in
detail." First-person framing signals intentional curation and distinguishes
human judgment from automated output.

### Over-scaffolding risk

Annotations can over-scaffold. Piscioneri and Hlavac's "Minimalist Reading
Model" was valued by many students but criticized by others as "dumbing down"
the material. The aim is to give a point of entry — not to pre-digest the
source. A good annotation says: here is the door, here is where to start. It
does not walk the student through every room.

---

## Draft Discipline: What Never Appears in Student-Facing Output

When drafting guides with AI assistance or under uncertainty, editors
sometimes leave process notes in the output. These must be removed before
publication. The following phrases are draft metadata — they are useful during
generation and harmful in the final guide:

- "not included due to verification uncertainty"
- "could not be verified with confidence"
- "originally planned resource was replaced"
- "this citation requires further checking"
- "In its place: [title]"

If a resource was replaced because it could not be verified, the final guide
should show only the replacement resource — with no trace of the discarded one.
Students reading a course guide should not encounter evidence of the editorial
process. Exposing it suggests the guide's resources are unreliable and
undermines trust in the entire set.

**Rule:** The output format permits exactly one entry per resource. Each entry
begins with the exact title of the resource being recommended. Nothing else.

---

## Resource Selection Criteria

Apply in order. A resource failing an earlier criterion is excluded regardless
of how well it satisfies later ones.

### 1. Real and verifiable

This criterion is first because AI-assisted compilation regularly produces
hallucinated citations. Every resource must be independently confirmable through
a library catalog, DOI resolver, or publisher database before inclusion.

Before including any resource:
- Confirm the title is exact (not a plausible-sounding variation)
- Confirm the author(s) actually wrote this work (not a different work in the
  same area)
- Confirm the publication year and venue exist
- For books: confirm the chapter/page reference against the actual edition
- For articles: confirm the DOI resolves to the cited paper

If you cannot confirm a resource, flag it and use a different one. Do not
include a resource that has not been verified. Do not include uncertain
resources with a disclaimer ("this citation may need checking") — that is draft
metadata, not a guide entry.

Page numbers cited for books must be verified against the actual edition.
Different editions have different pagination. Citing page ranges from the
wrong edition is a factual error. If the edition cannot be confirmed, omit the
page range and name the section or chapter title instead — section titles are
stable across editions; page numbers are not.

### 2. Accessible to all students

Verify before adding:
- Paywalled: confirm institutional subscription access and provide a direct
  link; if uncertain, state "available via institutional library access" rather
  than a bare URL that may not work for all students
- Online: test the URL; use a DOI rather than a raw URL wherever one exists
- Multimedia: confirm captions, transcripts, or text alternatives exist
- PDF: confirm it is screen-reader compatible (not a scanned image of pages)

Resources that are inaccessible to students with disabilities, limited internet
access, or no print budget reproduce inequality regardless of their intellectual
quality.

### 3. Stable and citable

Prefer resources with persistent identifiers: DOIs for academic content, ISBNs
for books, official institutional URLs for documentation. For web resources
without DOIs, use Perma.cc to create a permanent snapshot URL, or provide a
Wayback Machine archive link.

Distinguish two failure modes:
- **Link rot**: the URL returns a 404 error — the resource is gone
- **Reference rot**: the URL resolves but the content has changed — the page
  cited no longer shows what it was cited for

Perma.cc addresses both by capturing the page at the moment of citation.
The Wayback Machine (web.archive.org) addresses link rot retrospectively.
For live web resources cited going forward, Perma.cc is preferred.

A 2022 study analyzing 2,500 peer-reviewed articles found 36% of hyperlinks
broken and 37% of DOIs inactive over ten years. Link rot is worse than most
instructors assume. Plan for it at the time of writing, not after links break.

### 4. Right level for the tier

Key and Recommended resources must be accessible to a student who just
finished the chapter. Further resources may assume more background — but that
must be stated in the annotation (level note + prerequisite).

Do not place a graduate-level paper in the Key tier because it is canonical.
Canonical does not mean accessible. Pair every canonical source with an
accessible secondary companion and explain the pairing.

### 5. Specific, not general

A resource covering twenty topics is a second textbook, not a further reading
resource. Prefer a resource covering one concept deeply over one surveying many
shallowly. If a book is recommended, name the chapter or page range. If a video
is recommended, name the timestamp range.

Version specificity matters: cite the edition you verified, and name whether
a newer edition exists. If citing a book, state whether the cited chapter
exists in the edition students are likely to find. If citing a documentation
page, note the version (e.g., "Java 21 documentation" vs. "Java 8 tutorial").
Version inconsistencies — citing a Java 8 URL in a course that uses Java 21 —
erode student trust even when the underlying content is similar.

### 6. Current

For most fields, prefer resources published within the last 10 years. For
fast-moving fields (STEM, computing, medicine), prefer within 5 years. If a
dated resource is irreplaceable (a foundational design paper, a primary source),
explain why no current alternative exists and note what has changed since
publication.

### 7. Open access — with realistic expectations

Prioritize open-access or library-licensed resources when quality is comparable.
Access barriers reliably reduce actual use: a paywalled resource is
pedagogically worthless if students cannot retrieve it.

However: Tlili et al.'s 2023 meta-analysis found a statistically significant
but negligible effect of OER on learning achievement. Open access removes
barriers but is not itself a learning intervention. "This is open access" is
not a quality argument; it is an access argument. When quality is comparable,
prefer open.

### 8. Diverse voices

Review the full guide's author list before publishing. A list drawn exclusively
from one demographic, institution, or decade is a representation claim about
whose work counts. Actively include authors from underrepresented backgrounds
as a standard of quality, not as a compliance exercise.

### 9. Use primary sources for disciplinary inquiry

For humanities, social science, and professional fields: primary sources
(original documents, archival materials, legal texts, historical records) have
distinctive value that secondary literature cannot substitute. Ithaka S+R's
research and Library of Congress guidance both find that primary sources promote
inquiry, critical thinking, and historical reasoning in ways that second-hand
summary does not. Where the chapter teaches students to think like practitioners
in a discipline, a primary source gives them something real to do that thinking
with.

### 10. Consider student-authored materials

For introductory modules, high-quality undergraduate research articles,
peer-vetted OER summaries, or annotated student projects can outperform
professional publications. Beginning students often identify what other
beginners need more accurately than experts do. Student-authored materials
also signal academic belonging — students see themselves as capable of
producing the kind of work the discipline values.

---

## Resource Type Mix

Mix formats when each type serves a different learning goal. Do not diversify
for cosmetic variety.

**Use text (books, articles) for:**
- Building precise conceptual vocabulary
- Understanding the argument structure behind a design decision
- Following a chain of reasoning step by step

**Use visual resources (diagrams, infographics) for:**
- Showing relationships between concepts hard to describe in prose
- Representing processes with multiple simultaneous steps

**Use multimedia (video, podcasts, interactive tools) for:**
- Demonstrating dynamic behavior (code execution, algorithm animation)
- Providing a second explanation from a different voice
- Building motivation before a difficult section

Prefer videos that show, animate, or demonstrate over videos that read text
aloud. Mayer's redundancy principle: on-screen text competes with narration for
the verbal channel. Narration + visuals outperforms narration + text.

Practical composition target (practitioner consensus, not empirical):
60–70% text, 20–30% visual, 10% multimedia — adjusted per discipline.

---

## Connection to Assessment

Reading guides not connected to assessments are used by 17–27% of students.
This is the single highest-leverage design decision: connecting at least one
resource to a near-term graded or structured task.

Low-stakes guided reading questions tied to supplementary resources
significantly increase compliance (Holbrook & Cassell, 2024). Carl Wieman's
research shows pre-class reading rises sharply when tied to visible payoff —
not threat of consequence, but the removal of "why bother?"

Minimum viable connections:
- **Key tier**: at least one resource tied to a specific concept, exercise, or
  discussion prompt the student is working on now. Name it explicitly.
- **Further tier**: align at least one stretch resource to a graded assignment,
  essay, or project milestone. Students engage with challenging resources when
  the payoff is visible and named.

Name the connection in the guide, not in the course description. "This resource
will help you answer Question 3 on the lab submission" is an explicit connection.
"Further reading supports learning outcomes" is not.

---

## Digital and OER-Specific Requirements

- **Integrate into the build pipeline**, not standalone files. Guides that do
  not appear in the compiled textbook or LMS module navigation are not read
  (see §Integration and Publication).

- **Use DOIs** for all academic content. A DOI resolves to the current location
  even when publishers reorganize. Check that cited DOIs are active — a 2022
  study found 37% of DOIs inactive over ten years.

- **Use Perma.cc or Wayback Machine** for web resources without DOIs. Perma.cc
  captures the page at citation time (protects against both link rot and
  reference rot). Wayback Machine provides retrospective rescue. Prefer Perma.cc
  when creating new citations.

- **Embed in LMS workflow** inside the weekly module, not in a separate
  resources folder. Reading guides embedded in the course flow are used more
  than guides stored in appendices or separate folders.

- **Deploy social annotation** where possible. Tools like Hypothesis and
  Perusall let students annotate and discuss supplementary readings directly in
  the text. Engagement becomes visible to the instructor; isolation of
  asynchronous reading is reduced.

- **Meet WCAG 2.1 AA** accessibility standards for materials you create. For
  externally hosted resources, note known accessibility limitations in the
  annotation.

- **Normalize typography** before publication. Mojibake artifacts (â€", â€™,
  etc.) appear when UTF-8 content is processed without correct encoding. Run
  encoding verification as part of the pre-publication review, not after. These
  artifacts break screen readers and undermine the guide's credibility.

- **Review semi-annually**: check all links, confirm resources are current and
  accessible, update or remove outdated items before each term.

### Open pedagogy

In OER contexts, consider involving successive student cohorts in building and
annotating the guide. Students adding multicultural resources, writing
collaborative annotations, and flagging outdated materials produce guides more
effective for introductory learners than instructor-authored guides alone —
because beginning students identify what other beginners need more accurately
than experts do. Apply the same verification and quality standards to student
contributions as to instructor contributions.

---

## AI Assistance

### What the empirical record shows

A JMIR Medical Informatics study (2024) compared human annotators against
ChatGPT 3.5, 4, and 5:

| Metric | Human | AI | Implication |
|--------|-------|----|-------------|
| Mean annotation length | 90 words | 113 words | AI writes longer but less readable |
| Flesch Reading Ease | 15.3 | 5.76 | Human annotations significantly more readable |
| Capture of main points | Baseline | Comparable | AI can summarize topics adequately |
| Factual error rate | Low | High | AI has significantly higher hallucination rate |
| Quality/context summary | Inconsistent | High | AI over-summarizes quality it cannot assess |

Hallucination is well-documented across independent studies: Walters (2023,
Scientific Reports), Chelli et al. (2024), Linardon et al. (2025), and Nature
(2026) all document citation fabrication and reference inaccuracy at scale.
This is structural, not a prompting problem.

### Documented failure modes

- **Citation hallucinations**: fabricated titles, authors, publishers, DOIs,
  and page ranges that appear plausible but do not exist
- **Page number errors**: incorrect page citations for real books — common when
  the model was trained on one edition and generates numbers for another
- **Misrepresented significance**: LLMs cannot reliably distinguish foundational
  from contested from marginal work
- **Voice mismatch**: dense, passive, formulaic language that students find
  harder to read and less compelling than human writing
- **Draft metadata leakage**: AI may insert uncertainty disclosures
  ("this citation needs verification") that must never appear in student-facing
  output

### Best-practice workflow

1. **Prime the model** with exemplar annotations before asking for output
2. **Use targeted prompts** specifying section, word count, and what to check
3. **Verify every item**: title, author, publication year/venue, page range,
   DOI — against the source itself, not another LLM
4. **Remove all draft metadata** before publication
5. **Disclose** if AI was used in any capacity — modeling responsible AI use
   is itself a learning outcome in any contemporary course

---

## Common Failures and How to Avoid Them

| Failure | Cause | Fix |
|---------|-------|-----|
| Guide is never opened | No assessment connection, no annotation | Tie Key tier to a named concept task; tie Further tier to a graded milestone |
| Links break mid-semester | Raw URLs, no persistent identifiers | Use DOIs; Perma.cc for web resources |
| Students feel overwhelmed | More than 5 total resources | Cut to highest-value per tier; never exceed 5 |
| Guide is too generic | Annotations describe any resource in the field | Rewrite until removing the title still identifies the resource |
| Wrong level in Key tier | Canonical source placed without accessible pairing | Pair every canonical source with an accessible secondary companion |
| Outdated materials | No review schedule | Semi-annual review before each term |
| Homogeneous authorship | Default to historical canon | Audit author list for diversity before publishing |
| Paywalled resources | Not verified through institutional library | Confirm access for every paywalled item; prefer open or library-licensed |
| Guide signals "read everything" | No explicit permission to skip | Define core vs. optional; give explicit permission not to read the Further tier |
| Students don't know guide exists | Published late or buried in navigation | Publish pre-semester; integrate into compiled book or LMS module |
| Labels inconsistent across chapters | No shared definition | Define categories once in course introduction; apply identically everywhere |
| Draft metadata in student-facing output | Process notes not removed | Final editorial pass removes all "not included due to..." language |
| Mojibake/encoding artifacts | UTF-8 not enforced through pipeline | Run encoding verification before publication |
| Content mismatch not noticed | Title accepted at face value | Check first three paragraphs against title; low threshold for adding notice |
| Version inconsistencies (Java 8 URLs in Java 21 course) | Resources not version-checked | Confirm all documentation URLs match course's actual runtime version |
| AI page citation errors | AI hallucinates page numbers for real books | Verify page ranges against physical or library copy of the actual edition |
| Guide not in compiled book | Files written but not integrated into build | Integrate further-reading-guide/ files into book build or copy into chapters |

---

## Editing Pass

Before publishing a further reading guide, verify all of these:

**Structure**
1. Are all three tiers present (Key / Recommended / Further)?
2. Is total resource count 3–5?
3. Key: 1–2 items. Recommended: 2–3 items. Further: 1–2 items.

**Framing text**
4. Is the framing text 100–150 words, narrative (not bullet list), and
   gain-framed (not obligation-framed)?
5. Does it frame the discipline as alive — current debate, not settled facts?
6. Does it define the tier labels and tell students exactly what to read and
   how to choose?
7. Does it give explicit permission not to read everything?
8. Does it include a content mismatch notice if the chapter title diverges from
   actual content? (Low threshold — when in doubt, add it.)

**Annotations**
9. Does every annotation include ontological value, pedagogical connection,
   and strategic guidance?
10. Is every annotation 100–150 words? (200 maximum for stretch resources
    requiring a conceptual buffer.)
11. Does every annotation name a specific chapter, page range, or timestamp —
    not just a title?
12. Are citations, annotations, and access links presented as one cohesive
    visual unit, not split across sections?
13. Could any annotation apply equally well to a different resource? If yes,
    rewrite it.

**Further tier**
14. Does the Further tier annotation include a level note, prerequisite, and
    payoff — woven into cohesive prose, not three labeled paragraphs?
15. Could a student who is not ready set the Further resource aside without
    concluding the whole guide is not for them?

**Access and identifiers**
16. Does every resource have a DOI, ISBN, or archive URL (Perma.cc / Wayback
    Machine)? At minimum, a verified URL plus an explicit note about how to
    access it through the institutional library.
17. Are all cited URLs version-consistent with the course's actual runtime,
    framework, or library version?
18. Have all page numbers been verified against the actual edition of the book?

**Assessment connection**
19. Is at least one Key-tier resource tied to a specific named concept,
    exercise, or discussion prompt?
20. Is at least one Further-tier resource tied to a specific graded assignment
    or project milestone?

**Quality and trust**
21. Has every AI-generated citation been independently verified against the
    original source?
22. Does the guide contain any draft metadata ("not included due to...",
    "could not be verified...", "In its place:", etc.)? If yes, remove before
    publishing.
23. Does the author list reflect disciplinary diversity?

**Publication readiness**
24. Is the guide integrated into the compiled book or LMS module (not just a
    standalone file)?
25. Is it published early enough for students needing alternative formats to
    request them?
26. Has encoding been verified (no mojibake artifacts: â€", â€™, etc.)?
27. Is a semi-annual review date calendared?

---

## Output Format

```markdown
## Further Reading — [Chapter/Module Title]

[100–150 word narrative framing. Paragraph 1: what knowledge gap the chapter
left open, framed as a living debate or open question — not a list of topics.
Paragraph 2 (or final sentences): tell students what each tier means and what
they are expected to do. Give explicit permission to skip the Further tier.]

### Key

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation: (1) what this resource contributes and where it
sits in the field; (2) which specific concept, exercise, or assessment it
directly supports and how; (3) which section to focus on and what reading
strategy to use. One cohesive unit — citation, annotation, and link together.]

> Supports: [specific named concept question, exercise, or project task]

### Recommended

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation with the same three elements.]

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation.]

### Further

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation. Includes, woven into prose: (a) explicit level
note stating difficulty and audience; (b) named prerequisite — what the
student must already understand; (c) specific payoff — what this gives
that Recommended does not. Do not use separate "Level note:" / "Prerequisite:"
/ "Payoff:" labels that fragment the annotation — weave them in.]

> Supports: [specific graded assignment, essay prompt, or project milestone]
```
