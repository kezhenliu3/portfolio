# Samples — Desensitization Statement

Everything in this directory was reviewed against the repository's desensitization rules before publication.

- **Media** — the seven screenshots in `media/` compare the public "九上阿" WeChat mini-program with a third-party app answering the same question. Brand marks of the third-party app and an in-app user name have been blurred/masked; the mini-program's own brand is left visible (it is a public product). `report-interpretation-demo.mp4` is a screen recording of the mini-program itself — a guest-mode introduction followed by a report-interpretation demo using the author's own test-report data (consented). It was transcoded (H.264, faststart), stripped of all metadata, and its audio track contains no speech (silent). No phone numbers, IDs, or personal identifiers appear in any media file.
- **Numbers** — `metrics.md` separates figures into two layers: development measurements (latency, test-pass counts) and production figures reported from operations (DAU, QPS, TTFT), which are explicitly labeled as directional because no public load-test scripts back them.
- **Dialogues** — `example-dialogues.md` contains illustrative transcripts **rewritten for sanitization**. They are not real user conversations and not verbatim system output; every question and value is fictional.
- **Configuration** — the configuration-driven design is described in words and diagrams only. No internal configuration files, snippets, or file paths are published.
- **Comparison scope** — the side-by-side comparison is a single same-question observation (anecdotal), not a benchmark. The third-party app is deliberately not named, and its screen captures are shown solely to illustrate a behavioral contrast.

*The screenshots and the video were produced by the systems themselves; the dialogue examples are rewritten illustrations. No internal source code, configuration, or other company material is published.*
