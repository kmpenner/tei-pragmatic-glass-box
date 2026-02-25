# Reason Codes: Adjudication Vocabulary (Project‑Level)

This file defines the controlled vocabulary used to adjudicate LLM suggestions in the **Pragmatic Glass Box** workflow.

## Design principles

- **Project‑level, not universal.** These codes are meant to be bounded and instructor/editor‑governed.
- **Fine granularity, minimal payload.** Most events should be logged with *decision + reason code only*.
- **Tiered writing.** Add a brief rationale note only for rejections, genuine ambiguity, or instructional exemplars.

## How to apply codes

Adjudication records typically use an attribute such as `@adjudication` to store:

- **one decision code** (`#accept`, `#reject`, `#modify`, `#defer`)
- **one or more reason codes** (the “why”)

Example (Tier 0, default — no prose):

- `adjudication="#accept #ok"`
- `adjudication="#reject #unitMismatch"`

Example (Tier 1, escalated — add a short note):

- `adjudication="#reject #overRegularization"` + one‑line `<note>`

---

# 1) Decision codes (what you did)

### `#accept`

**Meaning:** The suggestion is adopted as‑is.  
**Use when:** The suggestion matches witness evidence and project policy.  
**Avoid when:** You made any substantive change (use `#modify`).  
**Typical pairing:** `#ok`, or a policy code like `#normalizationPolicy`.

### `#reject`

**Meaning:** The suggestion is refused.  
**Use when:** It is wrong, misleading, ungrounded, or violates policy.  
**Guidance:** Rejections are the most valuable learning moments—Tier 1 notes are encouraged (briefly).

### `#modify`

**Meaning:** The suggestion is partly adopted but corrected.  
**Use when:** The suggestion is “close” but needs adjustment (e.g., wrong boundary, incomplete mapping).  
**Tip:** Pair with the reason describing *what was wrong*, not what was right.

### `#defer`

**Meaning:** No decision yet.  
**Use when:** A student needs instructor review or additional evidence before adjudication.  
**Examples:** Requires consulting an image zone; policy unclear; ambiguous form beyond student level.

---

# 2) Default meta reason

### `#ok`

**Meaning:** Routine acceptance; no notable issue.  
**Use when:** Logging an accepted suggestion with minimal overhead.  
**Typical usage:** `adjudication="#accept #ok"`.

---

# 3) Reason codes (why the decision was made)

## A. Structural / mapping reasons

### `#unitMismatch`

**Meaning:** The suggested mapping assumes commensurate units when they are not (token vs phrase, contraction vs expansion, compound vs phrase).  
**Use when:** The LLM forces a neat match by ignoring unmatched material.  
**Quick example:** Aligns “don’t” to “do” and leaves “not” orphaned.  
**Often leads to:** `#reject` or `#modify`.

### `#manyToMany`

**Meaning:** The relationship is not 1:1; it requires one‑to‑many or many‑to‑one (or many‑to‑many) mapping.  
**Use when:** The model proposes a single link where multiple anchors are required.  
**Tip:** Use `#unitMismatch` when the *type* of unit differs; use `#manyToMany` when the *cardinality* differs.

### `#boundaryAmbiguity`

**Meaning:** More than one segmentation boundary is plausible; ambiguity is real.  
**Use when:** The text genuinely supports multiple segmentations and the model fails to represent that uncertainty.  
**Escalation:** Often merits a short Tier 1 note stating the alternatives.

### `#formAmbiguity`

**Meaning:** The surface form legitimately allows multiple analyses (not merely multiple segmentations).  
**Use when:** The model asserts one analysis confidently but evidence supports more than one.  
**Examples:** Alternative expansions, ambiguous attachment, ambiguous category in context.  
**Escalation:** Encourage Tier 1 note (one sentence).

---

## B. Evidence / support reasons

### `#hallucination`

**Meaning:** The model introduces content, structure, or anchors not grounded in the text.  
**Use when:** The model invents tokens, readings, or relationships.  
**Common signal:** Suggestion references anchors that do not exist or implies a structure not present.

### `#contradictsWitness`

**Meaning:** The suggestion conflicts with witness/manuscript evidence.  
**Use when:** You can point to direct contradiction.  
**Escalation:** Tier 1 note recommended; add an evidence pointer when feasible (image zone, witness reference).

### `#unsupportedClaim`

**Meaning:** The suggestion lacks support in witness evidence or project policy; it may be plausible but isn’t justified.  
**Use when:** The model “sounds right,” but you cannot ground it.  
**Contrast with `#hallucination`:** `#unsupportedClaim` might still be possible; `#hallucination` is ungrounded/invented.

---

## C. Overconfidence / flattening reasons

### `#overRegularization`

**Meaning:** The model collapses legitimate variation or uncertainty into a single clean standard form/structure.  
**Use when:** The model produces a too‑neat result that erases meaningful variation.  
**Examples:** Normalizing away historically meaningful forms; enforcing a single boundary; forcing 1:1 mapping.

### `#policyConflict`

**Meaning:** The suggestion violates your project’s editorial policy or encoding guidelines.  
**Use when:** The correct decision is determined by *policy*, even if the suggestion is linguistically plausible.  
**Tip:** This is a great code for teaching that “editorial correctness” is often policy‑governed.

---

## D. Optional linguistic extension (use only when relevant)

These are useful in courses/projects that include lemmatization, morphology, or POS tagging. If your project does not, omit these from your ODD `<valList>`.

### `#lemmaError`

**Meaning:** Wrong base form / dictionary form (lemma).  
**Use when:** The model chooses the wrong lexeme for the surface form in context.

### `#morphMismatch`

**Meaning:** Wrong morphological analysis for the chosen lemma (features don’t match).  
**Use when:** The lemma is correct but parsing/features are wrong.

### `#posError`

**Meaning:** Wrong part of speech.  
**Use when:** The model assigns an incorrect POS category (often cascading from lemma/morph errors).

---

# 4) When to add a Tier 1 note (brief prose)

Add a short `<note>` only when:

- the decision is `#reject`, **or**
- the case is genuinely ambiguous (`#boundaryAmbiguity`, `#formAmbiguity`), **or**
- it is being used as an instructional exemplar.

**Guideline:** 1 sentence is usually enough. Prefer pointing to evidence/policy over extended explanation.

---

# 5) Governance (recommended classroom rule)

- The reason‑code list is **bounded** for the term/project.
- Additions require instructor/editor approval.
- If you add a code, document it here with definition + “use when” + example.

This keeps the vocabulary consistent and the dataset comparable over time.