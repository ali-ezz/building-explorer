# Attribution and data licences

> The MIT licence in `LICENSE` covers the viewer code only. Every layer below keeps
> its own licence and is not affected by that grant.

The Global Building Explorer displays data published by third parties. **Crediting
them is a condition of those licences, not a courtesy.** The application carries the
credits in two places — the (i) control on the map and the "Data & licences" section
of the panel. Both must be kept in any copy that is published or redistributed.

## Layers

### Building footprints — Google Open Buildings + Microsoft, combined by VIDA
Licence: **CC BY-4.0**
Google Open Buildings and Microsoft Building Footprints, conflated and published by
VIDA as a single global layer.
https://source.coop/vida/google-microsoft-open-buildings

### Building footprints, roads and administrative divisions — Overture Maps
Licence: **ODbL** for OpenStreetMap-derived content, **CC BY-4.0** for the rest
Overture Maps Foundation. Includes data © OpenStreetMap contributors.
https://overturemaps.org

### Building height and density — Microsoft
Licence: **CDLA-Permissive-2.0**
Microsoft Building Density, 2020Q4 and 2023Q4.
https://opendata.aiforgood.ai

### Satellite imagery — Esri World Imagery Wayback
Licence: **Esri terms of use**
Esri, Maxar, Earthstar Geographics and the GIS User Community. Imagery is streamed
from Esri at view time; none of it is stored or redistributed by this repository.
https://livingatlas.arcgis.com/wayback/

### Place search — Nominatim
Licence: **ODbL**. Data © OpenStreetMap contributors.
Subject to the Nominatim usage policy.
https://nominatim.org

## Software

| Library | Licence |
|---|---|
| MapLibre GL JS | BSD-3-Clause |
| PMTiles | BSD-3-Clause |
| geotiff.js | MIT |
| Noto Sans (glyphs) | SIL Open Font License 1.1 |

## What this repository contains

Two files of substance: one HTML document and one screenshot. **No third-party data
is stored here.** Every layer is fetched directly from its publisher when a user opens
the page, which is why the application cannot work offline.

The screenshot in the README shows Esri imagery and building outlines from the
sources above, reproduced for documentation and credited in its caption.
