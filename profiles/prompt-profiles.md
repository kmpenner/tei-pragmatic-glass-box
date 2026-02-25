# Prompt Profiles

A **Prompt Profile** is a citable, version‑controlled method used to generate LLM suggestions. Each profile encapsulates the instructions, model settings, and expectations for a specific type of editorial claim.

Prompt Profiles are declared once in your TEI header or project documentation and referenced by ID (e.g., `@source="#prompt.align.v1"`) in each suggestion record. This approach avoids duplicating lengthy prompt text and supports reproducibility.

## What to include in a profile

- **Profile ID:** A stable identifier following the pattern `prompt.<task>.v<version>` (e.g., `prompt.align.v1`).
- **Purpose:** A concise description of what claim type the profile generates (e.g., alignment links, segmentation boundaries, normalization candidates, lemma/morph tags).
- **Model and settings:** The LLM family/name, temperature or decoding settings, and any other relevant hyperparameters.
- **Date introduced:** When the profile was first used.
- **Input assumptions:** What the model sees (e.g., a passage with anchors, limited policy rules) and what it does not see (e.g., no external data or hidden context).
- **Output contract:** What constitutes a valid suggestion record (e.g., targets must be `xml:id` anchors; must not rewrite the base text; must not invent anchors).
- **Prompt text or storage policy:** Either include the full prompt text here, or store a hash and maintain the prompt text in a private repository. This ensures transparency while accommodating copyrighted material.
- **Version notes:** A brief summary of what changed from the previous version and why.

## Example

```
Profile ID: prompt.align.v1
Purpose: Generate proposed alignment links between a source token and its normalized expansion.
Model: GPT‑4; temperature 0.2
Date introduced: 2026‑01‑15
Input assumptions: Receives a line of text with `xml:id` anchors and the desired target segmentation rules; does not have access to external corpora.
Output contract: Returns one or more `<link>` elements referencing `xml:id` anchors. Must not introduce new IDs.
Prompt text: Stored privately; hashed as `a1b2c3...`
Version notes: Initial version for alignment tasks.
```

When updating a profile, increment the version number and briefly document the change. For example, you might refine the prompt to reduce over‑regularization or to better respect dialectal variation.