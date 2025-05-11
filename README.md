# Lindhard Reponse Function
## General remarks about the Lindhard Reponse Function
Tutorial on the LIndhard Response Function - Siesta[5.2]

The Lindhard Response Function in SIESTA is implemented under two approximations: plane-wave basis sets and static limit. 

```math
\begin{equation}
\chi(q)=-\sum_{i,j}\sum_{k}\frac{f_F(\epsilon_i({k}))-f_F(\epsilon_j({k}+{q}))}{\epsilon_i({k})-\epsilon_j({k}+{q})},
\end{equation}
```

where $`\textit {f}_F`$ is the Fermi-Dirac distribution function defined as:

```math
\begin{equation}
    f_F(\epsilon_i({k})) = \frac{1}{e^{(\epsilon_i({k})-\epsilon_F)/k_BT}+1}
\end{equation}
```

The electronic eigenvalues and corresponding k-point grid will be red from the siesta output file siesta.KP and siesta.EIG and further interpolated based on the keywords provided in the siesta.fdf file as an input to the lindhard executable. 

A prerequisite to generating these two files in the preliminary siesta run is to turn off time-reversal symmetry so as to have access to the full k-point grid: TimeReversalSymmetryForKpoints F .

## Limitations
The current implementation does not run for spin-polarized systems.

The current implementation runs in the (a*,b*) plane. 


## Keywords explained 

**Lindhard.Temperature 10 K** - Setting the temperature of the Fermi-Dirac distribution function.

**Lindhard.firstband	 23** - Setting the first electronic band to be accounted for in the integration, usually is enough to account for the first band that is crossing the Fermi level.

**Lindhard.lastband	 64** - Setting the last electronic band to be accounted for in the integration, usually is enough to account up to the last band that is crossing the Fermi level.

**Lindhard.ngridx		32** - Number of points used for interpolating the k-point grid along the x-axis.

**Lindhard.ngridy		32** - Number of points used for interpolating the k-point grid along the y-axis.

**Lindhard.ngridz		32** - Number of points used for interpolating the k-point grid along the z-axis.

**Lindhard.nq1		1** - Every nth point along a-axis will be printed in the siesta.lindhard

**Lindhard.nq2		1** - Every nth point along b-axis will be printed in the siesta.lindhard

## Tutorial exercises
This tutorial is made up of two parts:

1.Atomic H chain 

You will have access to the necessary minimal files 

2.Blue Bronze (K0.3MoO3)
