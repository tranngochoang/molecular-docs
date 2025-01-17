---
layout: default
title: Damage Model
nav_order: 2
parent: Overview
permalink: /docs/overview/damage-model
---
<!-- Need to import MathJax for this post -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!-- END MathJax Import -->

# Damage Model
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Direct Damage

Direct Damage occurs when energy from physical processes is deposited near a DNA molecule.
In Molecular DNA, we associate damage either with a 'strand' molecule (sugar or phosphate placement) 
or a base molecule.

The maximum distance from the centre of a molecule which can result in any energy deposition tied to that model
is called the direct interaction range and can be set using `dnageom/interactionDirectRange`.

To assign damage, the program looks up all molecules with the direct interation range of a given energy deposition
and assigns the damage to the closest molecule.

![Direct Damage is assigned to the closest molecule within a set radius]({{"/assets/images/dna-damage.png" | relative_url }})
{: .text-center}

In the literature direct strand break damage models typically take the sum of the energy depositions in the sugar-phosphate
part of the DNA strand and calculate the chance of a break based on the energy deposition.
We simulate this using the `/dnadamage/directDamageLower` and `/dnadamage/directDamageUpper` commands.
Essentially:

* Energy Deposition below directDamageLower never causes a break
* Energy Deposition above directDamageUpper always causes a break
* Between these bounds, the likelihood of a break rises uniformly

The likelihood of a break, for a lower bound of 5eV and an upper bound of 37.5eV is shown below

![Linearly increasing damage likelihood for physical damage]({{"/assets/images/break-chance.png" | relative_url}}){: width="300px"}
{: .text-center}

Some models assume a step likelihood function for physical damage. This can be modelled by setting `/dnadamage/directDamageLower` and `/dnadamage/directDamageUpper` to the same value.

## Indirect Damage

Indirect Damage is scored when a chemical reaction leads to a strand break.
The chemical reactions between radicals and DNA elements themselves are defined in the
[Chemistry Model]( {{ "docs/overview/chemistry-model" | relative_url }} ) through the `MolecularChemistryList` class.

The phosphate part of the sugar-phosphate backbone rarely takes part in reactions
(reactions between radicals and phosphate are not even defined in the simulation),
so the main factors in the indirect damage model are the likelihoods that a reaction
between a radical and the DNA backbone lead to a single strand break (SSB).

Each probablity is defined through the macro interface as below

| Reaction                                                              | Macro Command                        |
|:----------------------------------------------------------------------|:-------------------------------------|
| $$ Pr(\ce{e^{-}_{aq}} + \mathrm{Sugar} \rightarrow \mathrm{SSB}) $$   | `/dnadamage/indirectEaqStrandChance` |
| $$ Pr(H^{\bullet} + \mathrm{Sugar} \rightarrow \mathrm{SSB}) $$       | `/dnadamage/indirectHStrandChance`   |
| $$ Pr(\ce{^{\bullet}OH} + \mathrm{Sugar} \rightarrow \mathrm{SSB}) $$ | `/dnadamage/indirectOHStrandChance`  |


Base Damage is modelled through a similar interface, though two steps are provided for the modelling of both
base damage generally, and also strand break induction (while this might seem redundant, it was coded for a level of flexibility).

For a given base, we can consider seperately the likelihood that
the chemical reaction between the base and the radical
causes damage to the base pair, and the likelihood it causes a strand break.
In the case of $$\ce{^{\bullet}OH}$$ `/dnadamage/indirectOHBaseChance 0.5` would
set the likelihood that the simulation should consider a reaction between
$$\ce{^{\bullet}OH}$$ and a base as damage as 50%. If base damage does occur,
`/dnadamage/inductionOHChance 0.4` would mean that following base damage, the chance
of that damage causing an SSB is 40%. *Note that these are dependent events, so the likelihood*
*of the reaction causing an SSB is 20%*.

For most work, you would probably consider all chemical reactions with a base as base damage,
but assume these don't lead to SSBs. This requires the following settings for all radicals:

```
/dnadamage/indirectOHBaseChance 1.0
/dnadamage/inductionOHChance 0.00
```


## Radical Scavenging

One of the most important parameters in the simulation is `/dnageom/radicalKillDistance`
which specifies the spatial region in which we calculate chemistry.
This parameter is complimentary with what other simulations would model as scavenging or
an early simulation cut-off time, in that it is linked to the distance a radical is expected
to diffuse before the simulation ends.

In particular, for a radical with a diffusion constant $$D_c$$, we expect it to diffuse a
distance $$\bar{x}$$ in time $$t$$ as follows:

$$\bar{x} = \sqrt{6D_ct} $$

For the $$\ce{^{\bullet}OH}$$ radical ($$D_c=2.8\times 10^{-9}m^2s^{-1}$$), this
gives $$\bar{x} = 4.09 \sqrt{t} \ \mathrm{nm} $$. Typically for simulations in Molecular DNA,
this means that a radical kill distance of 4nm-6nm yields reliable results, while larger radical kill
distances would require scavenging to be more broadly implemented.

