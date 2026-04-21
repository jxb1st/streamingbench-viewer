# StreamingBench Viewer

A case-by-case web viewer for the [StreamingBench](https://arxiv.org/abs/2411.03628) benchmark — ships with a 45-video representative subset for browsing directly from GitHub Pages.

**Live site:** https://jxb1st.github.io/streamingbench-viewer/

## What this is

StreamingBench is a benchmark for **streaming video understanding** in multimodal LLMs, with four tasks:

- **Real-Time Visual Understanding** (10 sub-tasks: action, attribute, causal, counting, events, objects, spatial, text-rich, clips-summarize, prospective reasoning)
- **Omni-Source Understanding** (6 sub-tasks covering audio+visual alignment and discrimination)
- **Sequential QA** (multi-turn QA where prior turns' groundtruth answers are injected as context)
- **Proactive Output** (polling until the model decides it's the right moment to emit a pre-specified string)

The viewer lets you inspect each sample: the video, the full model prompt (including the SQA context-accumulation mechanism), metadata, options, correct answer, and per-task statistics.

## Contents

- `index.html` — single-file viewer (all CSS + JS inline)
- `data/questions_{real,omni,sqa,proactive}.json` — filtered to the subset
- `videos/` — 45 re-encoded 480p mp4s (h264 CRF 28 / AAC 64k / faststart)
- `file_durations.json` — duration lookup for the subset
- `selection_report.md` — which samples were picked and why

## Subset selection (~45 videos)

| Task | Criterion | Count |
|------|-----------|-------|
| Real | 10 sub-tasks × 2 shortest per | 20 |
| Omni | 6 sub-tasks × 2 shortest per | 12 |
| Proactive | 5 top video categories × 2 per | 10 |
| SQA | 3 groups with the most turns | 3 |

After 480p re-encoding, total video payload is ~600 MB (within GitHub Pages' 1 GB soft quota).

## Local preview

```bash
cd streamingbench-viewer
python3 -m http.server 8000
# open http://localhost:8000/
```

## Full benchmark

This viewer is a browseable sampler. For evaluation, use the full dataset from [Hugging Face](https://huggingface.co/datasets/mjuicem/StreamingBench) and the eval pipeline from [THUNLP-MT/StreamingBench](https://github.com/THUNLP-MT/StreamingBench).
