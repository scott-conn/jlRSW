# jlRSW
Numerical solver for the rotating shallow water equations

## 1 - The Shallow Water Equations
The shallow water equations are a set of 3 coupled PDEs for the velocity - $(u,v)$ - of a fluid and the height of the fluid - $h$.

$$\begin{align}
  \frac{\partial u}{\partial t} + u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y} -fv &= -g\frac{\partial \eta}{\partial x},\\
  \frac{\partial v}{\partial t} + u\frac{\partial v}{\partial x} + v\frac{\partial v}{\partial y} +fu &= -g\frac{\partial \eta}{\partial y},\\
  \frac{\partial \eta}{\partial t} + \frac{\partial hu}{\partial x} + \frac{\partial hv}{\partial y} &=0,
\end{align}$$

where we have defined $\eta(x,y)=h(x,y)-H(x,y)$ and $H(x,y)$ is the bathymetry of the problem.

## 2 - Pseudospectral Solution in a Periodic Domain
Taking the Fourier transform in $x$ and $y$ we obtain:

$$\begin{align}
  \frac{d \tilde{u}}{dt} + \widetilde{u\frac{\partial u}{\partial x}} + \widetilde{v\frac{\partial u}{\partial y}} - f\tilde{v} &= -igk\tilde{\eta},\\
  \frac{d \tilde{v}}{dt} + \widetilde{u\frac{\partial v}{\partial x}} + \widetilde{v\frac{\partial v}{\partial y}} +f\tilde{u} &= -igl\tilde{\eta},\\
  \frac{d \tilde{\eta}}{dt} + ik\widetilde{hu} + il\widetilde{hv} &=0,
\end{align}$$

For quadratic terms we take products in physical space and then transform to Fourier space. We can write the system of equations as:

$$\begin{equation}
  \frac{d\vec{U}}{dt}=\vec{f}(\vec{U}).
\end{equation}$$

We introduced the vector $\vec{U}=(\tilde{u},\tilde{v},\tilde{\eta})$. We can solve this ODE using whatever time-stepping method we choose. For example, with RK2 ($\alpha=2/3$) we have:

$$\begin{align}
  \vec{k}_1 &= \vec{f}(t_n,\vec{U}_n),\\
  \vec{k}_2 &= \vec{f}\left(t_n+\frac{2\Delta t}{3},\vec{U}_n+\frac{2\Delta t\vec{k} _1}{3}\right),\\
  \vec{U} _{n+1} &=\vec{U}_n+\frac{\Delta t}{4}\(\vec{k}_1+3\vec{k}_2)
\end{align}$$
