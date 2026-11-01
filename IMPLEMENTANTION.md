The Kigali inputs stay as two source files in `tools/data/`:

- `kgl-datasets-big-version.geojson`
- `kgl-around-kcc-elevation.tif`

`npm run build` reads both files directly and generates `js/kigali-geodata.js`; it does not split or rewrite the GeoJSON. Run it after changing either input or `tools/bbox.json`. The bbox sets the terrain grid and map extent, but does not clip GeoJSON features. Terrain beyond the TIFF coverage uses clamped edge elevations.

The old Nairobi Overpass extracts, fetch scripts, terrain JSON, and captured building models have been removed from the data pipeline. The UI labels are intentionally unchanged. Traffic, camera presets, and other hard-coded Nairobi gameplay assumptions remain for a later integration.