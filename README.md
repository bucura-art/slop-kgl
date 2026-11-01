# Slop Cities - Kigali

![Flying the helicopter over KICC, CBK Pension Towers and Times Tower at golden hour](screenshots/Kigali.jpg)

A Kigali remix of [Slop New York](https://github.com/mrdoob/slop-newyork): the CBD at 1:1 on its real terrain, built with [three.js](https://threejs.org/).

## Run it

The page needs a local web server because it loads ES modules:

```bash
python3 -m http.server 8080
```

Then open http://localhost:8080. While editing, `python3 tools/serve-nocache.py 8081` serves the same files with caching off, so changed modules load on every reload.

Controls: **1–4** switch between walking, driving, cycling and the helicopter. **W**/**S** go and brake, **A**/**D** turn, **Space** jumps on foot and climbs in the helicopter, **Q**/**C** descend. Drag to look around the player and scroll to zoom. **V** steps through the cameras (**5–0** pick them directly): chase, low-angle action, first person, and fixed views of City Square, Kenyatta Avenue, Uhuru Park, Upper Hill and an aerial one. **F** switches to the free camera: click to look around (Esc releases the mouse) or drag, **WASD** moves, **Space**/**C** go up and down, **Shift** goes faster and the scroll wheel sets the speed. **Shift+1–9** fly it to the tallest towers and **Shift+0** back to the start view. **M** opens the street map, **H** hides the HUD. On a touch screen a joystick and buttons appear; a gamepad works too (left stick moves, right stick looks, the triggers drive or climb, the bumpers switch modes, Y the camera and Start the map).

Debugging, from the browser console: `window.Kigali` exposes the scene, cameras, controllers, colliders, data, traffic, lighting and the colour grade. `Kigali.roof('times')` puts the player on the roof of the tallest building whose name contains the text, `Kigali.roof(x, z)` on the building at that point, and `Kigali.roof(n)` on the nth tallest. The toolbar's Debug menu (the bug icon) does the same with a click: with **Teleport to a roof** on, clicking a building puts you on its roof (Esc turns it off).

## Make it your own

Fork it, remix it, improve it, break it. Make games, animations, films, experiments, or something completely different. Use it as a starting point and take it wherever you want. Have fun!

## Tests

```bash
npm test
```

Ports of Slop New York's controller and camera tests (`tests/`), run against the city colliders, plus checks for hills, ledges, decks and rooftop landings.

## Geodata

```bash
npm run build                    # → js/kigali-geodata.js
```

- The builder reads `tools/data/kgl-datasets-big-version.geojson` and `tools/data/kgl-around-kcc-elevation.tif` directly; it does not split or rewrite either source. After changing either input or `tools/bbox.json`, run the build and reload the game (hard-refresh if the browser cached modules).
- **Area:** `tools/bbox.json` sets the terrain grid and map extent; it does not clip GeoJSON features. The elevation TIFF covers a smaller area, so terrain samples beyond its edge use the nearest edge elevations.
- **Frame:** 1 unit = 1 m, x = east, z = south (north = -z), y = up. The origin is the Kigali Convention Centre. `GEO.frame.drivesOn` is `right`.
- **Gameplay scope:** roads, buildings, and mapped features are loaded from the generated module. Traffic lanes and cameras follow right-hand driving.
- **`GEO` contents:** roads, buildings and building parts, areas, landmarks, and mapped street furniture are derived from the GeoJSON. Rivers, rail, and stations are empty when absent from the source.
- **Road graph:** the GeoJSON has road geometries but no OSM node IDs. The build reconstructs shared graph nodes by matching road coordinates.
- **Terrain:** `GEO.terrain` is a 25 m grid, filtered toward bare ground with a ~60 m morphological opening and light smoothing. Use `heightAt(x, z)` from `js/terrain.js` to sample it, and `baseOf(ring)` for a building's footing.
- Geographic data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), ODbL 1.0. Confirm and document the elevation TIFF's source and license before redistribution.

## License and data

Code: MIT. Parts are adapted from Slop New York (MIT).

Geographic data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), ODbL 1.0.

Elevation source attribution and redistribution terms need to be confirmed for the supplied TIFF.
