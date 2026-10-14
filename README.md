# Drone flights over the water — Google Maps 3D

A single-page web app that flies a camera along the water through four cities, using
Google's photorealistic 3D map (`<gmp-map-3d>`, Maps JavaScript API). The camera
looks forward and follows the water through every bend. Pick a route from the menu
under the title; it opens on Utrecht.

| Route | From → to | Length | Default view |
| --- | --- | --- | --- |
| Utrecht – Oudegracht | Tolsteeg → past the Weerdbrug | 1.9 km | 25 m up, 25° down, 50° FOV, 5 m/s |
| Amsterdam – Herengracht | Brouwersgracht → Amstel (via the Gouden Bocht) | 2.5 km | 25 m up, 25° down, 50° FOV, 6 m/s |
| Venice – Canal Grande | Piazzale Roma → San Marco basin | 4.3 km | 25 m up, 25° down, 50° FOV, 8 m/s |
| New York – East River | Lower Manhattan → Williamsburg | 4.2 km | 30 m up (under the bridges), 8° down, 55° FOV, 12 m/s |

When you switch routes, the camera flies across the globe to the new city. Each route
keeps its own settings, and has its own link: `index.html?route=utrecht`,
`?route=amsterdam`, `?route=venetie` or `?route=newyork`.

## Running it

Open `index.html` in a recent desktop browser (Chrome works best). A Google Maps
API key is set in `API_KEY` at the top of the script, so the flight starts straight away.

To use a different key:
- replace `API_KEY` in `index.html` with your own key (Maps JavaScript API enabled,
  billing active on the Google Cloud project),
- pass it in the URL: `index.html?key=YOUR_KEY`, or
- click *Andere API-sleutel gebruiken* in the settings and enter it there.

The key is visible to anyone who views the page or this repository. In the Google
Cloud console, restrict it to your own websites (HTTP referrers, for example
`https://martijnkunstman.github.io/*`) and to the Maps JavaScript API only, so others
can't use it on your bill.

## Controls

| Action | Control |
| --- | --- |
| Choose a route | Click the route name (top left) |
| Play / pause | Big button or `Space` |
| Restart | Restart button or `R` |
| Jump ±25 m | `←` / `→` |
| Jump anywhere | Timeline slider, or click the overview map |
| Settings | Sliders button: speed, height above the water, downward look, field of view, direction, bridge hop, water level, reset to the route's defaults |

Settings are remembered per route in the browser (localStorage).

## Notes

- **Water level.** The camera height is the water level plus the chosen height
  above it. Defaults: Utrecht +0.5 m (estimated from the municipality's archaeology
  report, which puts the wharves at about +1 m NAP), Amsterdam −0.4 m (canal level),
  Venice and New York 0 m (tidal, around mean sea level). Google's 3D mesh can be off
  by a metre or so. If you end up below the water or too high, pause, choose
  *Meet op de kaart* and click on the water to calibrate.
- **Bridges.** In the 3D mesh the canal bridges are solid, so at water level the
  camera briefly passes through them. Turn on *Over bruggen heen* to hop smoothly
  over each bridge instead. In New York the bridges are high: below 36 m the camera
  flies underneath; above that, the hop lifts it over the deck.
- **Routes.** The canal centrelines and bridges come from OpenStreetMap. The East
  River line is computed from the OpenStreetMap shorelines as the line that stays
  equally far from Manhattan and Brooklyn. Each line is resampled and smoothed
  (Gaussian), and the heading is derived from the smoothed line, so the camera stays
  parallel to the water in the bends.

## Data and attribution

- Water lines, shorelines and bridges: © [OpenStreetMap](https://www.openstreetmap.org/copyright)
  contributors, available under the Open Database License (ODbL).
- 3D map imagery: © Google and its data providers, shown through the Maps JavaScript API.
