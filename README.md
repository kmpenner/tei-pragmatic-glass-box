# TEI Pragmatic Glass Box: Accountable AI in Editorial Workflows

This repository provides a lightweight, TEI‑conformant methodology for **using** and **teaching** Large Language Models (LLMs) in digital scholarly editing without letting AI quietly rewrite the text.

It treats LLM output as **editorial claims** (suggestions), not as base transcription—then records human decisions in a compact, machine‑actionable way.

## What this solves

LLMs can now generate plausible TEI XML and linguistic analyses. That creates a real problem for TEI pedagogy and editorial practice:

- If AI produces “valid markup,” what are we actually teaching?
- How do we prevent AI use from becoming informal, untraceable, and impossible to review?
- How do we log decisions without producing an unmanageable stand‑off file or burning out students?

This toolkit answers those questions with a **risk‑based, minimal‑payload** approach.

## Core philosophy

**LLMs should not edit the base text.**  
Instead, they submit *claims* that humans adjudicate.

The goal is to encode **accountable disagreement**, not just valid XML.

## How it works (three layers)

1. **Stable base (unchanged):**  
   The base transcription stays clean and stable, providing only `xml:id` anchors.

2. **Machine claims (stand‑off):**  
   LLM suggestions are stored as stand‑off records, each citing a versioned **Prompt Profile** (a citable method).

3. **Human adjudication (stand‑off):**  
   Each suggestion receives a compact adjudication record:
   - **Tier 0 (default):** decision + reason code only (no prose)
   - **Tier 1 (escalate):** add a brief rationale note only for rejections, genuine ambiguity, or instructional exemplars

## Minimal logging, fine granularity

We log at fine granularity (token/boundary/link level) because that’s where **editorial assumptions hide**.  
We keep it feasible by making each record tiny by default.

## Repository structure

- `docs/` — slide deck and the 1‑page conference handout  
- `vocab/` — the controlled vocabulary for adjudication (`#reasonCodes`) + ODD `<valList>` snippet  
- `profiles/` — Prompt Profiles (versioned, citable methods) + guidelines  
- `examples/` — minimal language‑agnostic TEI examples (base anchors + stand‑off suggestion/adjudication)  
- `templates/` — fill‑in templates for prompt profiles and adjudication records  

## Getting started

- Read the conference cheat sheet: **docs/one‑page‑handout.md**
- Browse the minimal TEI patterns:
  - `examples/base/`
  - `examples/standoff/`
- If adapting for teaching, start with:
  - `templates/prompt-profile-template.md`
  - `vocab/reason-codes.md`

## What “TEI‑conformant” means here

This approach does **not** propose a new TEI standard. It is a project‑level pattern using:

- stable anchors in the base transcription
- stand‑off suggestion/adjudication records (e.g., within `standOff`)
- controlled vocabulary reason codes (easy to implement via ODD `<valList>`)

## License and reuse

Reuse is encouraged. If you adapt the reason‑code vocabulary for your project or course, consider noting changes in a short changelog so others can compare practices across contexts.