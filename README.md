# Global Building Explorer

**Every building on Earth, on one map — with its measurements, its height, and its
neighbours. One HTML file, 69 KB. No server, no database, no build step.**

### ▶ [Open the explorer](https://ali-ezz.github.io/building-explorer/)

![The explorer over Imbaba, Cairo — a building selected, its record open](preview.jpg)

<sub>Imbaba, Giza. Imagery © Esri World Imagery. Building outlines © Google, Microsoft
and Overture contributors.</sub>

---

## What it does

**Click any building** and read its record: footprint area, perimeter, compactness,
the **exact number of buildings physically touching it**, height in 2023 and 2020, an
estimate of storeys, and its share of a population total you supply.

**Travel in time.** The imagery slider moves through Esri's archive from 2014 to 2026.
Where two years turn out to be the same photograph, the app says so rather than
letting you wonder why nothing changed.

**Go anywhere.** Search any place on Earth, or use the find-me button when you are
standing in the area you are surveying.

**Share a view.** The map position lives in the URL — copy the address bar and whoever
opens it lands in exactly the same place, at the same zoom.

**Read it in English.** Street and place names appear in English wherever the data has
one, and are romanised character by character where it does not, so Greek, Cyrillic,
Arabic, Persian, Hebrew, Thai and Devanagari all render in Latin script.

Works on a phone, a tablet and a desktop, in a light or a dark theme.

---

## Measured, or estimated — the panel never blurs the two

| | |
|---|---|
| **Measured** | footprint geometry, area, perimeter, compactness, touching neighbours, the source's own confidence |
| **Estimated** | **height** — from a ~76 m grid, so it describes the block rather than the individual roof, and reads about 2 m low against finer data; **floors** — height ÷ 3.0 m, an estimate built on an estimate; **population share** — allocated by building volume from a total you enter, and **never a headcount** |

Every estimated figure carries that caveat in the panel itself, next to the number.

---

## A few things worth knowing, all of them measured

**Two open datasets often draw the same roof.** At zoom 17, the share of Overture
polygons sitting on a building the other source had already drawn was 74% over Imbaba,
90% over Cairo and 71% over Lagos — which is why buildings appeared to carry several
outlines stacked on them. Neither source can simply be dropped, because which one is
better flips by place: 634 buildings against 208 over Imbaba, but 32 against 253 over
Paris, and none at all over Beijing. The explorer picks the denser source for the
current view and hides only the *overlapping* polygons of the other, so coverage still
grows — Imbaba's 842 outlines resolve to 681 real buildings, 47 more than the best
single source alone.

**Some imagery years are the same photograph.** Comparing tile bytes over Imbaba, 2014,
2015 and 2016 are identical, and so are 2025 and 2026 — thirteen year options, ten real
captures. Which years collide depends on where you are, so it is resolved per tile.

**Building outlines date from about 2023** while the imagery may be older or newer. On a
2014 basemap you are looking at today's buildings over yesterday's ground, and the panel
warns you when the two drift apart.

---

## Data and licences — attribution is required, please keep it

| Layer | Source | Licence |
|---|---|---|
| Buildings | Google Open Buildings + Microsoft, combined by VIDA | CC BY-4.0 |
| Buildings | Overture Maps | ODbL / CC BY-4.0 |
| Height, density | Microsoft Building Density | CDLA-Permissive-2.0 |
| Imagery | Esri World Imagery Wayback | Esri terms |
| Roads, divisions | Overture Maps / OpenStreetMap | ODbL |
| Place search | Nominatim / OpenStreetMap | ODbL |

The in-app **(i)** control and the "Data & licences" panel carry the same credits.
Keep both in any copy you publish or redistribute.

**Requires an internet connection.** Nothing is bundled — every layer streams from its
publisher at the moment you look at it. That is what keeps the file at 69 KB while
covering the whole planet, and it also means the app cannot work offline.

---

## Where this came from

Built at **NARSS** (National Authority for Remote Sensing and Space Sciences, Egypt).

The explorer is the delivered product of a much larger study on **segmenting individual
buildings in dense informal settlements** — the case that breaks most methods, because
neighbouring buildings share walls and there is no gap between them to detect. That work
involved fine-tuning segmentation models on Kaggle, testing several instance-separation
approaches against one another, measuring the resolution ceiling of freely available
imagery, and validating against independent building footprints.

Two results from it shaped this app directly, and are worth stating plainly:

- **A fine-tuned model added about 9.5% over the public building data**, at roughly 50%
  precision — and separated touching buildings *worse* than the public data already
  does. At 0.26 m per pixel, the bottleneck is not the model.
- **0.26 m per pixel is the ceiling** for free imagery over the study area. Esri matches
  Google, Bing and Yandex are worse, there is no genuine zoom 20, and multi-frame
  super-resolution did not recover detail.

Which is why this explorer is built on the best available public data rather than on a
model — a conclusion reached by measurement, not assumption.

The research repository — experiments, the full findings log, training notebooks and
validation — is maintained separately and is not public.

---

## Deploying an update

This repository holds only what is published. It is a subtree of the private project
repository and is not edited here.

```bash
python3 scripts/build_global_app.py data/deliverable/global_app.html
cp data/deliverable/global_app.html site/index.html
git add site && git commit -m "site: update"
git push origin main
git subtree push --prefix site explorer main
```

GitHub Pages rebuilds within a minute or two.

## Hosting it yourself

It is one static file. Any web server works — drop `index.html` anywhere and open it.
There is nothing to configure and nothing to keep running.
