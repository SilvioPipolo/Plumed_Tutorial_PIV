## Biasing a simulation in the PIV-PathCV space

The files Liq.pdb and Ih.pdb contain the configurations of 144-molecule liquid water and hexagonal ice boxes respectively (TIP4P model). One can use them to construct a PIV-PathCV space to be used for biasing a Classical Molecular MD through metadynamics and simulating the crystallisation of undercooled homogeneous liquid water.

In order to set up such a metadynamics run one needs to add the following line to the plumed.dat file

```plumed
METAD ARG=p1.s,p1.z SIGMA=0.02,50.0   HEIGHT=0.1 PACE=500   LABEL=res
```

and simulation box constraints to avoid too skewed cells:

```plumed
cell: CELL

LOWER_WALLS ARG=cell.ax AT=1.30  KAPPA=4000.0 LABEL=lax
LOWER_WALLS ARG=cell.by AT=1.30  KAPPA=4000.0 LABEL=lbx
LOWER_WALLS ARG=cell.cz AT=1.30  KAPPA=4000.0 LABEL=lcx
UPPER_WALLS ARG=cell.ax AT=2.00  KAPPA=4000.0 LABEL=uax
UPPER_WALLS ARG=cell.by AT=2.00  KAPPA=4000.0 LABEL=ubx
UPPER_WALLS ARG=cell.cz AT=2.00  KAPPA=4000.0 LABEL=ucx

LOWER_WALLS ARG=cell.ay AT=-0.5  KAPPA=1000.0 LABEL=lay
UPPER_WALLS ARG=cell.ay  AT=0.5  KAPPA=1000.0 LABEL=uay
LOWER_WALLS ARG=cell.az AT=-0.5  KAPPA=1000.0 LABEL=laz
UPPER_WALLS ARG=cell.az  AT=0.5  KAPPA=1000.0 LABEL=uaz

LOWER_WALLS ARG=cell.bx AT=-0.5  KAPPA=1000.0 LABEL=lby
UPPER_WALLS ARG=cell.bx  AT=0.5  KAPPA=1000.0 LABEL=uby
LOWER_WALLS ARG=cell.bz AT=-0.5  KAPPA=1000.0 LABEL=lbz
UPPER_WALLS ARG=cell.bz  AT=0.5  KAPPA=1000.0 LABEL=ubz

LOWER_WALLS ARG=cell.cx AT=-0.5  KAPPA=1000.0 LABEL=lcy
UPPER_WALLS ARG=cell.cx  AT=0.5  KAPPA=1000.0 LABEL=ucy
LOWER_WALLS ARG=cell.cy AT=-0.5  KAPPA=1000.0 LABEL=lcz
UPPER_WALLS ARG=cell.cy  AT=0.5  KAPPA=1000.0 LABEL=ucz

```

Finally the PRINT line of keywords needs to be updated in order to print out the bias potential

```plumed
PRINT ARG=c1,c2,p1.s,p1.z,res.bias STRIDE=500  FILE=colvar FMT=%15.6f
```

The biased MD can then be run with the GROMCS package 

```plumed
gmx grompp -f md.mdp -c Liq.pdb -p TIP4P.top -o meta.tpr
gmx mdrun -deffnm meta -plumed plumed.dat
```

input files md.mdp and TIP4P.top for gromacs are provided. A run of 24 hours on a 4-core standard laptop is enough to reproduce a crystallisation event.
