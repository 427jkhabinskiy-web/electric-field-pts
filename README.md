# electric-field-pts
import numpy as np
import matplotlib.pyplot as plt
k=8.99e9
q=1
N=20
x0 = 6.0
y0=7.0 
x = np.linspace( x0 - 6.5 ,x0 + 6.5,N)+1e-6 # so as not to have point at zero
y = np.linspace(y0 - 7.0  , x0+7.0,N)+1e-6
X,Y = np.meshgrid(x,y)

# first charge at (6, 7)
dx= X- x0
dy= Y- y0
r2=dx**2+dy**2
# now find field
thE = np.arctan2(dy,dx)
magE = k*q/r2
Ex1 = magE*np.cos(thE)
Ey1 = magE*np.sin(thE)

# second charge at (1, 2)
x0_2 = 1.0
y0_2 = 2.0
dx2 = X - x0_2
dy2 = Y - y0_2
r2_2 = dx2**2 + dy2**2
# Avoid exact division by zero if a grid point hits the charge
r2_2[r2_2 < 1e-6] = 1e-6
# now find field for second charge
thE2 = np.arctan2(dy2,dx2)
magE2 = k*q/r2_2
Ex2 = magE2*np.cos(thE2)
Ey2 = magE2*np.sin(thE2)

# combine fields from both charges
Ex = Ex1 + Ex2
Ey = Ey1 + Ey2
magE_total = np.sqrt(Ex**2 + Ey**2)

mask = magE_total > 40 # will have big values near origin

# quiver plot
fig, ax = plt.subplots()
q = ax.quiver(X[mask],Y[mask],Ex[mask],Ey[mask])
ax.set_aspect('equal')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_title(f'Electric Field of Two Point Charges')

plt.show()
