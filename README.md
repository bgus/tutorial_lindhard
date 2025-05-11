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

**Lindhard.lastband	     25** - Setting the last electronic band to be accounted for in the integration, usually is enough to account up to the last band that is crossing the Fermi level.

**Lindhard.ngridx		64** - Number of points used for interpolating the k-point grid along the x-axis.

**Lindhard.ngridy		72** - Number of points used for interpolating the k-point grid along the y-axis.

**Lindhard.ngridz		 4** - Number of points used for interpolating the k-point grid along the z-axis.

**Lindhard.nq1		3** - Every nth point along a-axis will be printed in the siesta.lindhard

**Lindhard.nq2		4** - Every nth point along b-axis will be printed in the siesta.lindhard

## Tutorial exercises
This tutorial is made up of two parts. You will have access to the necessary minimal files to redo the calculations.

### 1.Atomic H chain 

The point of this first tutorial is to self-check that in-fact the half-filled electronic band of an atomic H chain gives exactly the Fermi nesting wave vector $'2k_F = 0.5 a*'$, as in half of the length of the reciprocal wave vector, corresponding to the half-filling of the band.

Go ahead and enter the **H_chain** folder. Download  the fdf, KP and EIG files and run locally **lindhard < h_chain.fdf**. Feel free to modify the keywords at your own will and follow how the position of the maximum converges with the k-point and q-point grids. Change the temperature and follow the maximum evolution . A simple linux command to do is to run, for example: **sort -rk3 h_chain.lindhard | head**

### 2.Blue Bronze (K0.3MoO3)
