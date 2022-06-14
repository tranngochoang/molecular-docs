---
layout: default
title: Bacterial Cell
nav_order: 2
permalink: docs/examples/bacterial-cell
parent: Examples
---

# Bacterial cell (ecoli.mac)

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview
This example that we investigated is the E. coli bacterium geometry, which imitates the genome of the bacterium.

## Geometry
The genome has been produced using four side-by-side Hilbert curve fractals [fractalDNA]({{"http://natl.github.io/fractaldna/" | relative_url}}). This creates 16383 placement volumes that are assumed to be cubic boxes with a side length of 50 nm. This was composed of 3,600 straight segments, and 5,652 turned segments of DNA. We only placed placement volumes that fell inside an ellipsoid with a semi-major axis of 950 nm and two equal semi-minor axes of 400 nm, creating an elliptical geometry that corresponded roughly to the dimensions of an E. coli bacterium. The final geometry (Figure) contained 4.63 Mbp, similar again to the length of an E. coli genome. 


```
/world/worldSize 8 um
/dnageom/setSmartVoxels 20

/dnageom/radicalKillDistance 6 nm
/dnageom/interactionDirectRange 6 angstrom

/dnageom/placementSize 50 50 50 nm
/dnageom/fractalScaling 50 50 50 nm

/dnageom/definitionFile geometries/bacteria-XFXFXFX-4.txt
/dnageom/placementVolume turn geometries/4strands_50nm_turn.txt
/dnageom/placementVolume turntwist geometries/4strands_50nm_turn.txt true
/dnageom/placementVolume straight geometries/4strands_50nm_straight.txt
```

![ecoli]({{"/assets/images/ecoliImage.png" | relative_url}})
{: .text-center}

## Particle source
Electrons are simulated coming from an ellipse enclosing the bacterial cell (of the same dimensions as the cell) with energy 1 MeV. The angular distribution of electron trajectories coming from the cell surface follows a cosine law, which simulates an isotropic radiation environment.
```
/gps/pos/type Surface
/gps/pos/shape Ellipsoid
/gps/pos/centre 0 0 0 nm
/gps/pos/halfx 950 nm
/gps/pos/halfy 400 nm
/gps/pos/halfz 400 nm
/gps/ang/type cos
/gps/particle e-
/gps/energy 9.999 keV
/run/beamOn 1000
```
## Damage Model
Direct damage model uses the 17.5 eV for lower and upper break threshold. The probability of 42% for the production of strand break by OH (OH● + 2-deoxyribose) was applied.
```
/dnadamage/directDamageLower 17.5 eV
/dnadamage/directDamageUpper 17.5 eV

/dnadamage/indirectOHBaseChance 1.0
/dnadamage/indirectOHStrandChance 0.42
/dnadamage/inductionOHChance 0.05

/dnadamage/indirectHBaseChance 1.0
/dnadamage/indirectHStrandChance 1.0
/dnadamage/inductionHChance 0.00

/dnadamage/indirectEaqBaseChance 1.0
/dnadamage/indirectEaqStrandChance 1.0
/dnadamage/inductionEaqChance 0.00
```

## Results
Output [analysis]({{"docs/overview/results-and-analysis"| relative_url}}) is analysed by using ecoli.C macro file. 

![ecoli]({{"/assets/images/ecoli.png" | relative_url}})
{: .text-left}

![ecoli]({{"/assets/images/ecoli_Fra.png" | relative_url}})
{: .text-left}