# strum-neuro.github.io

The website for **STRUM** — a dyadic multimodal neuroergonomics dataset from SCCN (UC San Diego)
and the U.S. Army Research Laboratory.

Served at **<https://strum-neuro.github.io>** by GitHub Pages from `main`.

| Path | |
|---|---|
| `index.html` | landing page — what STRUM is, one session drawn to scale, and where to go next |
| `explorer/` | **session explorer** — per-session and per-participant modality coverage, montage variants, delivered block structure, inter-brain clock alignment |
| `structure/` | **experiment structure** — the five blocks and their missions to scale, and the events each mission emits |
| `hed/` | **event → HED mapping** — all 55 event types with their validated HED-3G tags, meanings and filled examples |
| `data/` | the same data the pages are built from, as JSON |

## Where the content comes from

The two explorer pages are **generated**, not hand-written. Their sources live in the conversion
repository (`strum-neuro/strum-bids`):

```
viz/build_dashboard.py  ->  strum-dashboard.html + strum-sessions.json   ->  explorer/
viz/build_structure.py  ->  strum-structure.html + strum-structure.json  ->  structure/
viz/build_hed.py        ->  strum-hed.html       + strum-hed.json        ->  hed/
```

Copy them across with `uv run viz/sync_site.py`, which also fails if the landing page's
hardcoded block medians have drifted from `strum-structure.json`. Do not edit
`explorer/index.html` or `structure/index.html` by hand — the next regeneration overwrites them.

All three pages are generated; none should be edited by hand. `hed/index.html` renders
`.context/hed/strum_event_hed_master.tsv`, so a change to the annotation shows up here once
`build_hed.py` and `sync_site.py` are re-run.

## Not yet indexed

`robots.txt` disallows all crawlers and `index.html` carries `noindex, nofollow`, so the site does
not appear in search results while the dataset is unreleased. The URL still works for anyone given
it. **To publish: delete `robots.txt` and remove the `noindex` meta tag from `index.html`.**

## Notes

- Everything is static and self-contained: no build step, no external scripts, fonts or images.
  `.nojekyll` disables Jekyll processing.
- The pages follow the viewer's light/dark preference and remember an explicit choice.
- No participant-identifying information appears anywhere on the site or in `data/` — the records
  carry BIDS subject IDs, channel counts and coverage flags only.
