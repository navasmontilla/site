

## Numerical simulation of complex flows

Nowadays, the combination of modern supercomputers with cutting-edge simulation tools allows to solve very complex problems of technological and scientific interest and, what is more important, it allows to be predictive. The numerical simulation of environmental events, such as atmospheric, oceanic or surface water flows, has come to a point where trustworthy predictions can be done at an affordable cost, providing quite a realistic picture of the potential threats linked to those events. On the other hand, the rocketing technological growth of the manufacturing industry is demanding the study and resolution of new problems that can be addressed through the same approach.

### Hyperbolic conservation laws

Hyperbolic partial differential equations arise in a broad variety of fields where wave propagation phenomena are dominant, for instance, gas dynamics and acoustics, and there is a branch of CFD that is exclusively focused on such problems. Historically, many of the fundamental ideas were developed in the framework of the compressible Euler equations for gas dynamics by the aerospace community. At present, these methods have been extended to other applications such as free surface flows modeled by the shallow water equations (SWE). As Euler equations, the SWE are nonlinear and their solutions suffer from loss of regularity: solutions that are initially smooth may eventually become discontinuous in the form of shock waves.

### State-of-the-art challenges

Nowadays, the current trend is to design accurate and efficient schemes by means of a combination of: (a) very high order numerical schemes (e.g. WENO, ADER and DG schemes), which require a shorter computational time and memory than a lower order scheme to achieve the same accuracy (see Figures 1 and 2), (b) adaptive mesh refinement techniques and other sophisticated meshing algorithms and (c) efficient parallel implementations for high performance computing (OpenMP, MPI, CUDA and OpenACC, among others).

<figure style="text-align: center;">
  <img src="github_site/examples1.png" alt="my alt text"/>
  <figcaption>Figure 1. Numerical solution of the Doswell frontogenesis for the linear advection equation using a 1-st order and 7-th order WENO-ADER scheme.</figcaption>
</figure>

<figure style="text-align: center;">
  <img src="github_site/examples2.png" alt="my alt text"/>
  <figcaption>Figure 2. Logarithmic plot of the numerical error versus the number of cells (left) and CPU time (right) for the resolution of the acoustic equations using the WENO-ADER scheme.</figcaption>
</figure>

On the other hand, the presence of source terms in the equations is an issue which we must pay attention to. Source terms model the presence of extra physical effects not represented by the pure conservative terms in the equations and may often govern the dynamics of the problem. The search of a suitable treatment of the source term in the numerical scheme is not a trivial task, but it is of utmost importance in order to preserve steady states of relevance.

## Research project

The work herein presented has been developed at the [Computational Hydraulics Group](http://ghc.unizar.es) at [Univerisity of Zaragoza](https://www.unizar.es/). Computational resources have been provided by [LIFTEC-CSIC](http://www.liftec.unizar-csic.es/es/). The validation of the computational tools has been done in colaboration with the [LCH-EPFL](https://lch.epfl.ch/). 

### Generation of arbitrary order augmented schemes for hyperbolic problems with source terms: application to the SWE

We aim at the generation of fully-discrete arbitrary order numerical schemes, based on the WENO spatial reconstruction and ADER time-stepping technique, with application to hyperbolic problems with source terms. The proposed schemes are based on augmented Riemann solvers that include the contribution of source terms in the definition of the Riemann problem, allowing the presevation of equilibrium states with machine precision.

We consider the application of the aforementioned methods to the SWE with bed elevation, friction and Coriolis. In presence of such sources, the relevant equilibrium states are:

- Quiescent equilibrium (well-balanced property).
- Moving water equilibrium (energy-balanced property).
- Geostrophic equilibrium (well-balanced property in the rotating frame).

<figure style="text-align: center;">
  <img src="github_site/equistates.png" alt="my alt text"/>
  <figcaption>Figure 3. Relevant equilibrium states for the SWE.</figcaption>
</figure>

Furthermore, additional dissipation effects are accounted for by including turbulence models using the Boussinesq approximation. The RANS and URANS approaches are considered and algebraic as well as 1 and 2 equation turbulence models are used.

#### The WENO AR/ARL-ADER method in 1D: well-balanced and energy-balanced simulation of the SWE with bed variation

The first stage of the project was the development of the mathematical framework for the resolution of hyperbolic conservation laws with geometric source terms with arbitrary order of accuracy using WENO-ADER schemes. A new family of solvers for the Derivative Riemann problem are proposed, using the augmented-solver methodology and based on previous work from Toro, Castro and Titarev. The novelty of the proposed methods is:

- For transient cases, they converge with arbitrary order to the analytical solution.
- For steady cases, they provide the exact solution with independence of the grid thanks to the energy-balanced property.

<figure style="text-align: center;">
  <img src="github_site/rps1.png" width="80%" alt="my alt text"/>
  <figcaption>Figure 4. Resolution of RPs including strong bed variations.</figcaption>
</figure>

Detais of the methods and more results can be found in [Navas-Montilla, 2015](https://www.sciencedirect.com/science/article/pii/S0021999115001217) and [Navas-Montilla, 2016](https://www.sciencedirect.com/science/article/pii/S0021999116301024).

#### The WENO ARL-ADER method in 2D: well-balanced simulation of the SWE with bed variation, friction and Coriolis

In this part, the extension of the numerical schemes in the previous section are extended to the resolution of the 2D SWE with geometric source term and their application to other shallow water models involving non-geometric sources is also explored. The proposed method, implemented using the OpenMP paradigm, offers a remarkable gain in computational time when applied to 2D shallow water scenarios with source terms. Figure 5 shows the numerical error vs. CPU time (single-threaded/serial execution) and wall time (parallel execution in 28 threads). The numerical results evidence that the 3-rd order scheme is able to provide the same level of accuracy than a 1-st order scheme requiring a 65 times shorter computational time, for an error of around 1.E-4. On the other hand, the plots also show that the paralellization of the code allows an additional speed-up.

<figure style="text-align: center;">
  <img src="github_site/sim_times.png" width="90%" alt="my alt text"/>
  <figcaption>Figure 5. Numerical error vs. CPU and wall time, showing the ahcieved speedup.</figcaption>
</figure>

[![Simulation video](https://img.youtube.com/vi/3SAfCJ6xGqY/2.jpg)](https://www.youtube.com/watch?v=3SAfCJ6xGqY "play video") [![Simulation video](https://img.youtube.com/vi/-Dye0LG8-Ds/2.jpg)](https://www.youtube.com/watch?v=-Dye0LG8-Ds "play video") [![Simulation video](https://img.youtube.com/vi/M7ep81gngow/2.jpg)](https://www.youtube.com/watch?v=M7ep81gngow "play video")

#### URANS simulation of shallow flows using the WENO ARL-ADER method for the SWE

[![Simulation video](https://img.youtube.com/vi/J3epKVZyX-o/2.jpg)](https://www.youtube.com/watch?v=J3epKVZyX-o "play video") [![Simulation video](https://img.youtube.com/vi/Z9r3haLVEjc/2.jpg)](https://www.youtube.com/watch?v=Z9r3haLVEjc "play video")

### Overcoming numerical shockwave anomalies

### Markdown

Here it is an example of how to add a link to a video:

[![Simulation video](https://img.youtube.com/vi/M7ep81gngow/2.jpg)](https://www.youtube.com/watch?v=M7ep81gngow "video name")

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List


**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

* [Hyperlink](test.md)

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/navasmontilla/site/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
