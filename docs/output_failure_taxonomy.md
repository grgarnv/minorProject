# Output quality failure taxonomy

This taxonomy labels the saved **ab-1 development pilot** for prompt iteration. Tags describe observed or suspected output problems, not reviewer scores or population rates. `benchmark/results/pilot/quality_baseline.md` contains the case-by-case evidence. Human ratings and context-association audits remain pending.

| Tag | Failure type | How to apply it | Pilot examples |
|---|---|---|---|
| `GENERIC` | Subject named without enough image-specific information | The description could fit many images of this subject; it omits salient visible features, arrangement, or composition. | pilot-01, 03, 04, 05, 06, 08, 09, 10 |
| `SCENE_OMISSION` | Important visible scene or structure omitted | A photo lacks framing/background/props, or an information graphic lacks its layout, labels, ordering, or relationships. | pilot-02, 04–10 |
| `CONTEXT_COPY` | Article prose substitutes for image description | The response recites nearby article facts instead of describing the selected pixels. | pilot-02; possible for pilot-07 and pilot-09 |
| `CONTEXT_UNDERUSE` | Available context adds no useful, grounded relevance | Context-aware output is unchanged, generic, or fails to use an associated caption where it could clarify image purpose. | pilot-05, 06, 08, 10 |
| `UNSUPPORTED_VISUAL` | Claim may conflict with visible evidence | Record the exact claim and image evidence; do not tag merely because a detail is absent from a short description. | pilot-09 “circular shape” (verify); pilot-10 “realistic color and size” (verify) |
| `SOURCE_ATTRIBUTION` | Source-supported fact is presented as visually recognized | A name/category comes from caption or article association but the response implies the model identified it from pixels. | pilot-03 name lacks caption attribution; review pilot-07 category/process claims |
| `IMAGE_TYPE_ERROR` | Wrong image-type framing | A map/chart/process/diagram is called another type or receives instructions inappropriate to its visual structure. | pilot-07 “map of the water cycle” |
| `TEXT_RELATION_ERROR` | Labels or text relationships are missing or unreliable | The output misses readable text, assigns a value/category incorrectly, or asserts arrows/relationships without visible support. | pilot-07, pilot-08, pilot-10 require detailed inspection |
| `OVERLONG` | Description is far longer than needed or exceeds the constraint | Repeated background facts crowd out useful image information, or validation rejects the result for length. | pilot-02; pilot-08 context-aware rejection |
| `GENERATION_FAILURE` | No usable description returned | Preserve the failure and its error; do not drop it from denominators or silently retry. | pilot-08 context-aware |

## Labeling rules

- One output can have multiple tags. Add a short note pointing to the relevant sentence and visible/source evidence.
- Separate **visible support** from **source support**. A direct caption can support an attributed identity, but does not prove visual details.
- Use `UNSUPPORTED_VISUAL` only after comparing the claim to the frozen pixels. Mark uncertain cases “verify” until a reviewer checks them.
- Apply `CONTEXT_COPY` when sourced prose replaces image description, not simply because an output uses a fact that is also in the article.
- Keep generation/validation failures in the evaluation. Treat the failure itself as an outcome.
- Use the tags to select one failure target per prompt revision. Do not tune against the held-out set.

## Pilot tally (qualitative triage, not rates)

- Strongest prompt-development targets: `GENERIC`, `SCENE_OMISSION`, `CONTEXT_COPY`, and `IMAGE_TYPE_ERROR`.
- Measurement targets for reviewer verification: `UNSUPPORTED_VISUAL`, `SOURCE_ATTRIBUTION`, and `TEXT_RELATION_ERROR`.
- Reliability/length outcomes to retain: `OVERLONG` and `GENERATION_FAILURE`.

Counts should be produced only after independent annotations are reconciled. The sample has ten examples and is not representative of Wikipedia images.
