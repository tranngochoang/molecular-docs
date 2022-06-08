---
layout: default
title: Running from Source
nav_order: 5
---

# Running from source
{: .no_toc }

Geant4.11.1beta or higher is requested [Geant4]({{ "https://geant4.web.cern.ch" | relative_url }}). 

To build the example:

```
mkdir build
cd build
cmake ../pathToExamples/moleculardna
make
```
This example needs internet to download the pre-existing geometry data file. Please, check your connection. 

To run the example:
```
./molecular -m cylinders.mac -t 2 -p 2
```

-m : macro file [examples]({{ "/docs/examples/parameter-study" | relative_url }})

-t : number of threads to run

-p : physics list option [physics-model]({{ "/docs/overview/physics-model" | relative_url }})
