## Mapping a trajectory into PIV-PathCV space

The simplest version of PathCV needs the specification of two reference configurations, and for each of them one can compute the PIV as follows

```plumed
PIV ...
LABEL=c1
PRECISION=1000
VOLUME=4.589575
REF_FILE=Liq.pdb
PIVATOMS=2
ATOMTYPES=OW1,HW
SORT=1,1,1
SWITCH1={RATIONAL R_0=0.4 MM=18 NN=4}
SWITCH2={RATIONAL R_0=0.4 MM=18 NN=4}
SWITCH3={RATIONAL R_0=0.4 MM=18 NN=4}
NLIST
NL_CUTOFF=0.6,0.6,0.6
NL_STRIDE=10,10,10
NL_SKIN=0.1,0.1,0.1
UPDATEPIV=10
... PIV


PIV ...
LABEL=c2
PRECISION=1000
VOLUME=4.589575
REF_FILE=Ih.pdb
PIVATOMS=2
ATOMTYPES=OW1,HW
SORT=1,1,1
SWITCH1={RATIONAL R_0=0.4 MM=18 NN=4}
SWITCH2={RATIONAL R_0=0.4 MM=18 NN=4}
SWITCH3={RATIONAL R_0=0.4 MM=18 NN=4}
NLIST
NL_CUTOFF=0.6,0.6,0.6
NL_STRIDE=10,10,10
NL_SKIN=0.1,0.1,0.1
UPDATEPIV=10
... PIV
```

here the PIV is computed using Hydrogen (HW) and Oxygen (OW) atoms as named in the Ih.pdb and Liq.pdb files. The PIV version of the example above uses distances scaled by the cubic root of the ratio between a reference volume (VOLUME=4.589575) and the volume of the cell along the trajectory. 

PIV-PathCV collective variables (s and z) can then be computed by adding to the plumed.dat file the following lines:

```plumed
p1: FUNCPATHMSD ARG=c1,c2 LAMBDA=0.0810475
PRINT ARG=c1,c2,p1.s,p1.z FILE=colvar.dat FMT=%15.6f
```

Compute the the values of the PIV-PathCV along the provided trajectory (traj.xtc) as a function of time using the plumed driver:

```plumed
plumed driver --mf_xtc traj.xtc --plumed plumed.dat
```
Please note that atoms need to be listed in the same order in all reference files and in the trajectory.
