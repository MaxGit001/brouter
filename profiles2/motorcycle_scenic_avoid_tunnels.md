# motorcycle_scenic_avoid_tunnels.brf

BRouter/LoRouter/Locus profile derived from `Car-test-Template.brf`.

## Intent

- Motorcycle touring profile.
- Strongly avoid `tunnel=yes`.
- Penalize `covered=yes` weaker than true tunnels, because alpine galleries are often short and acceptable.
- Penalize larger-city/urban routing by increasing costs for residential, living-street, service, pedestrian, 30 km/h and urban-50 km/h ways.
- Prefer paved rural roads and pass-style routing indirectly by keeping secondary/tertiary/unclassified rural roads cheap while penalizing motorways, trunks, links and bad roads.

## Main tuning variables

```brf
assign avoid_tunnels          1
assign tunnel_avoidance       2
assign city_avoidance         2
assign prefer_scenic_roads    1
assign avoid_small_bad_roads  1
```

`tunnel_avoidance` values:

- `0`: off
- `1`: medium
- `2`: strong default
- `3`: extreme

Because tunnel penalty is added to `costfactor`, it scales with way length. A long tunnel is therefore punished much harder than a short underpass.

## Installation in Locus / BRouter

Copy the `.brf` file to one of these locations, depending on app and Android access:

```text
/Android/data/menion.android.locus/files/Locus/router/profiles2/
/Android/data/btools.routingapp/files/brouter/profiles2/
```

If Android blocks access to `/Android/data`, place the file in `Download` and import/open it with Locus.
