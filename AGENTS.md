# Agent instructions for the New York map

This file is for an agent editing the map. Read it before adding places or changing how the page works.

The map is one file, [index.html](index.html). There is no build step and no server. Pins, borough outlines, neighborhood areas, and subway lines are stored in that file. The street map loads from the internet when the phone is online. The published page is https://cassiuscas.github.io/new_york_map/ and GitHub Pages serves the branch `cursor/nyc-interactive-map-beea`.

## How the page works

The top row of chips filters the pins. **All** is always first. The other chips come from the categories actually used by places. The count next to the title is how many pins that filter shows.

**Spots** opens the same filtered list. Tap a name and the map flies to that pin and opens its panel. Tap a pin to open the same panel. **Close**, the Escape key, or a tap on the empty map dismisses it.

The panel shows the category, name, area, note, and address. If the place has a `maps` field, the panel also shows a Google Maps link that opens in a new tab.

The buttons on the map are separate from the category chips:

- **Near me** asks the browser for the phone’s location and drops a blue dot.
- **Neighborhoods** shows or hides the Manhattan neighborhood areas. The phone remembers that choice.
- **Lines** opens the subway color key. Tap a colored track to see which trains use it.
- The **New York** title zooms back out to the whole city.

A category in the URL hash, such as `#michelin`, starts the page on that filter.

## Ask before a new category or toggle

Before you add places, ask the user whether a new category or a new map toggle is required, or whether an existing one is fine.

Do this even when the request sounds like its own group. Michelin was a new category because the user asked for its own button. A single coffee shop is not. Wait for the answer before you invent a chip, a button, or a new `type`.

Use an existing category when it already fits:

| `type` | Chip label | Use it for |
| --- | --- | --- |
| `breakfast` | Breakfast | Breakfast spots. The chip stays hidden until a place uses it. |
| `coffee` | Coffee | Coffee and tea shops. |
| `bakery` | Bakery | Bakeries, pastry shops, and bread shops. |
| `restaurant` | Restaurant | Places to eat that are not in another food category. |
| `michelin` | Michelin | Michelin Guide restaurants the user asked to file under Michelin. |
| `bar` | Bar | Bars and rooftop drinks. |
| `outdoors` | Outdoors | Ferries, streets, and outdoor walks that are not in Parks or Gardens. |
| `rooftop-garden` | Rooftop garden | Rooftop parks, green roofs, and landscaped terraces. |
| `gardens` | Gardens | Community gardens and public gardens. |
| `parks` | Parks | Public parks and plazas. |
| `museum` | Museum | Museums and exhibitions. |
| `books` | Books | Bookstores and reading rooms. |
| `show` | Shows | Performances, tapings, galleries, and ticket booths. |

The map toggles that already exist are Neighborhoods, Lines, Spots, Near me, and the title zoom. Do not add another toggle unless the user says the existing ones are not enough.

## Adding a place

Search `PLACES` for the name first. If it is already on the map, update that entry. Do not drop a second pin on the same spot.

`PLACES` is the array near the top of the script in `index.html`. Copy one object and fill it in:

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

- `name` is the pin title.
- `type` is the category used for the pin color when All is selected. It must be one of the ids above unless the user approved a new category.
- `area` is the neighborhood and borough, or the city if it is outside the five boroughs. Example: `Park Slope, Brooklyn`.
- `address` is the street address, short, as you would say it. Example: `226 7th Ave`.
- `note` is one or two plain sentences: hours, price, what to order, or how to get in. Do not paste guidebook prose.
- `lat` is north. `lng` is west and is negative in New York. Use the building, not the middle of the street and not a match in the wrong borough.

Look up the real street address before you pin anything. A name search can land on a different business, a street of the same name, or a second location. If the house number is missing or the match is outside New York City when the place is in the city, look the address up again. Do not invent a coordinate.

### A place that belongs to two categories

Keep one pin. Set `type` to the category it should wear on All, and set `types` to every category it should appear in. Vato is the pattern: `type` is `restaurant`, and `types` is `["restaurant", "michelin"]`. On All it looks like a restaurant. On the Michelin chip it looks like a Michelin pin. Both filters include it.

### Google Maps link

Add `maps` when the user wants a maps link in the panel. Use a search link, not a copied short link:

`https://www.google.com/maps/search/?api=1&query=` plus the URL-encoded name and address, such as `Vato, 226 7th Ave, Park Slope, Brooklyn, NY`.

The panel prints the link only when `maps` is set. Other places can omit it.

### A new category, only after the user says yes

1. Add the id to `TYPE_META` with a short label, a color, and `ink` of `#fff` or `#241c16`.
2. Add a simple original icon to `ICONS`. Do not use a company logo or the Michelin Man.
3. Insert the id into the `preferred` list inside `typesInUse`, in the order the chip should appear.
4. Mention the new chip in the filter sentence in [README.md](README.md).

A `type` that is missing from `TYPE_META` still gets a chip, colored from `EXTRA_COLORS`, and the pin falls back to the museum icon. Prefer a real color and icon once the user has approved the category.

## What not to change for a new place

Borough outlines, neighborhood shapes, and subway lines are data already in the file. A new place does not need a new overlay. Neighborhood names appear as you zoom in. Subway colors follow the MTA trunks.

Leave the sample-era wording and the published-branch note in the README accurate if you touch that file. The live site does not change until the work is merged into `cursor/nyc-interactive-map-beea`.
