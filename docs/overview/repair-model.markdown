---
layout: default
title: Repair model
nav_order: 7
parent: Overview
---
# Repair model

This model calculates the accumulated proteins yield, by considering four principal DSB repair pathways. 

These pathways are [1]: 
- non-homologous end-joining (NHEJ),
- homologous recombination (HR), 
- single-strand annealing (SSA), and 
- alternative end-joining mechanism (Alt-NHEJ). 

The number of non-repairable DSB/Gy/cell is needed (NcDSB), as well as the number of DSBs that is more probable to be repaired (NncDSB). More analytically:

![repair model]({{"/assets/images/repairMode.png" | relative_url}})
{: .text-center}


Where: 
- N0 is the total numbe of DSB (NncDSB + NcDSB). 
- VNHEJ, VHR, VSSA and VmicroSSA are mathematical variables that characterize the way that each model affects 
the way that DSBs are repaired. 
- D is the dose (Gy). 
- a(L) is the slope coefficient of linear dose dependence that describes DSB induction per unit of dose (Gy−1/cell) and depends on LET. 

## Reference
[1] Performance Evaluation for Repair of HSGc-C5 Carcinoma Cell Using Geant4-DNA, D. Sakata et al., Cancers, vol. 13, p. 6046, 2021.