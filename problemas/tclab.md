---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.13.7
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Descripción general del Laboratorio de control de tempratura BYU

Este modelo representa el [Laboratorio de control de temperatura de BYU](http://apmonitor.com/pdc/index.php/Main/ArduinoTemperatureControl). El laboratorio de control de temperatura es una aplicación de control con un Arduino, un LED, dos calentadores y dos sensores de temperatura. La potencia de salida del calentador se ajusta para mantener una de las tempraturas en el valor deseado. La energía térmica del calentador se transfiere por conducción, convección y radiación al sensor de temperatura. El calor también se transfiere del dispositivo al entorno.

```{figure} .\tclab_device.png
:name: tclab
:alt: control de teperantura
:width: 250
:align: center

Dispositivo de control de temperatura
```


+++

Con este sistema el objetivo será controlar la temperatura en uno de los calentadores, que es midida mediante la señal $T1$. Para este propósito de control se utiliza la señal $Q1$. 

La señal $Q2$ no podrá ser utilizada por nuestro sitema de control, ya que es utilizada por otro lazo. 

Se tiene una segunda medición $T2$ que es la temperatura de un segundo calentador, pero que no nos interesa controlar.

A continuación se implementa un modelo de este sistema en Python. Para esto primero importamos las herramientas de Python que utilizaremos.

```{code-cell} ipython3
import control as ctrl
import matplotlib.pyplot as plt
import numpy as np
```

Escribimos ahora las ecuaciones que gobiernan la dinámica del sistema

```{code-cell} ipython3
def derivs_tclab(t, x, u, params):
    "Las ecuaciones de las derivadads en las ecuaciones de estados"
    Q1 = u[0]
    Q2 = u[1]
    Ta=params.get('Ta', 19)
    P1max=params.get('P1max', 100)
    P2max=params.get('P2max', 200)
    H1 = x[0]
    H2 = x[1]
    T1 = x[2]
    T2 = x[3]
    DeltaTaH1 = Ta - H1
    DeltaTaH2 = Ta - H2
    DeltaT12 = H1 - H2
    dH1 = P1max * Q1 / 5720 + DeltaTaH1 / 20 - DeltaT12 / 100
    dH2 = P2max * Q2 / 5720 + DeltaTaH2 / 20 + DeltaT12 / 100
    dT1 =(H1 - T1)/140
    dT2 = (H2 - T2)/140
    return [dH1, dH2, dT1, dT2]


def output_tclab(t, x, u, params):
    "Las ecuaciones de las salida"
    return [x[2], x[3]]
```

Con estas ecuaciones implementamos en Python el modelo no lienal del sistema.

```{code-cell} ipython3
tclab_sys = ctrl.NonlinearIOSystem(updfcn=derivs_tclab, 
                                  outfcn=output_tclab, 
                                  inputs=('Q1', 'Q2'), 
                                  outputs=('T1', 'T2'), 
                                  states=['H1', 'H2', 'T1', 'T2'], 
                                  name='susp')
```

Ahora vamos a definir el vector de entradas $U$, contiene las entradas $T1$ y $T2$ para cada instante definido en un vector $T$.

```{code-cell} ipython3
T=np.linspace(0,2000, 2000)
def Usignal(T):
    U = np.zeros((2, len(T)))
    for i, t in enumerate(T):
        U[0,i] = 50 if t > 400 and t < 1600 else  0
        U[1,i] = 50 if t > 1200 else  0
        
    return U

U=Usignal(T)
```

Grafico las señales $Q1$ y $Q2$

```{code-cell} ipython3
fig, ax = plt.subplots(figsize=(12,5))
ax.plot(T, U[0,:], label=r'$Q1$')
ax.plot(T, U[1,:], label=r'$Q2$')
ax.set_xlabel('Tiempo [s]')
ax.set_ylabel('Potencia en % pot Max ')
ax.legend();
```

Ahora simularemos la respuesta al sistema a esas dos entradas. Consideraremos que todas las temperaturas del sistema están en equilibrio con la temperatura ambiente (19 grados)

```{code-cell} ipython3
X0 = [19,19, 19, 19]
t,y = ctrl.input_output_response(tclab_sys, T, U, X0)
```

En $y$ y en $t$ ahora están los valores que toman la salida $y(t) = [T1(t), T2(t)]$, para distintos valores de $t$.

+++

## Práctico 1

+++

1. Hacer un diagrama del bloque del laboratorio de temperatura donde se vean cuales son las entradas y las salidas. De las entradas diferenciar cuales son perturbaciones y cuales son variables manipuladas.
1. Viendo la grafica de las entradas anterior, analizar:
    - cuando entran la perturabación y de que dimensión
    - cuando entra la señal de control y de que dimensión es y como afecta
    
1. Graficar la salida $y$ obtenida de la simulación del sistema. Analizar la respuesta. 
    - analizar como varian las salidas condierando la gráficas de $T1$ y $T2$
    - es correcto usar $Q1$ para controlar $T1$ o es mejor usar $Q2$ para tal fin

Ayuda: 
- Utilizar como referencia el código de las gráficas de $U$ para hacer la gráfica de $y$
- con `y.shape` y `t.shape` obtenemos la "forma" de la señal. Por ejemplo, al señal $U$ de la figura anterior tiene `(2, 2000)`, es decir, 2 filas (una para $u$ y otra para $w$) y 2000 columnas (una para cada instante simulado).
- para hacer el diagrama de bloques usar como referencia el apunte de introducción a señales y sistemas.

```{code-cell} ipython3

```
