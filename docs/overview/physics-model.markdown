---
layout: default
title: Physics Model
nav_order: 2
parent: Overview
---

# Physics model

Geant4-DNA Monte-Carlo track-structure code describes spatial distribution of energy depositions, interaction types in material of biological interest (water, DNA,...) based on interaction probabilities (cross sections). Geant4-DNA physics processes and models have been built in physics constructors which are designed to activate required physical models in a single command line. 

![physics]({{"/assets/images/DNAPhysics.mp4" | relative_url}})
{: .text-center}

G4EmDNAPhysics_option2, G4EmDNAPhysics_option4 or G4EmDNAPhysics_option6 constructors are recommended to use in molecularDNA example. Water material is filled whole simulation geometries (even DNA). 

Please refer [Geant4-DNA]({{ "http://geant4-dna.in2p3.fr/styled-3/styled-8/index.html" | relative_url }}) for details
