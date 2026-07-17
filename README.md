# Week 2: Data Wrangler — Ops Sensor Log

Deep-dive cleaning and analysis of one week of simulated processing-plant sensor
telemetry (`ops_sensor_log_dirty.csv`), submitted as a GitHub repository per the
Week 2 project brief.

## Repo contents

```
.
├── week2_data_wrangler.ipynb   # Part A: full technical notebook (profiling,
│                               #   cleaning pipeline, time-series analysis,
│                               #   aggregation, visualization)
├── data/
│   └── ops_sensor_log_dirty.csv
├── report/
│   └── Week2_Insight_Report.pdf  # Part B: 1-page annotated Plant Manager report
├── PEER_REVIEW_TEMPLATE.md    # Part C: checklist used when reviewing a pod-mate's repo
└── README.md
```

## Part A — Technical Notebook (`week2_data_wrangler.ipynb`)

1. **Ingestion & Profiling** — loads the raw CSV, runs `.info()` / `.describe()`,
   and documents a full Data Health Report identifying 6 concrete quality issues
   (inconsistent `Zone` spellings, missing values, a corrupted timestamp, duplicate
   rows, sensor fault codes, and zero-value dropout readings).
2. **Cleaning Pipeline** — a reusable `clean_ops_data(df)` function with justified
   choices for each fix (see the function's docstring / the notebook's markdown).
3. **Time-Series Analysis** — hourly resampling of the cleaned data plus a 24-hour
   rolling average on `Pressure_PSI`.
4. **Aggregation** — Mean / Max / Min summary tables by `Shift` and by `Zone`.
5. **Visualization** — raw vs. cleaned pressure trend over the full week, with a
   bonus look at where sensor faults cluster (Zone_North / Zone_South).

Run it with `jupyter notebook week2_data_wrangler.ipynb` from the repo root (paths
in the notebook are relative to the repo root, e.g. `data/ops_sensor_log_dirty.csv`).

## Part B — Insight Report (`report/Week2_Insight_Report.pdf`)

A 1-page, code-free PDF written for a Plant Manager: the raw-vs-cleaned pressure
chart with annotated call-outs, followed by a Context → Insight → Action narrative
recommending a targeted sensor check in Zone_North and Zone_South plus an
ingestion-time range check to stop fault codes from reaching live dashboards.
