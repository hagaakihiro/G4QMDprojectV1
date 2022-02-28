# G4QMDprojectV1 - 20211201 version

## 1: Model description
We developed the QMD model in Geant4 by implementing modern Skyrme interaction parameter sets as well as by incorporating with an ad-hoc $\alpha$ cluster model in the initial nuclear state. The details can be described in ***.

This is developed based on the original QMD model in Geant4.10.07 Patch03, which is composed of eight source files,

- G4QMDCollision.cc
- G4QMDGroundStateNucleus.cc
- G4QMDMeanField.cc
- G4QMDNucleus.cc
- G4QMDParameters.cc
- G4QMDParticipant.cc
- G4QMDReaction.cc
- G4QMDSystem.cc

and the corresponding eight include files. Here, we denote briefly the development in each file.


