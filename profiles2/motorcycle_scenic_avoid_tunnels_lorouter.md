# motorcycle_scenic_avoid_tunnels_lorouter.brf

LoRouter/LocusMap profile derived from the current uploaded `LoCarVarioEco.brf`.

## Why this version exists

The previous variant was based on an older `car-vario.brf`. The current Locus car profiles use:

```brf
---model:btools.router.KinematicModel
```

and the current `allow_*` switch style:

```brf
assign allow_toll      = true
assign allow_unpaved   = false
assign allow_motorways = true
assign allow_ferries   = true
```

This profile follows that structure.

## Main switches

```brf
assign avoid_tunnels       = true
assign tunnel_avoidance    = 2
assign city_avoidance      = 2
assign prefer_scenic_roads = true
assign avoid_small_bad_roads = true
assign vmax                = 85
```

## Behaviour

- `tunnel=yes`: capped to 20 / 12 / 8 km/h depending on avoidance strength.
- City roads: residential/living/service/30-zone/urban tags get lower caps.
- Motorway/trunk/primary roads: allowed but speed-capped so they are less attractive for scenic motorcycle routing.
- Secondary/tertiary/unclassified roads remain mostly unchanged, so rural and pass-style roads are preferred indirectly.
- Unsupported shelter/gallery lookup keys are not referenced, because some LoRouter/BRouter lookup tables reject them with `ParseException: unknown lookup name`.

## Installation

Copy the `.brf` file to a BRouter/LoRouter profiles folder, for example:

```text
/Android/data/menion.android.locus/files/Locus/router/profiles2/
/Android/data/btools.routingapp/files/brouter/profiles2/
```

If Android blocks direct access to `/Android/data`, place the file in `Download` and import/open it with Locus.
