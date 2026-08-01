# strum-neuro.github.io

The website for **STRUM** — a dyadic multimodal neuroergonomics dataset from SCCN (UC San Diego)
and the U.S. Army Research Laboratory.

Served at **<https://strum-neuro.github.io>** by GitHub Pages from `main`.

| Path | |
|---|---|
| `index.html` | landing page — what STRUM is, one session drawn to scale, and where to go next |
| `explorer/` | **session explorer** — per-session and per-participant modality coverage, montage variants, delivered block structure, inter-brain clock alignment |
| `structure/` | **experiment structure** — the five blocks and their missions to scale, and the events each mission emits |
| `data/` | the same data the two pages are built from, as JSON |

## Where the content comes from

The two explorer pages are **generated**, not hand-written. Their sources live in the conversion
repository (`strum-neuro/strum-bids`):

```
viz/build_dashboard.py  ->  strum-dashboard.html + strum-sessions.json   ->  explorer/
viz/build_structure.py  ->  strum-structure.html + strum-structure.json  ->  structure/
```

To update the site, regenerate there and copy the four files across. Do not edit
`explorer/index.html` or `structure/index.html` by hand — the next regeneration will overwrite them.

Every figure on the site is measured from the recordings. The landing page's session timeline uses
the block and lull medians from `strum-structure.json`; if those change, update the `BLOCKS` and
`LULL` constants at the bottom of `index.html` to match.

## Notes

- Everything is static and self-contained: no build step, no external scripts, fonts or images.
  `.nojekyll` disables Jekyll processing.
- The pages follow the viewer's light/dark preference and remember an explicit choice.
- No participant-identifying information appears anywhere on the site or in `data/` — the records
  carry BIDS subject IDs, channel counts and coverage flags only.
