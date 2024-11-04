## Associating PIVs to system configurations
The following example shows how to associate a PIV to a system configuration:

```plumed
PIV ...
LABEL=c1
PIVATOMS=1
ATOMTYPES=O
PRECISION=1000
REF_FILE=Liq.pdb
SORT=1
SWITCH1={RATIONAL R_0=0.4 MM=12 NN=4}
NLIST
NL_CUTOFF=1.2
NL_STRIDE=10
NL_SKIN=0.1
... PIV

PRINT ARG=c1 FILE=colvar.dat FMT=%15.6f
```

Oxigen atoms (ATOMTYPES=O) are used for the PIV construction, and neighbor lists (NLIST) are used for the calculation of atom-atom distances. Distances are then mapped into numbers from 0 to 1 usign a switching function (SWITCH1={RATIONAL R_0=0.4 MM=12 NN=4}) with a precision of $10^{-3}$ (PRECISION=1000). A complete description of all the keywords can be found [here](https://www.plumed.org/doc-v2.9/user-doc/html/_p_i_v.html).

When including the example above into a file (e.g. plumed.dat) and running 

```plumed
plumed driver --mf_pdb Ih.pdb --plumed plumed.dat
```
one gets the PIV distance between the configurations specified in the Ih.pdb and Liq.pdb files. Please note that the order of atoms in Ih.pdb and Liq.pdb files must be the same.

Check that if one computes the distance between two identical configurations the result is zero.
