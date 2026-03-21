# Health Interpreter

An evidence-based framework for interpreting Apple Watch and wearable health data using personal baselines, composite scoring, and cross-metric pattern detection.

**This is not a diagnostic tool.** It's a methodology for understanding what your body is telling you through the data your watch already collects — and making better decisions about training, recovery, and when to talk to your doctor.

## What Makes This Different

Most health apps compare you to population averages. That's nearly useless. A "good" HRV for one person is a crisis for another.

This skill:

- **Compares you to YOU** — personal baselines established over 14-28 days
- **Detects patterns across metrics** — single metrics fluctuate; clusters of correlated changes tell the real story
- **Knows the device limits** — Apple Watch accuracy is well-studied; this skill knows when to trust the data and when not to
- **Cites real research** — every recommendation traces to published evidence with quality ratings
- **Never diagnoses** — interprets and flags for medical review

## What's Included

```
health-interpreter/
├── SKILL.md                          # The full interpretation framework
├── profile-template.md               # Your personal health profile (fill this in)
├── references/
│   └── evidence-base.md              # 28 cited studies with quality ratings
└── README.md                         # You're reading it
```

## Quick Start

1. **Copy `profile-template.md`** to your project and fill in your personal data
2. **Establish baselines** — wear your watch consistently for 14-28 days during normal life
3. **Add `SKILL.md`** to your AI assistant's context (Claude Code, Cursor, etc.)
4. **Ask questions** like "interpret my health data" or "what does my HRV trend mean?"

The skill works without a filled-in profile, but it's dramatically more useful with one.

## What It Covers

| Category | Metrics |
|----------|---------|
| **Autonomic** | HRV (SDNN), Resting HR, Heart Rate Recovery |
| **Sleep** | Duration, Deep/REM staging, Efficiency, Respiratory Rate |
| **Cardiovascular** | Walking HR, VO2max, Cardiac Drift, SpO2 |
| **Training** | TRIMP, Acute-to-Chronic Workload Ratio (ACWR) |
| **Composite Scores** | Morning Readiness (0-100), Recovery Stability (0-100), Systemic Strain (0-12) |
| **Blood Labs** | Iron panel, inflammation (hs-CRP, ESR), CBC with differential, metabolic panel (glucose, insulin, HOMA-IR, liver/kidney), hormones (testosterone, cortisol, full thyroid), advanced lipids (ApoB, Lp(a), TG/HDL ratio), micronutrients (D, B12, Mg, omega-3) |
| **Patterns** | Inflammatory flare, sleep-disordered breathing, iron limitation, overreaching, positive adaptation, pre-symptomatic relapse |
| **Lab + Wearable Correlation** | 8 cross-correlation patterns linking blood work to wearable trends (iron-limited adaptation, systemic inflammation, HPA dysfunction, eosinophilic process, insulin resistance, thyroid conversion, vitamin D cascade, positive recovery) |

## The Orientation Model

The core philosophy: **orientation, not optimization.** Every morning, check three things:

1. **Sleep duration** — enough or not?
2. **HRV trend** — 3-day direction?
3. **Active disruptors** — anything going on?

That's it. That gives you enough to make a good decision about your day. No color-coded dashboards required.

## Evidence Base

33 cited studies covering HRV-guided training, blood lab interpretation, inflammation-autonomic coupling, Apple Watch measurement accuracy, iron and performance, sleep architecture, and training load management. Every citation includes a quality rating (Strong / Moderate / Limited).

See `references/evidence-base.md` for the full list.

## Background

This framework was built from real experience — interpreting health data through chronic illness, tracking recovery patterns, and making daily training decisions based on what the numbers actually mean (not what a generic app says they mean).

The methodology matters more than any individual's data. Fill in the profile template with your own baselines and it becomes yours.

## Created By

**[Kris Puckett](https://heyneuma.com)** — designer, builder, and the person behind [Epilogue](https://apps.apple.com/app/epilogue-track-your-books/id6446276309) and [NEUMA](https://heyneuma.com).

Learn more about how this was built: [The Most Useful Thing I've Built With AI Has Nothing to Do With Code](https://heyneuma.com)

## License

MIT — use it, modify it, share it. If it helps you understand your health better, that's the point.
