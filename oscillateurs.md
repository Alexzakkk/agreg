[VanderPol.py](https://github.com/user-attachments/files/26571763/VanderPol.py)Oscillateurs, portraits de phase et non-linéarités
Fillette + \
[Nonlinear Dynamics and Chaos (Steven H. Strogatz) (z-library.sk, 1lib.sk, z-lib.sk)_removed_removed.pdf](https://github.com/user-attachments/files/26060331/Nonlinear.Dynamics.and.Chaos.Steven.H.Strogatz.z-library.sk.1lib.sk.z-lib.sk._removed_removed.pdf)
<img width="619" height="577" alt="Capture d&#39;écran 2026-04-06 132525" src="https://github.com/user-attachments/assets/70428fd2-e024-4dc7-ae29-8675f0a8507e" />
<img width="797" height="740" alt="Capture d&#39;écran 2026-04-06 132510" src="https://github.com/user-attachments/assets/ee2ebb3e-af3c-4143-aec5-b5c417ba8c22" />
<img width="1092" height="737" alt="Capture d&#39;écran 2026-04-06 132453" src="https://github.com/user-attachments/assets/1d6af80c-ae19-4acc-9e2b-4a36bc0b1788" />
<img width="1109" height="746" alt="Capture d&#39;écran 2026-04-06 132438" src="https://github.com/user-attachments/assets/35481028-2b18-4681-a305-d0aa2ea7adc8" />
[Nonlineaire.ipynb](https://github.com/user-attachments/files/26507103/Nonlineaire.ipynb) \



[Uploaimport numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

#code pour portrait de phase oscillateur de Van der Pol
#pas plus intéressant que ça de jouer sur les conditions initiales
#En revanche, plus espsilon est grand (~100) plus la convergence vers le cycle limite est grand et plus les oscillations de theta 
#présentent des temps de charge et décharge différents
#plus epsilon est grand plus il faut augmenter t (~400)
#sinon des valeurs espilon = 2 et t =100 sont bien
#on peut mettre en évidence la sélection d'amplitude comme cause de la non-linéarité

def VdP(y, t, eps, useless):

    theta, Y = y

    dydt = [Y - eps*((theta/3)**3-theta), -theta]

    return dydt

y01 = [0.1, 2]
y02 = [8, -4]
y03 = [0.0001, 0.0001]

eps = 1
useless = 0.9

t = np.linspace(0, 100, 1001)

sol1 = odeint(VdP, y01, t, args=(eps,useless))
sol2 = odeint(VdP, y02, t, args=(eps,useless))
sol3 = odeint(VdP, y03, t, args=(eps,useless))





fig = plt.figure("Espace des phases")
plt.plot(sol1[:, 0], sol1[:,1]-eps*((sol1[:, 0]/3)**3-sol1[:, 0]), 'b', label='VdP')
plt.plot(sol2[:, 0], sol2[:,1]-eps*((sol2[:, 0]/3)**3-sol2[:, 0]), 'red', label='VdP')
plt.plot(sol3[:, 0], sol3[:,1]-eps*((sol3[:, 0]/3)**3-sol3[:, 0]), 'green', label='VdP')

plt.xlabel(r'$\theta$')
plt.ylabel(r'$\dot\theta$')
plt.legend()
plt.grid()

plt.show()


fig = plt.figure("Oscillations")
plt.plot(t,sol1[:, 0])







plt.ion()
fig = plt.figure("Dynamic Van der Pol")
ax = fig.add_subplot(111)
line1, = ax.plot(sol3[0,0], sol3[0,1]-eps*((sol3[0, 0]/3)**3-sol3[0, 0]), 'b-')
plt.xlim(-10,10)
plt.ylim(-10,10)

for i in range(len(t)-1):
    line1.set_ydata(sol3[0:i,1]-eps*((sol3[0:i, 0]/3)**3-sol3[0:i, 0]))
    line1.set_xdata(sol3[0:i,0])
    fig.canvas.draw()
    fig.canvas.flush_events()

plt.pause()ding VanderPol.py…]()
