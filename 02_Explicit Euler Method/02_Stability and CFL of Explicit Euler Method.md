## Week 2 – Stability and CFL Condition of the Explicit Euler Method

### Objective
The goal is to analyze the stability properties of the explicit euler method for the 1D heat equation.
Using Fourier (von Neumann) stability analysis and numerical experiments, 
the CFL condition is derived and verified, with particular emphasis on the role of high frequency modes.

### Governing Equation and Numerical Scheme

Considering 1D heat equation discretized on a uniform grid using a second-order central difference in space and the Explicit Euler method in time:

$$
T_i^{n+1}=
T_i^n
+
r \left( T_{i+1}^n - 2T_i^n + T_{i-1}^n \right),
$$

### Fourier Stability Analysis and CFL condition

To analyze stability, a single Fourier mode is assumed:

$$
T_i^n = G^n e^{ikx_i},
$$

where $G$ is the amplification factor.
Substituting into the discrete scheme yields


$$
G(k) = 1 - 4r \sin^2\left(\frac{k\Delta x}{2}\right).
$$


Requiring 

$$
|G| \le 1 
$$

for all modes gives the CFL condition

$$
r \le \frac{1}{2}.
$$

This result indicates that the Explicit Euler method is **conditionally stable** for diffusion problems.

## Stability vs Monotonicity

Stability alone does not guarantee physically meaningful solutions.
While the stability condition requires the amplification factor to satisfy

$$
|G(k)| \le 1,
$$

monotonicity additionally requires

$$
G(k) \ge 0,
$$

which prevents sign changes and spurious oscillations.

For the Explicit Euler scheme, the amplification factor is

$$
G(k) = 1 - 4r \sin^2\left(\frac{k\Delta x}{2}\right).
$$

The monotonicity condition is therefore

$$
1 - 4r \ge 0 \quad \Rightarrow \quad r \le \frac{1}{4}.
$$

This implies:

- stable and monotone (no oscillation)

$$
r \le 0.25
$$

- stable but non-monotone (oscillatory behavior possible)

$$
0.25 < r \le 0.5
$$

- unstable

$$
r > 0.5
$$

Numerical results confirm that oscillations may appear even when the CFL condition
is satisfied, highlighting the distinction between stability and monotonicity.


### Why the Worst-Case Mode is High-Frequency
The discrete Laplacian amplifies short-wavelength (high-frequency) components most strongly.
For grid-scale oscillations (near the Nyquist limit), the second-order finite difference operator
attains its maximum magnitude, leading to the smallest (and potentially negative) amplification factor.

As a result, instability always originates from the highest-frequency mode supported by the grid.
This motivates the use of sinusoidal initial conditions to isolate and test worst-case behavior.


### Numerical Experiments

### 1. Stability Map with Fixed Number of Time Steps

With a fixed number of time steps \( N_t \), simulations were performed for several values of \( r \):

- \( r = 0.10, 0.25, 0.49 \): solutions remain bounded
- \( r = 0.51, 0.60 \): oscillatory growth and divergence are observed

For \( r > 0.5 \), the numerical solution exhibits alternating sign oscillations
and rapidly growing amplitude, confirming violation of the CFL condition.

### 2. High-Frequency Mode Test

To directly examine the most unstable mode, the initial condition

$$
T(x,0) = \sin(m\pi x/L)
$$

with large \( m \) was used.
This mode corresponds to short-wavelength oscillations near the grid resolution limit.

Results show:

- For \( r < 0.5 \), the high-frequency mode decays due to diffusion
- For \( r > 0.5 \), the same mode grows exponentially while alternating in sign

This confirms that instability originates from insufficient damping of high-frequency components.

## Key Takeaways

- The Explicit Euler method for the heat equation is **conditionally stable**.
- The CFL condition \( r \le 0.5 \) arises from the most oscillatory (high-frequency) spatial mode.
- Instability manifests as alternating-sign oscillations with growing amplitude.
- Violating the CFL condition does not immediately guarantee visible instability unless
  sufficient time steps are taken for unstable modes to grow.
- Stability does not imply accuracy; even stable solutions may suffer from excessive numerical diffusion.
