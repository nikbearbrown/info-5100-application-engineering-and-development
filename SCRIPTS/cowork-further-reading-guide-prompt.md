# Further Reading Guide Generation Prompt

Use this prompt to generate a Further Reading Guide for any textbook chapter
or course module. Paste the chapter text after the final line.

A Further Reading Guide is not a bibliography, not a reference list, and not
a syllabus reading list. It is a curated, annotated set of resources that
extends a chapter's learning beyond what the main text covers — organized by
priority tier, connected to learning outcomes, and written to earn engagement
rather than assume it.

**Generation failure modes to avoid:**
- A guide with bare citations and no annotations (functionally equivalent to
  no guide at all)
- A guide with annotations that could describe any resource in the field
  (too generic to be useful)
- Resources that cannot be verified (AI hallucination risk: every title must
  be real, verifiable, and locatable)
- A guide disconnected from the chapter's learning objectives (students have
  no reason to engage)
- More than 6 total resources (cognitive overload; students stop reading)

---

## STEP 0 — IDENTIFY THE CHAPTER'S KNOWLEDGE GAPS

Before selecting any resources, identify what the chapter does NOT cover that
a student who masters this chapter would benefit from knowing.

Read the chapter and extract:

1. **Learning objectives** — what the student must be able to do after the
   chapter. State as actions, not topics.

2. **Implicit limits** — what does the chapter touch but not explain? What does
   it name without defining? What does it assume without justifying?

3. **Practical extension** — what would a student who wants to apply this
   concept professionally need to know that the chapter does not teach?

4. **Conceptual depth** — what would a student who wants to understand the
   underlying theory need to read?

Do not begin selecting resources until all four gaps are named.

---

## STEP 1 — SELECT RESOURCES

Select 4–6 total resources across three tiers. Do not exceed this count.

**Tier 1 — Key (1–2 resources)**
Directly supports meeting the chapter's core learning objective. A student
who skips this has a meaningful gap. Must be accessible to a student who
just finished the chapter. No graduate-level material in this tier.

**Tier 2 — Recommended (2–3 resources)**
Extends and deepens the chapter's main concept. Worth reading before an
exam, project, or the next module. May require slightly more background.

**Tier 3 — Further (1–2 resources)**
Exploratory, stretch, or professional orientation. May be more challenging.
Clearly labeled as such. Intended for students who want to go beyond the
requirement.

### Resource selection checklist

Before including any resource, confirm:

- [ ] **Real and verifiable** — the title, author, and publication exist and
  can be located through a library catalog or DOI resolver. Do not include
  a resource you cannot verify. If uncertain, use a different resource.

- [ ] **Accessible** — not paywalled without institutional access; URL loads;
  accessible format (not a scan). If paywalled, note that institutional
  access is typically available.

- [ ] **Specific** — if a book, name the chapter or page range. If a video,
  name the timestamp range. A resource that covers twenty topics is not a
  further reading resource.

- [ ] **Current** — for STEM fields, prefer resources published within the
  last 5–10 years. If a dated resource is irreplaceable, say why.

- [ ] **Right level for its tier** — Key and Recommended resources must be
  accessible to a student who just finished the chapter.

### Do not use AI to generate citations

LLM-generated resource lists contain hallucinated titles, authors, and
publishers at high rates. Every resource in this guide must be one you can
describe from actual content knowledge or can locate through a search. If you
are uncertain whether a resource exists, flag it and use a different one.

---

## STEP 2 — WRITE THE GUIDE

### Opening framing (2–3 sentences)

Name the knowledge gap this guide addresses that the chapter did not close.
State specifically what the student gains from further reading here. Be honest
about level if the resources are challenging.

**Do not write:** "The following resources provide additional information on
the topics covered in this chapter."

**Do write something like:** "This chapter introduces [concept] as it works in
[narrow context]. These resources extend that foundation to [broader context]
and to the failure modes that appear when [specific condition]. The Key
resource is worth reading before attempting [specific project task]."

### For each resource, write an annotation

Every annotation must include all three of these elements:

1. **Scope** — which specific part of the resource matters for this chapter?
   Name the chapter, section, or timestamp. "Chapter 3, pages 44–61" is scope.
   "This book" is not.

2. **Learning outcome link** — how does this resource support a stated course
   objective? "This deepens the distinction between X and Y introduced in this
   chapter" is a learning outcome link. "This is useful" is not.

3. **Engagement instruction** — what should the student do with this resource?
   Read deeply? Skim? Watch only the first 8 minutes? Compare to the textbook
   treatment? Students who do not know how to engage skip it.

**Length:** 3–7 sentences. Longer (up to 200 words) only when the resource
requires scaffolding to use effectively.

**Voice:** First person where the instructor chose the resource. "I included
this because the chapter skips the failure-mode analysis that this resource
covers." First-person framing signals intentional curation.

**Quality test:** Could this annotation describe a different resource equally
well? If yes, rewrite it. The annotation must be specific enough that removing
the title would still identify what was recommended.

---

## STEP 3 — CONNECT TO ASSESSMENT

Name one wonder question or project task that a Key-tier resource directly
helps answer or accomplish. State it explicitly in the guide so the student
knows why reading this resource matters now.

---

## STEP 4 — EDITING PASS

Before finalizing, check:

1. Does every resource have an annotation with scope, learning outcome link,
   and engagement instruction?
2. Does every annotation name a specific chapter, page range, or timestamp?
3. Is the total resource count between 4 and 6?
4. Is the opening framing gain-framed, specific to this chapter's gap, and
   honest about level?
5. Is at least one Key-tier resource connected to a specific assessment or
   project task?
6. Could any annotation apply equally well to a different resource? If yes,
   rewrite it.
7. Are all resources real and verifiable? Flag any you are uncertain about
   rather than including them.

---

## OUTPUT FORMAT

```markdown
## Further Reading — [Chapter/Module Title]

[2–3 sentence framing: what knowledge gap this guide addresses, what the
student gains, honest level note if needed.]

### Key

**[Exact resource title]** — [Author(s), Year]
[3–7 sentence annotation covering: scope (specific section/timestamp),
learning outcome link, engagement instruction.]

### Recommended

**[Exact resource title]** — [Author(s), Year]
[3–7 sentence annotation.]

**[Exact resource title]** — [Author(s), Year]
[3–7 sentence annotation.]

### Further

**[Exact resource title]** — [Author(s), Year]
[3–7 sentence annotation including honest note about level or context.]

---

> **Assessment connection:** [Name the specific wonder question or project
> task that the Key resource directly helps with.]
```

---

## CHAPTER TO TRANSFORM:

[paste chapter text here]
