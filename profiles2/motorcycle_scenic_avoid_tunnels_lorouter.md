# motorcycle_scenic_avoid_tunnels_lorouter.brf

Motorcycle touring profile for LocusMap LoRouter and BRouter.

## Technical base

The profile is rebuilt from the current official BRouter `car-vario.brf` and uses:

```brf
---model:btools.router.KinematicModel
```

It therefore combines realistic speed/access handling with additive `costfactor` preferences.

## Main options

```brf
assign avoid_toll          = false
assign avoid_unpaved       = true
assign avoid_motorways     = false
assign consider_river      = false
assign consider_forest     = false
assign consider_town       = true
assign avoid_tunnels       = true
assign tunnel_avoidance    = 2
assign prefer_scenic_roads = true
```

`consider_town` is the official BRouter city/big-town avoidance switch. It uses `estimated_town_class` rather than only checking residential roads or urban speed limits.

## Tunnel avoidance

Tunnel penalties are added to the `costfactor`:

- `0`: off
- `1`: medium, +20
- `2`: strong, +50
- `3`: extreme, +100

Because the cost accumulates over distance, long tunnels are affected much more strongly than short tunnels or underpasses.

## Scenic road preference

With `prefer_scenic_roads=true`:

- motorway and motorway links: +4
- trunk and trunk links: +2
- primary and primary links: +0.5
- secondary, tertiary and unclassified roads: no additional penalty

This keeps motorways available when necessary while preferring rural secondary and pass-style roads.

## Motorcycle model

The KinematicModel parameters are approximate values for a loaded touring motorcycle with rider and luggage:

```brf
assign vmax             = 90
assign recup_efficiency = 0.0
assign totalweight      = 360
assign f_roll           = 55
assign f_air            = 0.36
assign f_recup          = 0
assign p_standby        = 500
```

They are routing approximations, not a calibrated fuel-consumption model for one specific motorcycle.

## Compatibility

The profile does not use the unsupported `covered` lookup. It uses the current official BRouter lookups `estimated_town_class`, `estimated_forest_class` and `estimated_river_class`.

If a local LoRouter installation reports `unknown lookup name: estimated_town_class`, its routing-data/lookup version is older than the current BRouter-Web environment.
