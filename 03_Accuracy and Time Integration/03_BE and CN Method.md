## Week 3 – Accuracy and Implicit Time Integration for the 1D Heat Equation

### Objective
The objective of this week is to analyze the **temporal accuracy and error behavior**
of time integration schemes for the 1D heat equation.

While the Explicit Euler method studied in Week 2 is conditionally stable under the CFL condition,
stability alone does not ensure solution quality.
Backward Euler (BE) and Crank–Nicolson (CN) methods are introduced to remove the CFL restriction,
and their accuracy, stability, monotonicity, and numerical diffusion properties are examined
using Taylor expansion and Fourier (von Neumann) analysis.

---

### Governing Equation and Spatial Discretization

We consider the one-dimensional heat equation:

$$
\frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}.
$$

Using a uniform grid and second-order central differences in space, the semi-discrete form becomes

$$
\frac{d T_i}{dt}=\alpha \frac{T_{i+1} - 2T_i + T_{i-1}}{\Delta x^2}.
$$

Defining the nondimensional parameter

$$
r = \frac{\alpha \Delta t}{\Delta x^2},
$$

the temporal behavior of different time integration schemes can be directly compared.

---

### Time Integration Schemes

#### Explicit Euler (reference)

$$
T_i^{n+1}=
T_i^n
+
r \left( T_{i+1}^n - 2T_i^n + T_{i-1}^n \right).
$$

- Conditionally stable
- CFL condition: $r \le 1/2$
- Used as a baseline for comparison

---

#### Backward Euler (BE)
$$
T_i^{n+1}=
T_i^n
+
r \left( T_{i+1}^{n+1} - 2T_i^{n+1} + T_{i-1}^{n+1} \right).
$$

- Implicit and unconditionally stable
- First-order accurate in time
- Strong numerical diffusion
- Monotonic for all time step sizes

---

#### Crank–Nicolson (CN)
$$
T_i^{n+1}=
T_i^n
+
\frac{r}{2}
\Big[
(\Delta_x^2 T)^{n+1} + (\Delta_x^2 T)^n
\Big].
$$

- Implicit and unconditionally stable
- Second-order accurate in time
- Reduced numerical diffusion
- Monotonicity not guaranteed for large time steps

---

### Temporal Accuracy and Truncation Error

Using Taylor expansion in time:

- Backward Euler has a local truncation error of $O(\Delta t^2)$,
  leading to a first-order global accuracy.
- Crank–Nicolson has a local truncation error of $O(\Delta t^3)$,
  resulting in second-order global accuracy.

This difference explains the improved transient accuracy of the CN method.

---

### Fourier Mode Analysis and Amplification Factor

To analyze stability and monotonicity, a single Fourier mode is assumed:

$$
T_i^n = G^n e^{ikx_i}.
$$

The resulting amplification factors are:

- Explicit Euler:

$$
G_E = 1 - 4r \sin^2(\theta/2)
$$

- Backward Euler:

$$
G_{BE} = \frac{1}{1 + 4r \sin^2(\theta/2)}
$$

- Crank–Nicolson:

$$
G_{CN}=
\frac{1 - 2r \sin^2(\theta/2)}
       {1 + 2r \sin^2(\theta/2)}.
$$

---

### Stability, Monotonicity, and Numerical Diffusion

- Stability requires $|G| \le 1$
- Monotonicity requires $G \ge 0$

Backward Euler suppresses high-frequency modes aggressively,
introducing significant numerical diffusion.
Crank–Nicolson reduces numerical diffusion by time-centering,
but may produce non-physical oscillations due to sign reversal of high-frequency modes.

---

### Summary

- Backward Euler is robust and monotone, but overly diffusive for transient problems.
- Crank–Nicolson provides higher temporal accuracy and better transient behavior,
  at the cost of possible oscillations.
- Stability, accuracy, and monotonicity are distinct numerical properties
  and must be evaluated separately.

---

### Time Convergence Study

To verify the temporal accuracy of the Backward Euler and Crank–Nicolson schemes,
a time convergence study was performed.

The spatial discretization was fixed using a sufficiently fine grid,
and only the time step size was varied.
To eliminate boundary effects and enable an exact reference solution,
homogeneous Dirichlet boundary conditions were imposed,
with the initial condition

$$
T(x,0) = \sin(\pi x).
$$

The corresponding analytical solution is

$$
T(x,t) = e^{-\alpha \pi^2 t} \sin(\pi x),
$$

which allows direct evaluation of numerical error.

For each time step size, the numerical solution was advanced to a fixed final time,
and the $L^2$ error with respect to the analytical solution was computed.

Figure below shows the $L^2$ error as a function of the time step size on a log–log scale.

---

### Results and Interpretation

The Backward Euler method exhibits approximately first-order convergence in time,
as indicated by the slope of the error curve.
The absolute error level is relatively large,
reflecting the strong numerical diffusion introduced by the method.

In contrast, the Crank–Nicolson method demonstrates second-order temporal convergence
over a wide range of time step sizes.
For sufficiently small time steps, the error curve flattens,
indicating that the temporal error has been reduced below the level of the spatial discretization error.

These results confirm the theoretical analysis:
Backward Euler is robust and monotone but overly diffusive for transient problems,
whereas Crank–Nicolson provides higher temporal accuracy
at the cost of potential non-monotonic behavior.

---


## Reflection

Compared to the previous two weeks, the concepts covered in Week 3 were more clearly connected.
The distinction between stability, monotonicity, and accuracy became concrete through
Fourier mode analysis and amplification factor interpretation.

In particular, the time convergence experiment played a crucial role in reinforcing
the theoretical results.
Observing first-order convergence for Backward Euler and second-order convergence for
Crank–Nicolson clarified the practical implications of temporal accuracy,
numerical diffusion, and method selection for transient problems.

Overall, this week helped bridge the gap between formal analysis and numerical behavior,
providing a more intuitive understanding of implicit time integration schemes.
