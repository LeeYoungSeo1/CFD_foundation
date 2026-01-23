# Explicit Euler Discretization of the Heat Equation

## 1. Time Discretization
The temporal derivative is approximated using a forward difference:

$$
\frac{\partial T}{\partial t} = \frac{T_i^{n+1}-T_i^n}{\Delta t}
$$

This corresponds to advancing the solution using the current time slope only,
which is the defining characteristic of the Explicit Euler method.

## 2.  Spatial Discretization
The second spatial derivative is approximated using a central difference:

$$
\frac{\partial^2 T}{\partial x^2}= \frac{T_{i+1}^n-2 T_i^n +T_{i-1}^n}{\Delta x^2}
$$
This discretization measures the local curvature of the temperature field
and captures the imbalance of heat flux at each grid point.

## 3. Fully Discrete Scheme
Considering time and spatial discretization yields,

$$
T_i^{n+1}=T_i^n+ r(T_{i+1}^n-2T_i^n+T_{i-1}^n)
$$

where the diffusion numer r is defined as

$$
r = \frac{\alpha \Delta t}{\Delta x ^2}
$$

## 4. Interpretation of the Diffusion Number
The diffusion number r represents the fraction of spatial diffusion occurring within a single time step.

- Small r corresponds to slow, incremental averaging.
- Large r corresponds to aggressive averaging and may lead to numerical instability.

Thus, r plays a dual role as both a physical and numerical parameter, connecting time step size, grid resolution, and material properties.

Explicit Euler uses only present-time information, which imposes a **stability constraint on r** that will be analyzed in later stages.

