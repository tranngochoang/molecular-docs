---
layout: default
title: Results and Analysis
permalink: /docs/overview/results-and-analysis
nav_order: 2
parent: Overview
---
<!-- Need to import MathJax for this post -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<!-- END MathJax Import -->


# Results and Analysis
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Implementation Overview

As the simulation runs, it keeps track of three main elements in relation to DNA damage.
- Energy depositions in each chromosome (To-do: Add track length)
- Energy Depositions and track length in the cell (when specified)
- DNA Damage in the DNA geometry

At the end of each event, the DNA Damage events are collected and analysed, reconstructing the
damage pattern in the DNA and assigning it a complexity.

In the damage model, a probability is assigned that certain events cause strand breaks
(i.e. $$ Pr(\ce{e^{-}_{aq}} + \mathrm{Sugar} \rightarrow \mathrm{SSB}) $$). These conditions
are tested at the end of each event when the analysis runs to determine the damage that occurs.

At the completion of the run, the following outputs are saved:

### Histograms

- foobar
- barfoo

### Tuples

- Foo
  1. Bar
  1. Baz
  1. Box

- Coo
  1. Dar
  1. Daz
  1. Dox



## Damage Classification Model



## Output Format

