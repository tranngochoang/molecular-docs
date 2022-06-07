---
layout: default
title: Chemistry Model
nav_order: 4
parent: Overview
---

# Time Step Models

Time step models describe an action (reaction or diffusion) of radio-induced reactive species during a discretized time step. In the MolecularDNA example, the time step models determinate a competition between free radical species recombination and indirect DNA damages.
## Table of contents
{: .no_toc .text-delta }

## Synchronous IRT method

The IRT method is based on the “Independent Pair Approximation”; thus, reactive pairs are assumed independent, that is, the reaction time between any reactant pairs does not depend on the other reactants present in the medium. Under this assumption, the reaction time is sampled from the reaction probability distributions of the reactant pairs that mainly depend on initial pair distance. The IRT method determines the minimum time to the next reaction. Reactive products created by reactions that have occurred can undergo reactions with other reactants. These new reactions then need to be considered and included in the possible reactions.

While this is a considerable advantage in terms of computing time, the spatial–temporal information of the system is not simulated explicitly. As a complementary extension, synchronous IRT (or IRT-syn) implementation calculates a time step using IRT method for the next reaction that should occur. The reactive products created in this reaction and the remaining molecules are considered explicitly together to diffuse for the time step. Then, based on their new positions, the new random reaction times are re-evaluated sequentially for all the radicals in the system and the new minimum reaction time and corresponding reaction is selected for next time step. This procedure is repeated until the end time of simulation.

## Reaction rates between free radicals and the DNA
Indirect damage occurs from the chemical reaction between a radical and a DNA molecule (see the table below). To induce indirect strand breaks, the chemical reaction occurs between the •OH radical and the 2-deoxyribose-phosphate group. The probablities to induce a single strand break are described in the
[Indirect Damage]( {{ "docs/overview/damage-model" | relative_url }} ) through `DamageModel` class.

| Reaction                                      | Reaction rate (109 M-1s-1)[1] |
|:----------------------------------------------|:------------------------------|
| 2-deoxyribose + OH●                           | 1.8                           |
| Adenine + OH●                                 | 6.1                           |
| Guanine + OH●                                 | 9.2                           |
| Thymine + OH●                                 | 6.4                           |
| Cytosine + OH●                                | 6.1                           |
| 2-deoxyribose + e-aq                          | 0.01                          |
| Adenine + e-aq                                | 9.0                           |
| Guanine + e-aq                                | 14.0                          |
| Thymine + e-aq                                | 18.0                          |
| Cytosine + e-aq                               | 13.0                          |
| 2-deoxyribose + H●                            | 0.029                         |
| Adenine + H●                                  | 0.10                          |
| Thymine + H●                                  | 0.57                          |
| Cytosine + H●                                 | 0.092                         |


The chemistry stage is simulated until 1 microsecond (by default). Users can decide the end time by using :
```
/scheduler/endTime 4 ns # set 4 nanosecond at which the simulation stops
```

To print reactions
```
/scheduler/verbose 1
```
## Reference 

1. Buxton GV, Greeanstock CL, Helman WP, Ross AB. Critical review of rate constants for reactions of hydrated electrons, hydrogen atoms and hydroxyl radicals (·OH/·O-) − in aqueous solution. J Phys Chem Ref Data. 1988;17:513–886.