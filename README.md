# BetaShape ![LNHB logo](http://www.lnhb.fr/img/logo-lnhb.png, height="50%", width="50%")
The BetaShape program calculates **beta and electron capture decays**, and provides for each transition: 
* Energy spectra of the emitted &beta; and &nu; particles.
* Capture probabilities and capture-to-positron ratios for all subshells.
* Average &beta; and &nu; energies.
* log-_ft_ values.
* In case of multiple branches, total decay spectra are also generated for each type of particles. 

All results are provided as formatted text files, including updated ENSDF files and CSV files.

BetaShape is part of the [ENSDF Analysis and Utility Programs](https://nds.iaea.org/public/ensdf_pgm/). 
It is also made available on [LNHB website](http://www.lnhb.fr/rd-activities/spectrum-processing-software/) as part of the Utility Programs of the [Decay Data Evaluation Project (DDEP)](http://www.lnhb.fr/nuclear-data/nuclear-data-table/). 
Any question can be addressed to Xavier Mougeot: xavier.mougeot@cea.fr

## Downloads
The **packages** directory contains the executables for Windows (10), macOS (Monterey M1 and Intel) and Linux (CentOS 8, Ubuntu 20.04.2 LTS, Scientific Linux 6.4).

## Quick start

The program takes as input a formatted ENSDF file, for example [Ni63.txt](http://www.lnhb.fr/nuclides/Ni-63.txt) for <sup>63</sup>Ni decay. With default options, it is simply run in Windows typing: 
```
C:\...> betashape Ni63.txt
```
Running the benchmark calculations is recommended at first use of the program:
```
C:\...> mybench.bat
```
Various options are available. In the previous example, one can ask in addition for an update of the Q-value (from AME2020), a &beta; spectrum with a constant energy step of 0.5 keV, the corresponding &nu; spectrum, and a CSV file:
```
C:\...> betashape Ni63.txt -qval myEstep=0.5 nu=1 -csv
```
More information can be found in the [Readme.txt](http://www.lnhb.fr/software/BetaShape_ReadMe.txt) file within the package. 

## Citations
**Beta decays**: [X. Mougeot, Applied Radiation and Isotopes 201, 111018 (2023)](https://doi.org/10.1016/j.apradiso.2023.111018)

**Electron captures**: [X. Mougeot, Applied Radiation and Isotopes 154, 108884 (2019)](https://doi.org/10.1016/j.apradiso.2019.108884)

## Change history
#### Version 2.3 (2023/09)
Following the [24<sup>th</sup> NSDD meeting](https://conferences.iaea.org/event/323/) held at the Australian National University in Canberra (24-28 October 2022) and further discussions, the changes below have been implemented.
* Provision of:
  - __*f*-values__ in CSV files.
  - __mean energy of the emitted neutrinos__ in CSV files.
  - __experimental shape factors__ in updated ENSDF files.
* **Rounding limit** can be changed via the option `unc_digit=X` with `X` from 1 to 99 (50 by default).
* Handling of __non-numeric uncertainties__ (`LT`, `GT`, `LE`, `GE`, `AP`, `CA`, `SY`), and __asymmetric uncertainties__ (with the `-asym` option) via the Min-Max method.
* Modification of __forbiddenness assignment__
  * Initial and final J<sup>&pi;</sup> unambiguously defined: single J, single &pi; for each level, `()` and `[]` accepted.

    &rarr; Allowed or forbidden unique transition treated correctly.

    &rarr; Forbidden non-unique transition treated as transition of same &Delta;J ignoring spin change (also known as &xi;-approximation)
    * 1<sup>st</sup> forbidden non-unique as allowed.
    * 2<sup>nd</sup> forbidden non-unique as 1<sup>st</sup> forbidden unique.
    * 3<sup>rd</sup> forbidden non-unique as 2<sup>nd</sup> forbidden unique.
    * etc.
  * Initial and final J defined but at least one parity undefined.

    &rarr; Transition treated according to the &xi;-approximation.
  * Otherwise, transition treated as allowed: initial and final J undefined; unplaced transitions; several J or &pi; in at least one level.
* Handling of __branching ratios__
`BR` and `NB` from N and PN records are taken into account to determine the normalization factor, and their uncertainties are propagated.

_Nota Bene_: For an EC/B+ transition, the splitting of the branch is calculated and the EC and B+ intensities are updated. Their uncertainties do include the uncertainty on the normalization factor. There is a risk of inconsistency because of multiple counting:
  * If the uncertainty on the normalization factor includes the uncertainties on the intensities, and vice-versa.
  * If the code is run several times on the updated dataset.

## Disclaimer
Neither the author nor anybody else makes any warranty, express or implied, or assumes any legal liability or responsibility for the accuracy, completeness or usefulness of any information disclosed, or represents that its use would not infringe privately owned rights.
