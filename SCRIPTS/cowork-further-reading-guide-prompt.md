# Further Reading Guide Generation Prompt

Use this prompt to generate a Further Reading Guide for any textbook chapter
or course module. Paste the chapter text after the final line.

A Further Reading Guide is not a bibliography, not a reference list, and not
a syllabus reading list. It is a curated, annotated set of resources that
extends a chapter's learning beyond what the main text covers — organized by
priority tier, connected to learning outcomes, and written to earn engagement
rather than assume it.

---

## BEFORE YOU BEGIN — FOUR RULES THAT OVERRIDE EVERYTHING ELSE

**Rule 1 — Verify before including.**
Every resource you name must be real and independently confirmable: exact
title, exact author(s), exact publication year and venue. Do not include a
resource you cannot confirm exists. If uncertain, use a different resource.
Do not write "this citation needs checking" — that is draft metadata, not a
guide entry. If you cannot verify it, exclude it silently and choose something
you can verify.

**Rule 2 — No draft metadata in the output.**
The following phrases must never appear in the final guide:
"not included due to verification uncertainty" · "could not be verified" ·
"originally planned resource was replaced" · "In its place:" ·
"this citation requires further checking."
These are editorial process notes. Students must never see them. The output
contains only the resources being recommended, each starting with the exact
resource title.

**Rule 3 — Page numbers must match the actual edition cited.**
Do not cite page ranges from memory or inference. If you can confirm a page
range against the actual edition, include it. If you cannot, name the section
or chapter title instead — section titles are stable across editions; page
numbers are not. A wrong page number is a factual error that sends students
to the wrong place.

**Rule 4 — Version consistency.**
If the chapter uses Java 21, cite Java 21 documentation. If the chapter uses
JavaFX 21, cite JavaFX 21 documentation. Do not cite Java 8 or JavaFX 2
documentation for a Java 21 course, even if the underlying behavior is similar.
Version inconsistencies erode student trust.

---

## STEP 0 — ALIGNMENT CHECK

Read the chapter title and the first three paragraphs of the chapter body.

**Ask:** Does the chapter's actual content match its title?

Apply a low threshold — if the chapter's primary concept is not what the title
names, add the following notice immediately after the guide title, as the first
element of the output:

> **Content note:** Despite the title "[module title]," this chapter covers
> [actual content]. This guide addresses the actual chapter content.

**Do not skip this check.** Missing a content mismatch notice leaves students
who arrived expecting the titled topic disoriented about what they are reading.

---

## STEP 1 — IDENTIFY THE CHAPTER'S KNOWLEDGE GAPS

Before selecting any resources, extract:

1. **Learning objectives** — what the student must be able to do after the
   chapter. State as actions ("distinguish X from Y in a running program"),
   not topics ("understand X").

2. **Implicit limits** — what does the chapter touch but not explain? What does
   it name without defining? What does it assume without justifying? These
   create the guide's most important resources.

3. **Practical extension** — what would a student applying this professionally
   need to know that the chapter does not teach?

4. **Conceptual depth** — what would a student who wants to understand the
   underlying theory need to read?

Do not begin selecting resources until all four are named. Resources chosen
before this analysis tend to reflect the author's knowledge rather than the
student's gaps.

---

## STEP 2 — SELECT RESOURCES

Select **4–6 total resources** across three tiers. Do not exceed 6.

### Tier 1 — Key (1–2 resources)
Directly supports meeting the chapter's core learning objective. A student
who skips this has a meaningful gap. Must be accessible to a student who
just finished the chapter. No graduate-level or specialist material here.

### Tier 2 — Recommended (2–3 resources)
Extends and deepens the chapter's main concept. Worth reading before a project
or the next module. May require slightly more background than the Key resource.

### Tier 3 — Further (1–2 resources)
This is the stretch lane: exploratory, specialist, or professional orientation.
May be genuinely challenging. Must be explicitly marked as such — see annotation
rules below. Intended for students who want to go beyond the project requirement.

Without explicit labeling, a difficult Further resource is not read as
"this is optional and hard" — it is read as "this guide is not for me," and
the student abandons the entire guide.

### Resource selection checklist

Before including any resource:

- [ ] **Real and verifiable** — title, author(s), year, publication all
  confirmed. Not inferred, not paraphrased, not a similar title. If uncertain,
  exclude it and choose something you can confirm.

- [ ] **Accessible** — not paywalled without institutional access; URL loads
  and is current; format is accessible (not a scanned PDF). If paywalled, note
  "available via institutional library access."

- [ ] **Specific** — if a book, name the chapter or section title (and page
  range only if confirmed against the actual edition). If a video, name the
  timestamp range.

- [ ] **Version-consistent** — documentation, tutorials, and API references
  must match the course's actual runtime and framework version.

- [ ] **Current** — for STEM fields, prefer resources within the last 5–10
  years unless the foundational text has no current equivalent.

- [ ] **Right level for the tier** — Key and Recommended must be accessible
  to a student who just finished the chapter.

---

## STEP 3 — WRITE THE GUIDE

### Opening framing (100–150 words, narrative prose — not bullet points)

The framing does two distinct jobs. Both are required.

**Job 1 — Motivate.**
Name the knowledge gap the chapter left open. Frame it as a living debate or
open question, not a list of topics. Students who believe a field is settled
have no reason to read further. Be gain-framed ("this will let you..."), not
obligation-framed ("you should also...").

Do not write: "The following resources provide additional information on the
topics covered in this chapter."

**Job 2 — Instruct.**
Tell students what each tier means and what they are expected to do. Should
they read only the Key item? Choose one Recommended resource based on their
project angle? The Further item is for whom? Students who cannot answer "what
am I supposed to do with this?" default to skipping the guide.

Give explicit permission not to read everything. A guide that implies total
coverage is required will be abandoned by most students.

Example of good instruction:
> "Read the Key resource before the project milestone. Choose one Recommended
> resource based on which concept felt least clear. The Further item is for
> students who want to go beyond the requirement — it assumes familiarity with
> [prerequisite] and takes about 90 minutes."

### For each resource, write an annotation (100–150 words)

Every annotation must contain all three of these, in this order:

1. **Ontological value** — what this resource contributes to the field and
   where it sits in the broader conversation. Is it foundational, contested,
   a recent revision? Context before content.

2. **Pedagogical connection** — how it connects specifically to this chapter's
   concepts or assessments. Name the concept, exercise, or lab it supports.
   "This is useful" is not a pedagogical connection.

3. **Strategic guidance** — what the student should do with this resource.
   Which section to focus on. How to read it (skim / read deeply / compare to
   textbook / watch only first 8 minutes). Students who receive no reading
   strategy skip resources that require more than a surface skim.

**Quality test:** Could this annotation describe a different resource equally
well? If yes, rewrite it. The annotation must be specific enough that removing
the resource title still identifies what was recommended.

**Voice:** First person. "I included this because the chapter skips the
failure-mode analysis this article covers." First-person framing signals
intentional curation, not automated output.

### Further tier annotation — additional requirements

The Further tier annotation must also convey three additional things, woven
into the annotation as cohesive prose:

- **Level note**: who this is written for and how difficult it is ("this is
  specialist literature written for practitioners, not a student text")
- **Prerequisite**: what the student must already understand before this
  resource rewards them — name the specific concept, not "some background in X"
- **Payoff**: what specifically this gives that the Recommended tier does not

Do NOT format these as three separate labeled paragraphs with "**Level note:**",
"**Prerequisite:**", "**Payoff:**" headers. That fragments the annotation, makes
the resource count ambiguous, and reads as a form, not prose. Weave them in.

### Access information

Every resource entry must include one of: DOI · ISBN · stable institutional URL
· Perma.cc archived URL · Wayback Machine backup URL. A bare title with no
access path is incomplete. If the resource is a print book with no DOI, include
the ISBN and note "available via institutional library."

### Assessment connection

For the Key-tier resource, add a single line naming the specific concept,
exercise, or project task this resource directly supports:

> Supports: [name the specific lab, exercise, assessment, or project task]

---

## STEP 4 — EDITING PASS

Before finalizing, check every item:

**Structure**
1. Are all three tiers present?
2. Is total resource count 4–6?
3. Key: 1–2. Recommended: 2–3. Further: 1–2.

**Content mismatch**
4. Is there a content mismatch notice if the chapter title diverges from
   actual content? (Low threshold — when in doubt, add it.)

**Framing**
5. Is the framing 100–150 words of narrative prose (not a bullet list)?
6. Does it name the knowledge gap as a living debate, not a topic list?
7. Does it tell students what to read and how to choose?
8. Does it give explicit permission not to read everything?

**Annotations**
9. Does every annotation have ontological value, pedagogical connection, and
   strategic guidance?
10. Is every annotation 100–150 words? (200 max for stretch resources only.)
11. Does every annotation name a specific section, chapter, or timestamp —
    not just "this book covers X"?
12. Could any annotation describe a different resource equally well? If yes,
    rewrite it.
13. Is the citation, annotation, and access info presented as one cohesive
    unit per resource?

**Further tier**
14. Does the Further annotation convey level, prerequisite, and payoff — as
    woven prose, not three labeled paragraphs?
15. Could a student not ready for the Further resource set it aside without
    concluding the whole guide is not for them?

**Access and identifiers**
16. Does every resource have a DOI, ISBN, or archive/stable URL?
17. Are all documentation URLs version-consistent with the course?
18. Are all page numbers verified against the actual cited edition? (If not
    confirmed, use section/chapter title instead.)

**Assessment connection**
19. Does the Key tier have an explicit "Supports:" line naming a specific
    task or exercise?

**Draft hygiene**
20. Does the guide contain any of the following? If yes, remove before
    outputting: "not included due to...", "could not be verified", "In its
    place:", "this citation needs checking", "originally planned resource."
    These are never student-facing.

---

## OUTPUT FORMAT

```markdown
## Further Reading — [Chapter/Module Title]

[Content mismatch notice — add if title diverges from content. Low threshold.]

[100–150 word narrative framing. First: name the knowledge gap as a living
debate or open question. Then: tell students exactly what to read and how to
choose. Give explicit permission to skip the Further tier.]

### Key

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation: (1) what it contributes and where it sits in the
field; (2) which specific exercise or concept it supports and how; (3) which
section to focus on and what reading strategy to use.]

> Supports: [specific named exercise, lab, concept question, or project task]

### Recommended

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation with all three elements.]

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation with all three elements.]

### Further

**[Exact resource title]** — [Author(s), Year] | [DOI / ISBN / archive URL]
[100–150 word annotation. Weave in (without using labeled paragraph headers):
who it is written for and how hard it is; what the student must already
understand before it rewards them (specific named concept); what specifically
it gives that the Recommended tier does not.]
```

---

## CHAPTER TO TRANSFORM:

[paste chapter text here]
