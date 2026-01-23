# problem definition
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
$ q = -k \frac{\partial T}{\partial x} $
