The work herein shown is part of my Doctoral Thesis [Accurate simulation of shallow flows using arbitrary order ADER schemes and overcoming numerical shockwave anomalies](https://zaguan.unizar.es/record/70795?ln=en), presented at University of Zaragoza on the 27th April 2018. 

### Numerical shockwave anomalies

From the early stages of CFD, the computation of shocks using Finite Volume methods has been a very challenging task as they often prompt the generation of numerical anomalies. Such anomalies lead to an incorrect and unstable representation of the discrete shock profile that may eventually ruin the whole solution. The two most widespread anomalies are the slowly-moving shock anomaly and the
carbuncle, which are deeply addressed in the literature in the framework of homogeneous problems, such as Euler equations. In this work, the presence of the aforementioned anomalies is studied in the framework of the 1D and 2D SWE and novel solvers that effectively reduce both anomalies, even in cases where source terms dominate the solution, are presented. 

#### The slowly-moving shock anomaly

The slowly-moving shock anomaly was first investigated by Roberts, who defined it as numerical noise generated in the discrete shock transition layer which is transported downstream. Such noise is also referred to as post-shock oscillations. The slowly-moving shock problem is related to nonlinearities of the Hugoniot curves, which in the case of the SWE, are found in those branches of the Hugoniot locus related to hydraulic jump-type solutions.  Generally, physical shockwaves have a finite width, determined by the physical dissipation processes taking place within the shock. This is the case of hydraulic jumps, whose width has to do with the turbulent transition between the supercritical, more energetic region and the subcritical region. Contrary to this, shocks are mathematically represented by pure discontinuities in hyperbolic systems. On the other hand, when considering the numerical resolution of shockwaves using the FV method, a numerical width, different from the physical width, is enforced by the grid size. This leads to intermediate states which cannot be given a direct physical interpretation, as the shock width is not controlled by the physical dissipation mechanisms within the shock but only by the grid size. Such states cannot be removed even when refining the grid, hence numerical schemes must be designed in a particular way to overcome such flaw




Such solvers are motivated by the flux-extrapolation techniques presented by Dr. Daniel W. Zaide in [his Doctoral Thesis](http://www.danielzaide.com/PDF/zaide_thesis.pdf)


The first stage of the project was the development of the mathematical framework for the resolution of hyperbolic conservation laws with geometric source terms with arbitrary order of accuracy using WENO-ADER schemes. A new family of solvers for the Derivative Riemann problem are proposed, using the augmented-solver methodology and based on previous work from Toro, Castro and Titarev. The novelty of the proposed methods is:

- For transient cases, they converge with arbitrary order to the analytical solution. The numerical solution to a complete set of RPs, including solutions in the resonant regime, are presented in [Navas-Montilla, 2015](https://www.sciencedirect.com/science/article/pii/S0021999115001217) and [Navas-Montilla, 2016](https://www.sciencedirect.com/science/article/pii/S0021999116301024) (see Figure 4).

- For steady cases, they provide the exact solution with independence of the grid thanks to the energy-balanced property.

<figure style="text-align: center;">
  <img src="github_site/rps1.png" width="80%" alt="my alt text"/>
  <figcaption>Figure 4. Resolution of RPs including strong bed variations.</figcaption>
</figure>

Details of the methods and more results can be found in [Navas-Montilla, 2015](https://www.sciencedirect.com/science/article/pii/S0021999115001217) and [Navas-Montilla, 2016](https://www.sciencedirect.com/science/article/pii/S0021999116301024).
