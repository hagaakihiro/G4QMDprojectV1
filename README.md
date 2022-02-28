# G4QMDprojectV1 - 20211201 version

We developed the QMD model in Geant4 by implementing modern Skyrme interaction parameter sets as well as by incorporating with an ad-hoc $\alpha$ cluster model in the initial nuclear state. The details can be described in ***.

This is developed based on the original QMD model in Geant4.10.07 Patch01 located at

geant4.10.07.p01-install/source/processes/hadronic/models/qmd/

, which is composed of eight source files,

- G4QMDCollision.cc
- G4QMDGroundStateNucleus.cc
- G4QMDMeanField.cc
- G4QMDNucleus.cc
- G4QMDParameters.cc
- G4QMDParticipant.cc
- G4QMDReaction.cc
- G4QMDSystem.cc

and the corresponding eight include files. Here, we denote briefly the development in each file.

## 1: Local(G4)QMDCollision.cc 
This code simulates nucleon-nucleon collisions of all paticipant in inelastic nuclear collision during time evolution.
In the present version, we modified two parts; for a treatment of short-lived particles (e.g. delta particle) and for the evaluation of energy conservation violation during nucleon-nucleon collision in matteer.

### 1-1: A short-lived particle 
Original code; when a short-lived particle (delta particle etc.) is produced in the nucleon-nucleon collision phase, the energy conservation is violated, due to the off-shell mass (original code uses on-shell mass). Tentatively we employ a short-lived particle as a decay mode, namely, a short-lived particle is immediately decayed if it is produced. This does not reflect the nature, but in the hadron therapy energy range, its contribution might be negligible, and we tentatively employ this handling.

### 1-2: Evaluation of energy conservation
G4 Nucleon-nucleon collision ( G4Scatterer ) employed in G4QMD is free one, but in actual situation, the collision is occured in medium (mutually inteacting among the participant nucleons). The nucleon-nucleon collision changes the momuentum, however, this change may violate the energy conservation during the collision due to the presence of the otehr nucleons. Therefore, the collision which violate the energy conservation of the system is wasted and agin the collision is tried till the conservation criteria is satisfied. To measure the total energy in the system, in the original code, non-relativistic version has been employed. In our developed version, the Lorentz covariant version is used for the consistency of the whole simulation in QMD.

## 2: Local(G4)GroundStateNucleus.cc 
This code creats the initial ground state nucleus entried in inelastic nuclear scattering.
We developed $\alpha$ cluster model in this code. Also some modifications the position/momentum sampling of nucleons are performed.

### 2-1: Ad hoc $\alpha$ cluster model
If the entryed nucleus is $^{12}$C or $^{16}$O, the nucleon positions are sampled with $\alpha$ cluster model
using "samplingPosition_cluster" function (for detail, see [1]).

### 2-2: Ad hoc $\alpha$ cluster model



## 3: Local(G4)MeanField.cc 

## 4: Local(G4)Nucleus.cc 

## 5: Local(G4)Parameters.cc 

## 6: Local(G4)Participant.cc 

## 7: Local(G4)Reaction.cc 

## 8: Local(G4)System.cc 
