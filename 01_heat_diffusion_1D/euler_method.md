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
\frac{\partial^2 T}{\partial x^2}=frac{T_{i+1}^n-2 T_i^n +T_{i-1}^n}{\Delta x^2}
$$
