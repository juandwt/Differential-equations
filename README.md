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
  <video src="https://github.com/user-attachments/assets/38017465-3e5c-4c61-a8b8-aac4087c6081" width="400" />
</div>


```python
import numpy as np
import matplotlib
matplotlib.use('TkAgg')

import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

plt.rcParams['axes3d.mouserotationstyle'] = 'azel'
plt.rcParams['toolbar'] = 'none'

# Parámetros del atractor de Lorenz
sigma = 10
rho = 28
beta = 8/3

dt = 0.01
num_steps = 10000

# Condición inicial
x, y, z = 0.0, 1.0, 1.05

# Listas para almacenar la trayectoria
xs, ys, zs = [], [], []

# Generar trayectoria
for _ in range(num_steps):
    dx = sigma * (y - x)
    dy = x * (rho - z) - y
    dz = x * y - beta * z

    x += dx * dt
    y += dy * dt
    z += dz * dt
    xs.append(x)
    ys.append(y)
    zs.append(z)

# Crear figura
fig = plt.figure(facecolor='#121212')
ax = fig.add_subplot(111, projection='3d', facecolor='#121212')
ax.set_facecolor('#121212')
ax.set_box_aspect([1, 1, 0.6])
ax.axis('off')


fig.subplots_adjust(left=0, right=1, bottom=0, top=1)
# Inicializar línea
line, = ax.plot([], [], [], lw=0.5, color='white')

# Límite de la animación
ax.set_xlim((min(xs), max(xs)))
ax.set_ylim((min(ys), max(ys)))
ax.set_zlim((min(zs), max(zs)))

def update(frame):
    step = int(frame)
    line.set_data(xs[:step], ys[:step])
    line.set_3d_properties(zs[:step])
    ax.view_init(elev=30, azim=0.1 * step)  # Rotación lenta

# Crear animación

ani = FuncAnimation(fig, update, frames=range(0, len(xs), 10), interval=30)
#ani.save('lorenz_attractor.mp4', writer='ffmpeg', fps=30, dpi=200)
plt.show()
```
