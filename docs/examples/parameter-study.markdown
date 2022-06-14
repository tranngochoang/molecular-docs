---
layout: default
title: Parameter Study
nav_order: 1
permalink: docs/examples/parameter-study
parent: Examples
---

# Parameter Studies (cylinders.mac)

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview
The simulation geometry based upon a past parameter study[1] of direct and indirect DNA damage yields in straight DNA fibres to study the impacts of the different parameters. 
## Geometry
The geometry for parameter sweeps consists of a 3 μm sphere filled with 200.000 individual 216bp long straight DNA segments in a 100×30×30 nm placement volume. Radical kill distance [Damage Model]( {{ "docs/overview/damage-model" | relative_url }} )  was set to 9 nm, as well as the range for direct interaction was set to 7 A

```
/world/worldSize 10200 nm
/cell/radiusSize 3 3 3 um

/dnageom/setSmartVoxels 1
/dnageom/checkOverlaps false

/dnageom/radicalKillDistance 9 nm
/dnageom/interactionDirectRange 7 angstrom

/dnageom/placementSize 30 30 100 nm
/dnageom/fractalScaling 1 1 1 nm
/dnageom/definitionFile geometries/prisms200k_r3000.txt
/dnageom/placementVolume prism geometries/straight-216-0.txt

/dnageom/setVoxelPlacementAnglesAsMultiplesOfPi false
/dnageom/useCustomMoleculeSizes false
```

![cylinders]({{"/assets/images/cylinderImage.png" | relative_url}})
{: .text-center}

## Particle source
Primary electrons are generated randomly, with a random direction in a smaller 500 nm sphere in the centre of the test region. The primary particles with energies no greater than 4.5 keV cannot escape the larger spherical region, and all primaries see an equivalently random region.
```
/gps/particle e-
/gps/ang/type iso
/gps/energy 4.5 keV
/gps/pos/type Volume
/gps/pos/shape Sphere
/gps/pos/radius 500 nm
/gps/pos/centre 0 0 0 nm
/run/beamOn 2
```
## Damage Model
Direct damage model uses the 17.5 eV for lower and upper break thresholds. 
```
/dnadamage/directDamageLower 17.5 eV
/dnadamage/directDamageUpper 17.5 eV

/dnadamage/indirectOHBaseChance 1.0
/dnadamage/indirectOHStrandChance 0.65
/dnadamage/inductionOHChance 0.0

/dnadamage/indirectHBaseChance 1.0
/dnadamage/indirectHStrandChance 0.65
/dnadamage/inductionHChance 0.00

/dnadamage/indirectEaqBaseChance 1.0
/dnadamage/indirectEaqStrandChance 0.65
/dnadamage/inductionEaqChance 0.00
```
## Results
Output [analysis]({{"docs/overview/results-and-analysis"| relative_url}}) is analysed by using cylinders.C macro file.



## Reference
1. Nikjoo, H., O’Neill, O., Goodhead, T., & Terrissol, M. 1997, Computational modelling of low-energy electron-induced DNA damage by early physical and chemical events, International Journal of Radiation Biology, 71, 467