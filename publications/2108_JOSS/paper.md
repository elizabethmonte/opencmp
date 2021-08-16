---
title: 'OpenCMP: An Open-Source Computational Multiphysics Package'
tags:
 - Python
 - finite element method
 - discontinuous Galerkin FEM
 - computational multiphysics
 - computational fluid dynamics
 - diffuse interface method
 - immersed boundary method
authors:
 - name: Elizabeth J. Monte
   orcid: 0000-0001-7328-775X
   affiliation: 1
 - name: Alexandru Andrei Vasile
   orcid: 0000-0002-0233-0172
   affiliation: 1
 - name: James Lowman
   orcid: 0000-0002-1745-9454
   affiliation: 1
 - name: Nasser Mohieddin Abukhdeir^[Corresponding author]
   orcid: 0000-0002-1772-0376
   affiliation: "1, 2" # Need quotes for multiple affiliations
affiliations:
 - name: Department of Chemical Engineering, University of Waterloo, Ontario, Canada
   index: 1
 - name: Department of Physics and Astronomy, University of Waterloo, Ontario, Canada
   index: 2
date: 
bibliography: paper.bib
---

# Summary

OpenCMP is a computational multiphysics software package based on the finite element method [@Ferziger2002]. It is primarily intended for physicochemical processes in which fluid convection plays a significant role. OpenCMP uses the NGSolve finite element library [@ngsolve] for spatial discretization and provides a configuration file-based interface for pre-implemented models and time discretization schemes. It also integrates with Netgen [@ngsolve] and Gmsh [@Geuzaine2009] for geometry construction and meshing. Additionally, it provides users with built-in functionality for post-processing, error analysis, and data export for visualisation using Netgen [@ngsolve] or ParaView [@Ahrens2005]. 

OpenCMP development follows the principles of ease of use, performance, and extensibility. The configuration file-based user interface is intended to be concise, readable, and intuitive. Furthermore, the code base is structured such that experienced users with appropriate background can add their own models with minimal modifications to existing code. The finite element method enables the use of high-order polynomial interpolants for increased simulation accuracy, however, continuous finite element methods suffer from stability and accuracy (conservation) for fluid convection-dominated problems. OpenCMP addresses this by providing discontinuous Galerkin method [@Cockburn2000] solvers, which are locally conservative and improve simulation stability for convection-dominated problems. Finally, OpenCMP implements the diffuse interface method [@Monte2021], an immersed boundary method [@Mittal2005], which allows complex simulation domains to be meshed by non-conforming structured meshes for improved simulation stability and reduced computational complexity (under certain conditions [@Monte2021]).

# Statement of Need

Simulation-based analysis continues to revolutionise the engineering design process. Simulations offer a fast, inexpensive, and safe alternative to physical prototyping for preliminary design screening and optimisation. Simulations can also offer more detailed insight into the physical phenomena of interest than is feasible from experimentation. Computational multiphysics is an area of particular importance since coupled physical and chemical processes are ubiquitous in science and engineering.

However, there are several barriers to more wide spread use of simulations. One such barrier is a lack of suitable software accessible to the general scientific and engineering community. Many of the most widely-used computational multiphysics software packages, such as COMSOL Multiphysics [@comsol] or ANSYS Fluent [@fluent], are closed-source and cost-prohibitive. Furthermore, the predominance of the finite volume method for fluid dynamics simulations inherently limits simulation accuracy for a given mesh compared to the finite element method [@Ferziger2002]. Open-source packages that uses the finite element method, such as the computational multiphysics software MOOSE [@Permann2020] or the finite element libraries NGSolve [@ngsolve] and FEniCS [@Alnaes2015], have very steep learning curves and are inaccessible to the general scientific and engineering communities.

A second barrier is the complex geometries inherent to many real-world problems. Conformal meshing of these complex geometries is time and labour intensive and frequently requires user-interaction, making conformal mesh-based simulations infeasible for high-throughput design screening of many industrially-relevant processes [@Yu2015]. A possible solution is the use of immersed boundary methods [@Mittal2005] to allow the use of non-conforming structured meshes - simple and fast to generate - for any geometry. Use of structured meshes can also potentially improve simulation stability compared to unstructured meshes [@Yu2015]. The diffuse interface method, a form of immersed boundary method, has been shown by Monte *et al* [@Monte2021] to significantly speed up inherently low accuracy simulations - such as those used for preliminary design screening and optimisation - compared to conformal mesh-based simulations. Providing an easy-to-use publicly available implementation of said method would enable broader use by the research community and further development.

The goal of OpenCMP is to fill this evident need for an open-source computational multiphysics package which is user friendly, based on the finite element method, and which includes the diffuse interface method. OpenCMP is built on top of the NGSolve finite element library [@ngsolve] to take advantage of its extensive finite element spaces and high performance solvers and preconditioners. OpenCMP provides pre-implemented models and a configuration file-based user interface in order to be accessible to the general simulation community, not just finite element experts. The user interface is designed to be intuitive and readable and requires no programming experience. On the whole, OpenCMP requires minimal programming experience - solely knowledge of the command line interface. Users must choose the model that suites their application, but need no experience with the actual numerical implementation of said model. Finally, OpenCMP provides the only publicly available implementation of the diffuse interface method.

# Features

The table below summarises the current capabilities of OpenCMP. Future work on OpenCMP will focus on adding models - for multi-phase flow, turbulence, and heat transfer - and enabling running simulations in parallel over multiple nodes with MPI [@mpi].

| Feature           | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| Meshing           | Accepts Netgen[@ngsolve] or Gmsh [@Geuzaine2009] meshes      |
| Numerical Methods | Standard continuous Galerkin finite element method           |
|                   | Discontinuous Galerkin finite element method                 |
|                   | Diffuse interface method                                     |
| Models            | Poisson equation                                             |
|                   | Stokes equations                                             |
|                   | Single-component incompressible Navier-Stokes equations      |
|                   | Multi-component reacting incompressible Navier-Stokes equations |
| Time Schemes      | First-, second-, and third- order discretizations            |
|                   | Adaptive time-stepping                                       |
| Solvers           | Direct or iterative solvers                                  |
|                   | Direct, Jacobi, or multigrid preconditioners                 |
|                   | Oseen [@Cockburn2003] or IMEX [@Ascher1995] linearization of nonlinear models |
| Post-Processing   | Error norms calculated based on reference solutions          |
|                   | Mesh and polynomial refinement convergence tests             |
|                   | General simulation parameters (surface traction, divergence of velocity...) |
|                   | Exports results to Netgen [@ngsolve] or ParaView [@Ahrens2005] format |
| Performance       | Multi-threading                                              |

# Acknowledgements

This research was supported by the Natural Sciences and Engineering Research Council (NSERC) of Canada.

# References