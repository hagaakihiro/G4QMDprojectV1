# G4QMDprojectV1 - 20211201 version

We developed the QMD model in Geant4 by implementing modern Skyrme interaction parameter sets as well as by incorporating with an ad-hoc $\alpha$ cluster model in the initial nuclear state. The details can be described in [1].

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

### 2-2: Others
Parameter "radam" is used in the sampling of the nucleon position. In original code, this is calculated as radm = radious - rada * ( gamm - 1.0 ) + radb, and this gives radm = radious in the original JQMD parameter set. In the developed version, we used radm = radious directly, because the rest terms contribute to the radm in general Skyrme parameter sets, which the stable sampling makes difficult.
In addition, we ceals to evalute the single energy of nucleons in the momuntum sampling.

The nuclear ground state is formed as the experimental binding energy is satistied within a certain threshold. In this evaluation, the Lorentz covariant version is also used.

## 3: Local(G4)MeanField.cc 
This code simulates the system dynamics with mean field potential.
We added the new paramters to allow to simulate with the general Skyrme interaction.
In addition, the functions "CalDensityProfile" and "CalChargeDensityProfile" to calculate are added to calculate the expectation values of the system raius and charge radius, respectively, and the functions "GetSingleEnergy" and "GetTotalEnergy" are added to calculate the nucleon energy and total energy, respectively in the mean field potential.

## 4: Local(G4)Nucleus.cc 
This code simulate the excitated nucleus as well as the ground state nucleus.
Here, we added the new paramters to allow to simulate with the general Skyrme interaction.
In addition, the Lorentz covariant version is also used in the evaluation of the excitation energy.

## 5: Local(G4)Parameters.cc 
This code indicates the parameters in the model employed.
We added 3 parameter sets, (SLy4, SkM*, and SIII) as well as the original JQMD one.
Please use each parameter set by inserting or removing the comment out.

## 6: Local(G4)Participant.cc 
Not changed in the present version.

## 7: Local(G4)Reaction.cc 
This code manages inelastic nuclear collistion in QMD. 
The modifications in this version are 1) to add system->clear() in line 735, which saves the unnatural proton diplication in trial loop in line 236, and 2) to allow the simulation of nucleon-nucleon and pion-nucleon scattering with this code.

## 8: Local(G4)System.cc 
Not changed in the present version.
