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
\T_i^{n+1}=T_i^n+ r(T_{i+1}^n-2T_i^n+T_{i-1}^n)
$$

where the diffusion numer r is defined as

$$
r = \frac{\alpha \Delta t}{\Delta x ^2}
$$
