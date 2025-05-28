# Lindhard Reponse Function
## General remarks about the Lindhard Reponse Function in SIESTA
Tutorial on the LIndhard Response Function - Siesta[5.2]

The Lindhard Response Function in SIESTA is implemented under two approximations: plane-wave basis set and static limit. 

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

The electronic eigenvalues and corresponding k-point grid will be red from the siesta output files siesta.KP and siesta.EIG and further interpolated based on the keywords provided in the siesta.fdf file as an input to the lindhard executable. 

A prerequisite to generating these two files in the preliminary siesta run is to turn off time-reversal symmetry so as to have access to the full k-point grid (e.g. TimeReversalSymmetryForKpoints F).

At the end of the run, one should obtain a siesta.LINDHARD file with 3 columns: the first two will contain the information about the grid of q-points in the (a*,b*) plane determined by the keywords **Lindhard.ngridx** and **Lindhard.ngridy** (see below explanation), while the third will contain the actual response.

## Limitations
The current implementation does not run for spin-polarized systems.

The current implementation runs in the (a*,b*) plane while it collapses the sum along the third direction according to the number of slice (c* direction q-points) one inputs. 


## Keywords explained 

**Lindhard.Temperature 10 K** - Setting the temperature of the Fermi-Dirac distribution function.

**Lindhard.firstband	 23** - Setting the first electronic band to be accounted for in the integration, usually it is enough to account for the first band that is crossing the Fermi level.

**Lindhard.lastband	     25** - Setting the last electronic band to be accounted for in the integration, usually it is enough to account up to the last band that is crossing the Fermi level.

**Lindhard.ngridx		64** - Number of points used for interpolating the k-point grid along the x-axis, this will be your equivalent q-point grid along a* printed in the siesta.LINDHARD output in the first column.

**Lindhard.ngridy		72** - Number of points used for interpolating the k-point grid along the y-axis, this will be your equivalent q-point grid along b* printed in the siesta.LINDHARD output in the second column.

**Lindhard.ngridz		 4** - Number of points used for interpolating the k-point grid along the z-axis.

**Lindhard.nq1		4** - Every nth point along a-axis will be printed in the siesta.LINDHARD. This option is useful only if you want to print less points than the grid you use for interpolation (for example here you print every 4th point).

**Lindhard.nq2		4** - Every nth point along b-axis will be printed in the siesta.LINDHARD.

N.B. All the Lindhard grid points need to be even numbers.

## Tutorial exercises
This tutorial is made up of two parts. You have access to the necessary minimal files to redo the calculations.

### 1.Atomic H chain 

The point of this first tutorial is to self-check that in-fact the half-filled electronic band of an atomic H chain gives exactly the Fermi nesting wave vector $'2k_F = \pi/a'$, as in half of the length of the reciprocal wave vector, corresponding to the half-filling of the band.

Go ahead and enter the **H_chain** folder. Download  the fdf, KP and EIG files and run locally **lindhard < h_chain.fdf**. Inspect the output file. Feel free to modify the keywords at your own will and follow how the position of the maximum converges with the k-point and q-point grids. Change the temperature and follow the maximum evolution . A simple linux command to look for the maximum in the output file is to run, for example: **sort -rk3 h_chain.lindhard | head -n 10**, to see the 10th largest value of the response.

### 2.Blue Bronze (K0.3MoO3)

The point of this tutorial is to understand how to use the code when multiple bands are crossing the Fermi level, now in a real material. 

Please feel free to download the fdf, KP and EIG files and run locally **linhard < bluebronze.fdf**. Feel free to modify the keywords at your own will and follow how the position of the maximum converges with the q-point grid.

In order to obtain the full q-point map, you can now run locally by modifying the (a*,b*) in-plane grid, for example change to:

>Lindhard.ngridx		64
>
>Lindhard.ngridy    	64
>
>Lindhard.ngridz		 2

on the two bands crossing the Fermi level (160 and 161).

You can see the results using gnuplot or python or other prefered software. 

In gnuplot, you can simply run:

>set palette defined (0 "black", 0.5"blue",0.75"white", 1.00"red")
>
>set view map
>
>sp 'bluebronze.lindhard' u 1:2:3 w p ps 3 lc palette  t ''
>


