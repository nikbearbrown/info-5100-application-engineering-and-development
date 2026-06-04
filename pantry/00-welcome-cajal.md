# CAJAL Figure Intelligence — Module 0: Welcome

**Source:** `chapters/00-welcome.md`
**Mode:** `/scan silent`
**Domain note:** Layout-purpose palette in effect. The chapter author has embedded `[SCOPE | Figure N.N | ...]` markers inline — CAJAL validates, formats, and applies the discipline (density, video pass, exclusion-list completeness).

The draft pre-specifies five figures via inline SCOPE markers (Fig 1.1, 1.2, 1.3, 1.4, 1.5). All five are doing distinct argumentative work and align with CAJAL design rules. Validate, architect, deliver.

---

## Density Recommendation

**5 figures, Mechanistic density.** The welcome module's entire pedagogical move is *make the invisible toolchain visible before you write code*. The figures carry the visibility argument that prose alone cannot. Five is at the upper boundary, justified by the chapter being foundational infrastructure for the whole semester.

---

## Zone Map

- **MC:** Java toolchain pipeline (source → compile → bytecode → JVM → execution). Three-layer diagnostic model (toolchain / project / program).
- **VG:** JDK-vs-JRE structural relationship — the chapter argues this is the single most common setup error and the reader must *see* what's inside each package. NetBeans project folder structure — students who can't locate the .class file have not verified.
- **PQ:** None — the chapter resists chartable data deliberately (no version-number distributions, no error-frequency stats).

---

## Figure 0.1 — JDK vs. JRE Containment

**Priority: Critical.** VG. Inline SCOPE Fig 1.1. The chapter's foundational distinction.

### Block 1 — Illustrae paste block

A nested rectangle composition. Outer rectangle (JDK): Blue `#0072B2` outlined 1pt, no fill, taking up approximately 70% of the panel area. Inside the outer rectangle, in its lower-left quadrant, an inner rectangle (JRE): Sky Blue `#56B4E9` outlined 1pt, no fill, taking up about 55% of the JDK rectangle's area. Inside the JRE, two small filled boxes side by side: JVM (Sky Blue `#56B4E9` filled) and Class Libraries (Sky Blue filled). Inside the JDK but *outside* the JRE (in the upper-right region), one small filled box: javac (Orange `#E69F00` filled) — the compiler that lives in the JDK but not the JRE. The visual mechanism: javac sits inside JDK ∧ outside JRE, which is the chapter's single most-important diagnostic distinction. White background, flat vector, single-column 89mm.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector, white background.
[C] Outer JDK rectangle, inner JRE rectangle nested inside it. Inside JRE: JVM box + Class Libraries box. Inside JDK but outside JRE: javac box.
[O] Nested-rectangle containment. JRE in lower-left quadrant of JDK to leave room for javac in the upper-right.
[P] JDK Blue `#0072B2` 1pt outline, no fill. JRE Sky Blue `#56B4E9` 1pt outline, no fill. JVM and Class Libraries Sky Blue filled. javac Orange `#E69F00` filled.
[E] No text labels in image (post-applied typography), no PATH configuration, no version numbers, no operating system layers, no classpath details, no module system, no Java logo, no human figures.

### Block 3 — Negative prompt

text labels, words, PATH configuration, version numbers, OS layers, classpath details, module system, Java logos, human figures, gibberish letters, captions, titles, decorative ornament, photographic elements, realistic textures, drop shadows, gradient fills, gradient backgrounds, hand-drawn styles, sketch lines, decorative borders, colorful backgrounds, visual clutter, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 0.2 — Java Toolchain Pipeline

**Priority: Critical.** MC. Inline SCOPE Fig 1.2.

### Block 1 — Illustrae paste block

A horizontal flow. From left to right: a small rectangle (HelloWorld.java) Sky Blue `#56B4E9` filled, a Black `#000000` 1pt arrow labeled implicitly *javac*, a rectangle (HelloWorld.class) Blue `#0072B2` filled, a Black 1pt arrow labeled implicitly *JVM*, a rectangle with three small horizontal sub-bands inside (Win/Mac/Linux) Sky Blue filled. Beneath the entire flow, a horizontal Orange `#E69F00` 1pt dashed bracket spanning the rightmost rectangle — the *portability* annotation zone. White background, flat vector, double-column 174mm preferred.

### Block 2 — Full SCOPE prompt

[S] Double-column 174mm preferred, vector, white background.
[C] 3-node horizontal pipeline: source file → bytecode → execution (with 3 OS sub-bands). 2 transformation arrows between nodes. Portability bracket beneath the execution node.
[O] Strict left-to-right flow. Equal-spaced arrows. OS sub-bands stacked inside the execution rectangle.
[P] Source rectangle Sky Blue `#56B4E9` filled. Bytecode rectangle Blue `#0072B2` filled. Execution rectangle Sky Blue filled with OS sub-bands. Arrows Black `#000000` 1pt single-headed. Portability bracket Orange `#E69F00` 1pt dashed.
[E] No text labels, no file extension typography (.java/.class), no javac/JVM text, no OS names, no classpath, no packages, no IDE toolbar, no multiple class files, no jar packaging, no module system.

### Block 3 — Negative prompt

text labels, words, file extensions, OS names, IDE toolbar, jar packaging, module system, gibberish letters, captions, titles, decorative ornament, photographic elements, realistic textures, drop shadows, gradient fills, gradient backgrounds, hand-drawn styles, sketch lines, decorative borders, colorful backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 0.3 — Belief-Based vs. Evidence-Based Verification

**Priority: Important.** VG. Inline SCOPE Fig 1.3. The chapter's framing diagnostic.

### Block 1 — Illustrae paste block

A two-column composition. Left column header band (blank, for "Belief"); right column header band (blank, for "Evidence"). Below each header, a vertical stack of four small indicator rectangles. Left column (Belief approach): Vermillion `#D55E00` filled rectangles representing each step (installer says complete → assume it works → write code → fail with no anchor). Right column (Evidence approach): Blue `#0072B2` filled rectangles representing each step (run java/javac --version → inspect output → identify the .class file → enter coding with a small diagnostic surface). Between each pair of adjacent rectangles, a small Black `#000000` 1pt downward arrow. Thin Black 0.5pt vertical rule separates the two columns. White background, flat vector, single-column 89mm.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector, white background.
[C] Two parallel 4-step columns. Left: belief approach steps in Vermillion. Right: evidence approach steps in Blue. Inter-step downward arrows. Column divider.
[O] Side-by-side columns. Strict horizontal alignment of steps across columns. Downward arrows between adjacent steps.
[P] Belief-approach rectangles Vermillion `#D55E00` filled. Evidence-approach rectangles Blue `#0072B2` filled. Arrows Black `#000000` 1pt single-headed. Column divider Black 0.5pt.
[E] No text labels, no step names, no version numbers, no IDE screenshots, no AI tool comparisons, no runtime errors, no human figures.

### Block 3 — Negative prompt

text labels, words, step names, version numbers, IDE screenshots, AI tool icons, runtime errors, human figures, gibberish letters, captions, titles, decorative ornament, photographic elements, realistic textures, drop shadows, gradient fills, gradient backgrounds, hand-drawn styles, sketch lines, decorative borders, colorful backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 0.4 — NetBeans Project Folder Tree

**Priority: Critical.** VG. Inline SCOPE Fig 1.4. The folder hierarchy the student must be able to navigate.

### Block 1 — Illustrae paste block

A vertical tree diagram. Root node at top center: a Black `#000000` 1pt outlined rectangle labeled (in post) "MyProject". Two branches descend to two child folder nodes side by side: src/ on the left (Sky Blue `#56B4E9` filled rectangle), build/ on the right (Sky Blue filled rectangle). From src/, one leaf descends: HelloWorld.java (Blue `#0072B2` filled smaller rectangle). From build/, one intermediate folder descends: classes/ (Sky Blue filled), and from classes/, one leaf descends: HelloWorld.class (Blue filled smaller rectangle). All connecting lines Black 1pt solid right-angled (orthogonal tree-routing). White background, flat vector, single-column 89mm.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector, white background.
[C] Tree with root MyProject. Two top-level folders: src/ and build/. Under src/: HelloWorld.java leaf. Under build/classes/: HelloWorld.class leaf.
[O] Vertical tree, root at top, leaves at bottom. Orthogonal connector routing. Two-level depth for src branch, three-level depth for build branch.
[P] Folder nodes Sky Blue `#56B4E9` filled rectangles. Leaf nodes Blue `#0072B2` filled smaller rectangles. Connector lines Black `#000000` 1pt solid orthogonal. Root rectangle Black 1pt outlined, no fill.
[E] No text labels, no folder names, no filenames, no nbproject/ folder, no manifest files, no library jars, no package subdirectories, no IDE toolbar, no run configuration icons, no file-type icons.

### Block 3 — Negative prompt

text labels, words, folder names, filenames, file-type icons, nbproject folder, manifest files, library jars, IDE toolbar, gibberish letters, captions, titles, decorative ornament, photographic elements, realistic textures, drop shadows, gradient fills, gradient backgrounds, hand-drawn styles, sketch lines, decorative borders, colorful backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 0.5 — Three-Layer Diagnostic Model

**Priority: Critical.** VG. Inline SCOPE Fig 1.5. The diagnostic framing that persists through the semester.

### Block 1 — Illustrae paste block

A vertical stack of three horizontal bands of varying widths. Bottom band (widest, foundation): Blue `#0072B2` filled, full panel width — the toolchain layer (JDK, JVM, PATH). Middle band (medium width, centered): Sky Blue `#56B4E9` filled, approximately 75% of the bottom band width — the project layer (NetBeans structure, build config). Top band (narrowest, centered): Orange `#E69F00` filled, approximately 50% of the bottom band width — the program layer (Java source). Bands stacked flush vertically. To the right of each band, a small Vermillion `#D55E00` filled rectangle indicating the characteristic failure type for that layer ("command not found" / "class not found" / compile errors and runtime exceptions). White background, flat vector, single-column 89mm.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector, white background.
[C] Three-band vertical stack. Widest bottom band (toolchain). Medium middle band (project). Narrowest top band (program). Lateral failure-type indicators on the right for each band.
[O] Vertical stack, bottom-to-top, centered horizontally. Widths step down each level. Failure indicators external on right side.
[P] Toolchain band Blue `#0072B2` filled. Project band Sky Blue `#56B4E9` filled. Program band Orange `#E69F00` filled. Failure indicator rectangles Vermillion `#D55E00` filled.
[E] No text labels, no layer names, no failure-type descriptions, no IDE screenshots, no specific error text, no OS-specific path syntax, no version numbers, no network or classpath issues, no human figures.

### Block 3 — Negative prompt

text labels, words, layer names, failure descriptions, IDE screenshots, error text, OS-specific syntax, version numbers, network details, human figures, gibberish letters, captions, titles, decorative ornament, photographic elements, realistic textures, drop shadows, gradient fills, gradient backgrounds, hand-drawn styles, sketch lines, decorative borders, colorful backgrounds, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass

**FIGURE 0.1 (JDK/JRE):** STATIC SUFFICIENT. Containment is a structural claim.
**FIGURE 0.2 (Toolchain pipeline):** STATIC SUFFICIENT — borderline. A short animation of source compiling to bytecode and bytecode executing would communicate the two-stage transformation viscerally. But static lets the reader inspect the portability annotation simultaneously.
**FIGURE 0.3 (Belief vs. evidence):** STATIC SUFFICIENT.
**FIGURE 0.4 (Folder tree):** STATIC SUFFICIENT.
**FIGURE 0.5 (Three layers):** STATIC SUFFICIENT.

**Video candidates identified: 0.** No production recommended.

---

## Split-point note

The chapter's task tables (AI-appropriate / what student must verify), the AI prompt template, and the five-item verification checklist are typography — hand to the typesetter. The two-column "what AI can do / cannot do" comparisons throughout the chapter are typography tables.
