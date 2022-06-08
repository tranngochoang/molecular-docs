---
layout: default
title: Human Cell
nav_order: 3
permalink: docs/examples/human-cell
parent: Examples
---
# Human cell (human_cell.mac)

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview
DNA damage induced in a simplified human fibroblast cell was evaluated using the proposed changes and compared with experimental data.
## Geometry

```
/world/worldSize 50 um
/cell/radiusSize 14 2.5 14 um
/scheduler/endTime 5.0 ns
/scheduler/maxNullTimeSteps 10000000
/dnageom/radicalKillDistance 9 nm
/dnageom/interactionDirectRange 3.5 angstrom

/dnageom/placementSize 75 75 75 nm
/dnageom/fractalScaling 75 75 75 nm
/dnageom/definitionFile geometries/cube-centred-X-8.txt
/dnageom/placementVolume turn geometries/turned_solenoid_750_withHistone.txt
/dnageom/placementVolume turntwist geometries/turned_twisted_solenoid_750_withHistone.txt true
/dnageom/placementVolume straight geometries/straight_solenoid_750_withHistone.txt
```
![human_Cell]({{"/assets/images/humanCellImage.png" | relative_url}})
{: .text-center}

## Particle source

```
/gps/pos/type Plane
/gps/pos/shape Circle
/gps/pos/centre 0 3000 0 nm
/gps/pos/rot1 0 0 1
/gps/pos/rot2 1 0 0
/gps/pos/radius 7100 nm
/gps/direction 0 -1 0
/gps/particle  proton
/analysisDNA/fileName 50MeV
/gps/energy 50 MeV
/run/beamOn 2
```