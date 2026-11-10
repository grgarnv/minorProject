# Pilot output quality baseline

This is a qualitative first-pass review of the ten frozen images and their saved image-only/context-aware outputs (`prompt ab-1`, SmolVLM2-2.2B). It records observable gaps to investigate, not human-study ratings. The image-only and context-aware outputs are shown in `comparison.html`; frozen images are in `artifacts/dataset/`. The rejected context-aware periodic-table attempt is included as a failure, not omitted.

The separate `review.csv` remains blank for independent reviewers. Copy it per reviewer and do not use this baseline as a substitute for image/context association audits or independent scoring.

## Case-by-case observations

| Sample | Image-only output | Context-aware output | First-pass quality issue to investigate |
|---|---|---|---|
| pilot-01 Sunflower | “A sunflower with yellow petals and a brown center.” | Adds “in front of a blue sky.” | Both identify the main subject correctly but omit the large flower head, stem/leaves, and composition. Context adds a visible background detail but little article-specific value. |
| pilot-02 Golden Gate Bridge | Defines the bridge and its location. | Repeats a long block of article prose about geography, routes, and recognition. | Neither describes the visible view (bridge structure, water, shoreline, or framing). The context-aware output is a clear context-copying and excessive-length failure. |
| pilot-03 Einstein portrait | “A black and white photograph of a man with white hair and a mustache.” | “A black and white photo of Albert Einstein.” | The image-only version gives visible features but omits pose/clothing/composition. The context-aware name is supported by the direct caption “Einstein in 1947,” but the output does not state that its identification comes from the caption. |
| pilot-04 Moon | “A black and white photo of the moon.” | “The moon is shown in this image.” | Both are generic. They omit the nearly full lunar disk, visible surface markings/craters, and dark background. The context-aware output is especially uninformative. |
| pilot-05 Bicycle | “A black bicycle is parked on the side of the road.” | Same as image-only. | Main object is correct, but both omit salient visible details such as the side view, front basket, rear rack, and urban background. Context does not improve the description. |
| pilot-06 Monarch butterfly | “A monarch butterfly is perched on a flower.” | Same as image-only. | Main subject/action are captured, but both omit the prominent orange-and-black wing pattern, spread wings, and green blurred background. Context does not improve the description. |
| pilot-07 Water cycle | “A map of the water cycle.” | A detailed explanation of the water cycle and human water use, closely matching supplied caption/context. | Image-only misclassifies a complex diagram as a map and misses its visible structure. Context-aware names processes, but should be checked against the actual labeled layout and arrows; much of its wording may be sourced from context rather than independently grounded in the image. |
| pilot-08 Periodic table | “A periodic table of elements.” | Rejected: “Description exceeded the word limit. Try again.” | Image-only is too generic to explain the grid, groups/periods, or color-coded categories. Context-aware generation failed validation; preserve and count this failure in comparisons. The rejected raw output is not present in the saved result record. |
| pilot-09 World map | “A world map with a blue ocean and landmasses.” | A broad explanation of what world maps represent, including “displayed in a circular shape.” | Image-only is accurate but generic. Context-aware gives generic map-purpose text instead of describing this image; its shape claim appears inconsistent with the oval projection shown and should be verified as a visual factuality error. |
| pilot-10 Solar System | Says the Sun is centered, planets are in order, and their color and size are realistic. | “A diagram of the solar system with the sun in the center and planets orbiting around it.” | Both identify the diagram but omit the visible left-to-right arrangement, labels, and important scale caveat. The image-only claim that sizes are realistic should be checked against the image and source caption; context-aware is more cautious but sparse. |

## Cross-case baseline

- **Specificity:** Photo outputs usually name the subject but omit distinguishing visible details and composition. Diagram outputs often collapse to a generic category.
- **Context use:** The bridge and water-cycle examples show the main risk: article/caption text can dominate the visible description. Context adds little or nothing for several other pairs.
- **Grounding:** The map-shape claim and Solar System scale wording are priority factuality checks. Identity naming should be explicitly attributed to the caption when that is its source.
- **Coverage and failures:** One of ten context-aware attempts failed output validation; it remains part of the baseline. The periodic table’s generic image-only result also shows a successful response can still be low-information.

## How to use this baseline

1. Have each reviewer independently complete a separate copy of `review.csv`, using the frozen image and source context, not this qualitative table as an answer key.
2. Record unsupported material claims and the evidence for each in `review_notes`; distinguish visually supported facts from caption-attributed facts.
3. Compare reviewer disagreements before changing prompts. Treat this ten-example development pilot as diagnostic only; evaluate any revised prompt on a fresh set.
