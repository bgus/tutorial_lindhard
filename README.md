# Tutorial Lindhard Reponse Function
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

The current implementation does not run 

This tutorial is made up of two parts:

1.Atomic H chain 

You will have access to the necessary minimal files 

2.Blue Bronze (K0.3MoO3)
