# motorcycle_scenic_avoid_tunnels_lorouter.brf

LoRouter/LocusMap profile derived from the uploaded `car-vario.brf`.

## Why this version exists

The earlier `motorcycle_scenic_avoid_tunnels.brf` used the older/classic BRouter style with additive `costfactor` penalties.

The LocusMap `car-vario.brf` profile uses:

```brf
---model:btools.router.KinematicModel
```

In this model the main routing behaviour is controlled through `maxspeed`, `minspeed`, node speeds and energy/time modelling. Therefore this LoRouter-specific motorcycle variant avoids tunnels, cities and motorway-like routing by applying **speed caps** instead of classic costfactor offsets.

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
- Motorway/trunk/primary roads: not forbidden, but speed-capped so they are less attractive for scenic motorcycle routing.
- Secondary/tertiary/unclassified roads remain largely untouched, so rural and pass-style roads are preferred indirectly.

Note: `covered=yes` is intentionally not used. Some LoRouter/BRouter lookup tables do not contain the `covered` key, which causes `ParseException: unknown lookup name: covered`.

## Installation

Copy the `.brf` file to a BRouter/LoRouter profiles folder, for example:

```text
/Android/data/menion.android.locus/files/Locus/router/profiles2/
/Android/data/btools.routingapp/files/brouter/profiles2/
```

If Android blocks direct access to `/Android/data`, place the file in `Download` and import/open it with Locus.
