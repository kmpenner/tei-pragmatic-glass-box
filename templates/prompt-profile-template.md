# Prompt Profile Template (Citable Method)

**Profile ID:** `prompt.&lt;task&gt;.vN`  
Example: `prompt.align.v1`

## Purpose (1–2 sentences)
What claim type does this profile generate? (e.g., alignment links, segmentation boundaries, normalization candidates, lemma/morph tags)

## Model + settings (minimal)
- Model family/name:
- Temperature / decoding:
- Date introduced:
- Notes on constraints (if any):

## Input assumptions
What the model is allowed to see (e.g., only the excerpt with `xml:id` anchors, plus limited policy rules). What it does *not* see (e.g., no external corpora or hidden context).

## Output contract (machine‑checked expectations)
Describe what a “valid suggestion record” must include. For example, targets must be `xml:id` anchors; suggestions must not rewrite the base text; suggestions must not invent anchors.

## Prompt text (optional storage policy)
Include the full prompt text here **or** store a hash and note where the prompt is stored in a private repository. This allows reproducibility while respecting copyright or privacy constraints.

## Version notes
What changed from the previous version, and why (1–3 bullets).