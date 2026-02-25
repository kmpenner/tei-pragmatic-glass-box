# Adjudication Record Template

Use this template to record decisions on LLM suggestions.

## Attributes (required)

- **xml:id** – A unique identifier for the adjudication record.
- **resp** – The ID of the person making the decision (e.g., `#student_01`).
- **target** – The ID of the suggestion record being adjudicated (e.g., `#llm_sugg_01`).
- **adjudication** – A space‑separated list of the decision code and one or more reason codes (e.g., `#reject #unitMismatch`).
- **source** – The ID of the Prompt Profile used to generate the suggestion (e.g., `#prompt.align.v1`).

## Optional elements

- **`<note>`** – A brief rationale explaining the decision. Required for rejections, genuine ambiguity, or instructional exemplars. Keep it to one sentence and point to evidence or policy when possible.
- **`<linkGrp>`** – Provide a corrected mapping or annotation. For example, if rejecting a one‑to‑one mapping, supply the one‑to‑many mapping in a `linkGrp`.

## Example

```xml
<annotation xml:id="adj_01" resp="#student_01"
            target="#llm_sugg_01" adjudication="#reject #unitMismatch"
            source="#prompt.align.v1">
  <note>Contraction requires one-to-many mapping.</note>
  <linkGrp type="alignment_corrected">
    <link target="#w_dont #w_do #w_not"/>
  </linkGrp>
</annotation>
```

This template encourages consistency across adjudication records and helps to ensure that adjudications remain compact, structured, and machine‑actionable.