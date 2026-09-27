# New York map

A single HTML file you can open in a phone browser. There is no server to run. Pins, borough outlines, and subway lines are saved inside [index.html](index.html). The street map underneath them loads from the internet when you have a connection.

## Open it on your phone

1. Copy `index.html` onto the phone (AirDrop, email, or a cable).
2. Open the file in Safari or Chrome.
3. Pinch to zoom and tap a pin. The street names appear when the phone is online.

If the page is blank, the browser blocked the map library. Open the file again on a connection, or send it to yourself and open it from the browser’s download list.

“Near me” uses the phone’s location. Some browsers only allow that on a website, not on a file saved to the phone. Panning still works.

## Filter

The chips across the top filter the pins by activity: breakfast, coffee, restaurant, outdoors, and museum. **Spots** opens the same list. **Lines** opens the subway color key. Tap the title to zoom back out to the whole city.

## Add your own places

The sample pins are there so the map is usable before you add real plans. Edit the `PLACES` list near the top of the script in `index.html`. Copy one block and change it:

```js
{
  name: "Morning coffee",
  type: "coffee",
  area: "Carroll Gardens, Brooklyn",
  address: "123 Smith St",
  note: "What you want to remember when you tap the pin.",
  lat: 40.678,
  lng: -73.995
}
```

`type` is the filter name. A type that is not already in the list gets its own chip. `lat` is the north coordinate and `lng` is the west coordinate, which is negative in New York. You can look those up by searching the address on a map and copying the coordinates.

## What the overlays are

- Borough outlines are the five New York City boroughs, from NYC Department of City Planning boundaries.
- Subway lines are the city’s subway centerlines, colored with the MTA trunk colors (red for the 1 2 3, green for the 4 5 6, and so on). Shared tracks draw those colors side by side when you zoom in.
- The street map is © OpenStreetMap contributors, styled by CARTO.
