---
layout: default
title: DNA Placements
nav_order: 2
permalink: docs/geometry-library/dna-placements
parent: Geometry Library
---

The DNA Placements here were built using the [FractalDNA]({{site.url}}/docs/geometry-library/fractal-dna)
package in Python. Accompanying each geometry is the Python code to
generate it.

## Single DNA Segments

Straight and Turned Segments for a 50nm box.

* Straight Segment ([link]({{"assets/csv/50nm_straight.csv" | relative_url}}))
* Turned Segment ([link]({{"assets/csv/50nm_turn.csv" | relative_url}}))
* Turned Segment with 90° rotation ([link]({{"assets/csv/50nm_turn_twist.csv" | relative_url}}))

_Generating Code_
```.py
from fractaldna.dna_models import dnachain
import numpy as np
bp_separation  = dnachain.BP_SEPARATION  # 3.32Å
side_length_nm = 50  # nm
num_basepairs_straight = int( side_length_nm / (0.1*bp_separation) )
num_basepairs_turned = int((side_length_nm * np.pi / 4.) / (0.1*bp_separation))

chain_straight = dnachain.DNAChain(
    ''.join(np.random.choice(['G', 'A', 'T', 'C'], num_basepairs_straight))
)

chain_turned = dnachain.TurnedDNAChain(
    ''.join(np.random.choice(['G', 'A', 'T', 'C'], num_basepairs_turned))
)

chain_turned_twisted = dnachain.TurnedTwistedDNAChain(
    ''.join(np.random.choice(['G', 'A', 'T', 'C'], num_basepairs_turned))
)

chain_straight.to_frame().to_csv('50nm_straight.csv', sep=' ')
chain_turned.to_frame().to_csv('50nm_turn.csv', sep=' ')
chain_turned_twisted.to_frame().to_csv('50nm_turn_twist.csv', sep=' ')
```
