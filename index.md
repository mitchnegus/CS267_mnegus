###### Mitch Negus – Spring 2018

[Bio](bio.md)

## Parallelizing Radiation Transport

<img src="img/te.png" width="600px"> 

Radiation is everywhere. Some of these particles–neutrinos and high energy gamma rays–pass through us every day with little effect. Other types, like relatively large alpha particles, are stopped by a barrier as thin as a sheet of paper. Since the beginning of the 20th century, scientists and engineers have pioneered applications based on the motion of these particles. Accelerators have been created for understanding the fundamental structure of our universe, X-ray devices have been invented to image anatomy, nuclear reactors have been constructed to harness the universe's most energy dense fuel, and nuclear weapons have been developed to threaten international adversaries.

The trajectories and behaviors of these particles are described by mathematical equations, which can be solved to predict the future of a system. One example is the neutron transport equation, a linear integro-differential equation which balances neutron production and elimination. While the equation itself is continuous (with 7 independent variables–the particle's position in 3 spatial dimensions, direction of motion in 2 angles, energy, and time) and is impossible to solve exactly but for a few simple cases, each of these variables can be discretized to facilitate numerical solutions.

Solving this equation numerically has been a focus of nuclear engineers, physicists, and mathematicians modeling neutronics. Numerous codes [^fn1][^fn2][^fn3][^fn4] have been developed to accomplish this, and nearly all of them have relied on parallel computing architectures. For example, MPACT, developed by the University of Michigan for the Consortium for the Advanced Simulation of Light Water Reactors (CASL), is implemented on (though not specifically designed for) the Titan supercomputer at Oak Ridge National Laboratory (ORNL). Titan ranks 5th on the Top 500 list as of November 2017[^fn5], with an Rmax of 17.6 PFlop/s and a theoretical peak of 27.1 PFlop/s. It has a total of 18,688 compute nodes, each with 16 CPUs, for a total of 299,008 CPUs.[^fn6] In addition to the CPUs, each node also has access to GPU processing equivalent to 14 CPU cores.[^fn7]

MPACT is designed specifically to solve the transport equation in nuclear reactor cores[^fn8] using the method of characteristics (MOC). This method has gained popularity recently due to its tractability on parallel computing architectures [^fn9]. Still, MPACT relies on 2D/1D MOC (which couple two dimensional MOC calculations with a more approximate calculation in the third dimension) since 3D MOC is too complicated. When run as part of the VERA code framework, MPACT has been shown to be successful in modeling the Watts Bar Nuclear Power Plant, Unit 1 (WBN1). The code was run on Titan, and was found to produce results matching the public data from the first operating cycle to within reasonable values.[^fn10] 



[^fn1]: DENOVO: Discrete ordinates, Oak Ridge National Laboratory
[^fn2]: PARTISN: Discrete ordinates, Los Alamos National Laboratory
[^fn3]: OpenMOC: Method of Characteristics, MIT
[^fn4]: MPACT: Method of Characteristics, University of Michigan
[^fn5]: [Top 500 List](https://www.top500.org/lists/2017/11/)
[^fn6]: [Titan Tech Specs](https://www.olcf.ornl.gov/computing-resources/titan-cray-xk7/)
[^fn7]: [Titan User Guide](https://www.casl.gov/sites/default/files/docs/CASL-U-2015-0078-000.pdf)
[^fn8]: Collins, B. [MPACT Theory Manual Version 2.0.0](https://www.casl.gov/sites/default/files/docs/CASL-U-2015-0078-000.pdf)
[^fn9]: Collins, B. _et al._ "Stability and accuracy of 3D neutron transport simulations using the 2D/1D method in MPACT." Journal of Computational Physics. December 2016.
[^fn10]: Kochunas, B. _et al._ ["Validation and Application of the 3D Neutron Transport Code MPACT within CASL VERA-CS."](https://www.casl.gov/sites/default/files/docs/CASL-U-2015-0078-000.pdf)
