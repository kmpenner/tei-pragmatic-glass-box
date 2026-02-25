# The Pragmatic Glass Box: Cheat Sheet

**A TEI‑native workflow for LLM adjudication (and teaching editorial discernment)**

## 1) Workflow rules (non‑negotiables)

- **Never overwrite the base text.** LLM output lives in stand‑off (e.g., within `standOff`).
- **Prompts are methods.** Cite them by ID (e.g., `@source="#prompt.align.v1"`), not by pasting full prompt text into every record.
- **Adjudicate everything; write sparingly.** Use reason codes for routine decisions. Add a brief `<note>` only for rejections, genuine ambiguity, or instructional exemplars.

## 2) The adjudication taxonomy (ODD‑style `@ana` tokens)

### Decisions (what you did)

- `#accept` — suggestion adopted
- `#reject` — suggestion refused
- `#modify` — suggestion partially adopted or corrected
- `#defer` — needs instructor review or additional evidence

### Reason codes (why you did it)

**Structural / mapping**

- `#unitMismatch` — units are incommensurate (e.g., contracted vs expanded; token vs phrase)
- `#manyToMany` — mapping is not 1:1
- `#boundaryAmbiguity` — multiple plausible segmentations exist
- `#formAmbiguity` — the form legitimately allows multiple analyses

**Evidence / support**

- `#hallucination` — content/structure ungrounded in the text
- `#contradictsWitness` — conflicts with witness/manuscript evidence
- `#unsupportedClaim` — lacks basis in project policy or standard references

**Overconfidence / flattening**

- `#overRegularization` — flattens legitimate variation or uncertainty into a single “clean” form
- `#policyConflict` — conflicts with editorial policy or encoding guidelines

**Optional extension (linguistic)**

- `#lemmaError` — incorrect lemma/base form
- `#morphMismatch` — incorrect morphological analysis
- `#posError` — incorrect part of speech

## 3) Minimal pattern (conceptual)

Goal: keep the base transcription stable; store claims and decisions in stand‑off.

```xml
<annotation xml:id="adj_01"
            resp="#student_01"
            target="#llm_sugg_01"
            adjudication="#reject #unitMismatch"
            source="#prompt.align.v1">
  <note>Contraction requires one-to-many mapping.</note>
  <linkGrp type="alignment_corrected">
    <link target="#w_dont #w_do #w_not"/>
  </linkGrp>
</annotation>
```

**Tip:** Tier 0 adjudication is usually just `adjudication="#accept #ok"` (no note).  
Only escalate to a `<note>` when the record is contested, ambiguous, or being used as an instructional exemplar.

## 4) What you can do with the data (why this is worth it)

Because adjudications are structured, you can:

- filter by error mode (e.g., all `#overRegularization`)
- identify ambiguity hotspots (e.g., clusters of `#boundaryAmbiguity`)
- compare outcomes across prompt profile versions over time

## 5) Where to find the rest

- Full reason‑code list and ODD `<valList>`: `vocab/`  
- Prompt Profile guidance + examples: `profiles/`  
- Minimal TEI examples: `examples/`  
- Reusable templates: `templates/`