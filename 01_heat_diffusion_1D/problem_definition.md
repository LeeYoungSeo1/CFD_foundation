# Problem Definition

## 1. Physical Meaning of the Heat Equation
Considering 1D diffusion eqn,

$$
\frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}
$$

where $T(x,t)$ is the temperature and $\alpha$ is the thermal diffusivity.

This eqn is derived directly from **energy conservation** and **fourier's law**.
Consider a differential control volume in a 1D rod. 
The rate of change of internal energy must balance the net conductive heat flux.
Thus,

$$
\rho C_p \Delta x = q(x) - q(x+ \Delta x)
$$

Using fourier's law,

$$
q = -k \frac{\partial T}{\partial x} 
$$

and applying energy conservation leads to 

$$
\rho C_p \frac{\partial T}{\partial t} = \frac{\partial}{\partial x} (k \frac{\partial T}{\partial x})
$$

Assuming constant material properties, this reduces to the heat equation,
where $\alpha = \frac{k}{\rho C_p}$. 


Importantly, temperature change due to the **imbalance of the heat flux** not its gradient itself.
The second spatial derivative represents curvature in the T field, which drives diffusion.

## 2. Diffusion as a Physical Process

This eqn describes a diffusion process.  
Regions of high temperature curvature experience stronger changes, while flat regions remain unchanged.

From a physical perspective, diffusion can be interpreted as a local averaging process:
- Points hotter than their neighbors lose heat.
- Points colder than their neighbors gain heat.

**This behavior distinguishes diffusion from wave propagation.**
While waves transmit information at finite speed, diffusion spreads information instantaneously but gradually.

## 3. Diffusion Time Scale
A characteristic time scale for diffusion can be obtained through scaling analysis.
Balancing the temporal and spatial terms of the heat equation,

$$
\frac{T}{\tau}=\alpha frac{T}{L^2}
$$

yields the diffusion time scale

$$
\tau=frac{L^2}{\alpha}
$$
