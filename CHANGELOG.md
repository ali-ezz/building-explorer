# Changelog

All notable changes to the Global Building Explorer. Dates are release dates.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the
project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.1] — 2026-08-12

### Fixed

- **A blank white page on first open, with no explanation.** Three render-blocking
  scripts came from one host, `unpkg.com`, with no fallback and nothing on screen while
  they loaded. Where unpkg is slow, throttled or blocked, the whole application was a
  white page — and the only sane response to a white page is to reload it, repeatedly,
  until it works. There is now a second host (jsdelivr, already trusted here for
  geotiff.js and the ONNX runtime) via a synchronous `document.write` fallback, and a
  boot screen that says what is happening from the first paint. If both hosts fail it
  says *that*, with one deliberate "Try again", instead of leaving a blank page to be
  interpreted.
- **The status line described the map while you were looking at a picture.** It is
  pinned outside the scroll region, so it survived the mode switch that hides every
  other map control, and went on reporting "3,501 buildings in the selected area ·
  imagery 4/30/2025" under a panel describing a file. It now describes whatever the
  panel describes — the file's name, extent and ground resolution.

### Changed

- **The map's outlines are off while a picture is open**, and the map's own setting is
  handed back untouched when the picture is removed. Drawing published footprints over
  an image the moment it opens buries the thing you came to look at under somebody
  else's tracing of the same ground. They remain one press away.

---

## [1.1.0] — 2026-08-12

The theme of this release is that several things the app said about itself were not
true, and were found by opening real files rather than by reading the code.

### Added

- **Any UTM zone is now read and reprojected.** A GeoTIFF's projection is taken from its
  own `ProjectedCSTypeGeoKey` instead of being guessed, and EPSG:326xx / 327xx are
  reprojected to WGS84 with a closed-form inverse transverse Mercator. Anything still
  unidentified is refused *by EPSG name*, with the `gdalwarp` line needed to fix it.
- **A corner-fit residual** is measured and reported when an image's extent is large
  enough for the four-corner placement to matter — 1.5 mm on a drone survey, 985 m on a
  237 km scene, stated rather than left to be discovered.
- **RFC 4180 quoting** in the CSV reader, so WKT geometry columns parse.
- **`raster_content` provenance** in the export CSV and README, naming whether the mask
  holds published footprints or a model's reading, plus `model_buildings` and
  `model_coverage_union` rows when it is the latter.

### Fixed

- **A UTM GeoTIFF was placed on the wrong continent.** The projection was inferred from
  coordinate magnitude — "anything over 180 must be Web Mercator" — and UTM eastings and
  northings are also over 180. A 3.3 cm/px survey of Desa Gumantar, Lombok landed in the
  North Sea; a UTM 18N scene landed in the Algerian Sahara. Both were announced as
  "Placed from its own georeferencing. Nothing was guessed."
- **Every WKT CSV parsed to zero features**, silently, because rows were split on the
  separator and WKT is full of quoted commas.
- **The vector comparison depended on tile timing.** The same 249 buildings over the same
  ground scored "75 published / 40 extra" or "499 / 268" depending on whether tiles had
  arrived. It now waits for the map to settle and says so when it cannot.
- **"imagery Null"** — Esri returns the literal string `Null`, which is truthy, so it was
  printed as if it were a capture date.
- **A model export was georeferenced as plate carrée** when its source image was Web
  Mercator, and mixed the model's coverage into published-footprint statistics.
- **A measurement outlived its image** — measuring an upload's footprint left a phantom
  selection that survived removal, freezing clicks and misreporting the status line.
- **The file table promised two controls that did not exist**: "Check the footprints" for
  every raster, and an export for vectors.
- An EXIF-placed photo was labelled "from its own georeferencing"; a points CSV was
  titled "3 of your polygons" above "Your polygons 0"; the height table's own caveat was
  pushed below two later notes; the population row directed users to an input that had
  been removed; `fitBounds` was passed a `minZoom` it does not accept.
- **"Sharpest here" claimed about 20 seconds** and measures 70–100 s. The claim now
  matches the measurement.

### Changed

- **The image workspace is organised by subject, not by verb.** "Export for this ground"
  was a separate top-level section mirroring the map panel's Export directly underneath
  it. Showing outlines, measuring and downloading are three things done to one subject —
  the published data under your picture — so they are one section.
- Attribution now credits **ONNX Runtime Web** and the **geobase** model weights, both
  fetched at runtime.
- The README documents the features added since 1.0.0, and states that this repository is
  the working copy rather than a read-only subtree export.

### Removed

- ~240 lines of unreachable code: `scanFill`, `overtureSplit`, `exportVisible`,
  `featureName`, `removeAllFiles`, `ctxIsBuildings`, and the `LAYERS` / `buildLayerUI`
  apparatus pointing at a `#lyrlist` element that no longer existed in the markup, with
  the CSS that styled it.

---

## [1.0.0] — 2026-07-27

First public release.

- Building records: area, perimeter, compactness, exact touching-neighbour count, street
  access, source confidence, and block height from a ~76 m grid with its caveat attached.
- Area measurement: density, footprint distribution, coverage from the union of
  rasterised footprints, and block complexity (Nature, 2025).
- Export: two-colour mask with a one-pixel instance seam, colour instance mask, GeoJSON,
  statistics CSV and world files, as one ZIP, in EPSG:3857.
- Esri Wayback imagery 2014–2026, with same-photograph detection per tile, and "Sharpest
  here" to search 196 releases for the best frame over the current ground.
- One product drawn at a time, chosen by density per view, so no roof is outlined twice.
- Upload GeoTIFF, JPEG (EXIF GPS), PNG, GeoJSON, KML or CSV; run a public segmentation
  model in the browser against your own picture.
- English and romanised labels for Greek, Cyrillic, Arabic, Persian, Hebrew, Thai and
  Devanagari.

[1.1.1]: https://github.com/ali-ezz/building-explorer/releases/tag/v1.1.1
[1.1.0]: https://github.com/ali-ezz/building-explorer/releases/tag/v1.1.0
[1.0.0]: https://github.com/ali-ezz/building-explorer/releases/tag/v1.0.0
