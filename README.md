# Differential-equations

# Caída libre 

$$
\frac{dv}{dt}= g - \frac{k}{m}v
$$

# Atractor de Lorentz

Las ecuaciones del atractor de Lorenz son:

$$
\begin{aligned}
\frac{dx}{dt} &= \sigma (y - x) \\\\
\frac{dy}{dt} &= x (\rho - z) - y \\\\
\frac{dz}{dt} &= x y - \beta z
\end{aligned}
$$

donde:

- $x, y, z$ son las variables del sistema dinámico,
- $\sigma$ es el número de Prandtl,
- $\rho$ es el número de Rayleigh,
- $\beta$ es un parámetro geométrico del sistema.



<div align="center">
  <video src="https://github.com/user-attachments/assets/38017465-3e5c-4c61-a8b8-aac4087c6081" width="100" />
</div>


```python
import numpy as np
import matplotlib.pyplot as plt

from matplotlib.animation import FuncAnimation

plt.rcParams['toolbar'] = 'none'

s, r, b = 10, 18, 8/3

dt = 0.01
n  = 10000

x, y, z = 0, 1.0, 1.05
xs, ys, zs = [], [], []

for _ in range(n):
    dx = s * (y - x)
    dy = x * (r - z) - y
    dz = x * y - b * z
    x += dx * dt
    y += dy * dt
    z += dz * dt
    xs.append(x)
    ys.append(y)
    zs.append(z)

fig = plt.figure(facecolor='#121212')
fig.subplots_adjust(left=0, right=1, bottom=0, top=1)
ax  = fig.add_subplot(111, projection='3d', facecolor='#121212')
ax.axis('off')


line, = ax.plot([], [], [], color='#ffffff', lw=0.5)


ax.set_xlim(min(xs), max(xs))
ax.set_ylim(min(ys), max(ys))
ax.set_zlim(min(zs), max(zs))

def update(frame):
    t = int(frame)
    line.set_data(xs[:t], ys[:t])
    line.set_3d_properties(zs[:t])
    ax.view_init(elev=30, azim= 0.1 * t)
    return line,

ani = FuncAnimation(fig, update, frames=range(0, len(xs), 10), interval=30)
#ani.save('lorenz_attractor.mp4', writer='ffmpeg', fps=30, dpi=200)
plt.show()
```
---

# Atractor de Rössler

Las ecuaciones del atractor de Rössler son:

$$
\begin{aligned}
\frac{dx}{dt} &= - y - z \\\\
\frac{dy}{dt} &= x + a y \\\\
\frac{dz}{dt} &= b + z (x - c)
\end{aligned}
$$

donde:

- $x, y, z$ son las variables del sistema dinámico,  
- $a, b, c$ son parámetros del sistema que determinan el comportamiento caótico.

# Atractor de Thomas

Las ecuaciones del atractor de Thomas son:

$$
\begin{aligned}
\frac{dx}{dt} &= \sin(y) - b x \\\\
\frac{dy}{dt} &= \sin(z) - b y \\\\
\frac{dz}{dt} &= \sin(x) - b z
\end{aligned}
$$

donde:

- $x, y, z$ son las variables del sistema dinámico,  
- $b$ es un parámetro que controla la disipación del sistema.

<div align="center">
  <video src="https://github.com/user-attachments/assets/da5b0b89-0a50-4c56-aba2-109fd99bf599" width="100" />
</div>

```python
import numpy as np
import matplotlib
matplotlib.use('TkAgg')

import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

plt.rcParams['toolbar'] = 'none'

b = 0.208
n  = 100000
dt = 0.01

x, y, z = 0, 1.0, 1.05
xs, ys, zs = [], [], []

for _ in range(n):
    dx = np.sin(y) - b * x
    dy = np.sin(z) - b * y
    dz = np.sin(x) - b * z
    x += dx * dt
    y += dy * dt
    z += dz * dt
    xs.append(x)
    ys.append(y)
    zs.append(z)


fig = plt.figure(facecolor='#121212')
ax  = fig.add_subplot(111, projection='3d')
ax.set_facecolor('#121212')

line, = ax.plot([], [], [], color='#ffffff')

ax.set_xlim(min(xs), max(xs))
ax.set_ylim(min(ys), max(ys))
ax.set_zlim(min(zs), max(zs))
ax.axis('off')

plt.plot(xs, ys, zs, color='#ffffff', lw=0.5)

def update(frame):
    t = int(frame)
    line.set_data(xs[:t],ys[:t])
    line.set_3d_properties(zs[:t])
    ax.view_init(elev=30, azim=0.1 * t)


ani = FuncAnimation(fig, update, frames=range(0, 1000, 1), interval=1, repeat=0)
#ani.save('Thomas.mp4', writer='ffmpeg', fps=30, dpi=200)
plt.show()
```
