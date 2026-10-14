# Oudegracht drone flight — Google Maps 3D

A single-page web app that flies a camera along the Oudegracht in Utrecht using
Google's photorealistic 3D map (`<gmp-map-3d>`, Maps JavaScript API). The camera
stays low above the water, looks forward, and follows the canal through every bend,
from Tolsteeg to just past the Weerdbrug (about 1.9 km).

## Running it

1. Get a Google Maps API key with the **Maps JavaScript API** enabled and billing
   active on the Google Cloud project.
2. Open `index.html` in a recent desktop browser (Chrome works best).
3. Enter the key when asked. You can also:
   - put it in `API_KEY` at the top of the script in `index.html`, or
   - pass it in the URL: `index.html?key=YOUR_KEY`.

If you open the file straight from disk, use a key without website restrictions.
When hosting (for example with GitHub Pages), restrict the key to your own domain
instead, and don't commit an unrestricted key to the repository.

## Controls

| Action | Control |
| --- | --- |
| Play / pause | Big button or `Space` |
| Restart | Restart button or `R` |
| Jump ±25 m | `←` / `→` |
| Jump anywhere | Timeline slider, or click the overview map |
| Settings | Sliders button: speed, height above the water, downward look, field of view, direction, bridge hop, water level |

Settings are remembered in the browser (localStorage).

## Notes

- **Water level.** The camera height is the water level plus the chosen height
  above it. The default water level is +0.5 m above sea level, estimated from the
  municipality's archaeology report, which puts the wharves at about +1 m NAP.
  Google's 3D mesh can be off by a metre or so. If you end up below the water or
  too high, pause, choose *Meet op de kaart* and click on the water to calibrate.
- **Bridges.** In the 3D mesh the 16 bridges are solid, so at water level the
  camera briefly passes through them. Turn on *Over bruggen heen* to hop smoothly
  over each bridge instead.
- **Route.** The canal centreline and bridge outlines come from OpenStreetMap. The
  line is resampled every metre and smoothed (Gaussian), and the heading is derived
  from the smoothed line, so the camera stays parallel to the canal in the bends.

## Data and attribution

- Canal centreline and bridges: © [OpenStreetMap](https://www.openstreetmap.org/copyright)
  contributors, available under the Open Database License (ODbL).
- 3D map imagery: © Google and its data providers, shown through the Maps JavaScript API.
