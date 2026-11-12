# Output quality iteration status

This record follows the quality-improvement sequence using the frozen ab-1 pilot as the diagnostic baseline.

## 1. Baseline

`benchmark/results/pilot/quality_baseline.md` reviews all ten frozen images and both saved outputs. Two separate blank annotation sheets are ready at `benchmark/results/pilot/review_reviewer_1.csv` and `benchmark/results/pilot/review_reviewer_2.csv`. Independent human scores and their disagreement resolution remain pending; no scores were invented.

## 2. Failure labels

`docs/output_failure_taxonomy.md` defines tags for generic descriptions, missing visible structure, context copying/underuse, unsupported claims, source attribution, image-type errors, text-relationship errors, verbosity, and generation failure. The taxonomy marks uncertain factuality claims for verification instead of treating them as proven errors.

## 3. Focused prompt revision

The saved pilot is `ab-1`. The new candidate is prompt `ab-7`, recorded in `backend/engine/prompts.py`. It adds one concise-detail check: include at least two distinct, concrete pixel-supported details beyond naming the topic, when the image makes them clear. It explicitly says not to pad with article facts or general knowledge. This targets `GENERIC` and `SCENE_OMISSION` while preserving uncertainty for images with few clear details.

The earlier ab-6 prompt and routing instructions already addressed the other high-priority baseline failures:

- Photo instructions request concrete appearance, framing, texture, arrangement, and background details.
- Chart, map, process, and diagram instructions request visible layout and relationships, and warn against inventing unreadable labels or connections.
- Context-aware instructions prioritize the selected image and associated caption, prohibit copying article prose, and distinguish source-supported names from visual recognition.
- The description validator retains a word limit and preserves failures as failures.

The prompt revision is versioned as ab-7 so future run records carry its prompt hash/version separately from historical runs. No model result has yet been produced for ab-7 in this execution environment.

## 4. Evaluation procedure and limits

The next comparison should use fresh, licensed Wikipedia occurrences across photos, charts/maps, and diagrams, with the prompt and model settings frozen. Independent ratings should include all outputs and failures.

The benchmark now reads model revision, device and token limit from `.env`. The collector can select articles and write images to a separate directory, so fresh collection no longer needs to overwrite frozen pilot images. Example commands are in README.md.

I attempted to collect two fresh examples (Volcano and Bar chart), but this environment could not resolve external hosts, so no new source images were collected. A local diagnostic run could load the cached checkpoint only after setting the project cache path; inference then ran on CPU because neither MPS nor CUDA is available here, and did not finish in a practical time. No new model outputs or quality gains are claimed.

Previously saved ab-5 image-type checks in `artifacts/image-types/verification-final.json` include four synthetic diagrams/charts/flags/maps and one bee photo. They are useful engineering observations, but they are not an ab-6 fresh-set comparison and do not replace step 4.

## 5. Decision

ab-7 is ready for local inference on the configured machine. Run it first on the existing pilot as a diagnostic, then collect/run the fresh two-image set using the separate image directory. Do not claim improvement from the ten-case pilot or synthetic checks. Have two reviewers complete separate sheets, compare by failure tag and agreement, then decide whether to keep or revise ab-7. A larger fresh set is needed before making a general quality claim.
