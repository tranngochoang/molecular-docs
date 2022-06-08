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
This geometry consists of a continuous chain defined by taking a basic Hilbert curve. This fractal is broken into cubic regions of straight and turned chromatin sections [DNA placement]({{"/docs/geometry-library/dna-placements" | relative_url}}). This chain is included in an ellipsoid with semi-dimensions 7.1x2.5x7.1 μm, which imitates a cell nucleus. Only cubes that are completely included in the ellipsoid are considered as parts of the chain, which length is 6.4 Gbp. Bp density of the produced cell corresponds to ~0.015 bp/nm3.
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
![human_Cell]({{"/assets/images/humanCell02.jpg" | relative_url}})
{: .text-right}

The DNA model in the simulation consists of joined straight (a), turned (c) and turned-twisted (e) chromatin segments. At a high level (a, c, e), the chromatin segments consist of a series of histones (DNA marked in yellow, protein core shown in blue). These are joined by linking sections (green) that were calculated along 3D-spline functions. The detailed structure of the straight and turned segments is also shown (b, d), with yellow lines joining the phosphate molecules and red lines joining the sugar molecules. The rotated direction of DNA fiber at beginning in both turned and turned-twisted segments is shown as red line (f). The rotated direction of DNA fiber at ending in turned segment is shown as red line and the direction in turned-twisted segment is shown as blue line (g).

![human_Cell]({{"/assets/images/humanCell01.jpg" | relative_url}})
{: .text-left}

Left: The 3D geometry of the cell nucleus ( 14.2μm x 14.2μm x 5μm ) used in this macro file, showing the continuous fractal interior. Right: The beam geometry used in the simulation, showing the incident protons as a parallel beam.
## Particle source
A proton source plane with circle radius 7.1 um was located 3 μm from the cell center. 
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