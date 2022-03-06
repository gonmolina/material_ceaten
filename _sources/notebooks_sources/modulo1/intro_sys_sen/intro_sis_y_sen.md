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

<!-- markdownlint-disable MD033 -->

# Definiciones de Sistemas y Señales

* **Sistema**: conjunto de componentes que interactúan entre si.
* **Señal**: es una función, típicamente del tiempo, y posiblemente de alguna otra variable (como ser coordenadas espaciales) que representa alguna magnitud de interés asociada con el sistema.

+++

## Señales

### Ejemplos de señal

#### Señales de Voz (variable independiente: tiempo)

```{code-cell} ipython3
:tags: [remove-input]

from scipy.io import wavfile
import IPython
import numpy as np
import matplotlib.pyplot as plt
```

Podemos escuchar el sonido aquí que "visualizaremos" luego en una figura aquí:

```{code-cell} ipython3
:tags: [remove-input]

IPython.display.Audio(filename='sorohanro_-_solo-trumpet-06.wav')
```

```{code-cell} ipython3
:tags: [remove-input]

wav=wavfile.read('sorohanro_-_solo-trumpet-06.wav')
s=np.array(wav[1])
final_time = 3.5
frequency = wav[0]
num = round(final_time*wav[0])
t=np.linspace(0., num/frequency, num)

fig, ax = plt.subplots(1,2, figsize=(12,4))
ax[0].plot(t, s[0:num])
ax[0].set_title('Ejemplo audio: solo trompeta')
ax[0].set_xlabel('tiempo');
ax[0].set_ylabel('Amplitud de la señal')
ax[0].grid()
ax[1].plot(t, s[0:num])
ax[1].set_title('Ejemplo audio: solo trompeta')
ax[1].set_xlim([2.,2.2]);
ax[1].set_xlabel('tiempo');
ax[1].set_ylabel('Amplitud de la señal')
ax[1].grid()
fig.tight_layout()
```

#### Señales en un electrocardiógrafo, o electroencefalógrafo (variable independiente tiempo)

```{figure} signal_electro.png
:name: ectrocardiograma
:alt: ectrocardiograma
:align: center
:width: 600px

Señal de un electrocardiograma
```

+++

#### Imagen digital (dos variables independientes: coordenadas espaciales del pixel)


```{figure} signal_image.png
:name: imagen
:alt: imagen
:width: 256
:align: center

Señal de Imagen Digital
```

+++

### Definiciones relativas a las señales

+++

* La interacción de los componentes en el sistema genera señales **observables** y **no observables**. Las **observables** son las que efectivamente se miden.
* Las señales observables que son de nuestro interés son usualmente denominadas **salidas** del sistema y las denotaremos con $y$.
* El sistema está también afectado por estímulos externos. Las señales externas que pueden ser manipuladas son usualmente llamadas **entradas**, que denotamos con $u$
* Las señales externas que no pueden ser manipuladas son llamadas **perturbaciones** que denotaremos en general con $d$.
* Las perturbaciones suelen dividirse en aquellas que pueden medirse directamente y aquellas que se ponen en evidencia sólo a traves de su influencia en las salidas.

+++

## Señales importantes

+++

### Impulso unitario

Esta señal impulso $\rho(t)$ es de la siguiente forma:

1. Amplitud $\dfrac{1}{T}$ en $t=0$.
1. Duración $T$.
1. $T\rightarrow 0.$

Es decir es una señal que tiene un area bajo su curva (integral) igual 1, tiene un duración que tiende a 0, y una amplitud que tiende a infinito.

Físicamente esta señal es irrealizable. Sin embargo modela bien la física en algunos eventos cotidianos, como puede ser la fuerza aplicada un cuerpo cuando se le da un martillazo, el chispazo ocurrido cuando se desenchufa un artefacto eléctrico (modela la tensión), etc.

+++

### Señal escalón

La señal escalón se define de la siguiente manera:

$$\mu(t) = \left\{
\begin{eqnarray}
0\quad &\quad \text{si}& t<0\\
1\quad &\quad \text{si} &t\geq 0\\
\end{eqnarray} \right.$$

+++

### Relación entre el escalón y el impulso unitario

La relación entre el impulso y el escalón es la siguiente:

$$\frac{d\mu(t)}{dt} = \rho(t)$$

Es decir, la derivada de la función escalón es la función impulso unitario.

+++

## Sistemas

### Esquema básico de un sistema
```{figure} sis_general2.png
:align: center
:width: 400px
:alt: Esquema de sistema
:name: Esquema de sistema

Esquema de sistema
```
Los sistemas no necesariamente están restringidos a sistemas físicos. Pueden ser biológicos, económicos, computacionales, informáticos, sociales, etc.

+++

### Ejemplos de sistema

+++

#### Sistema de Calefacción Sistema de Calefacción Solar Solar

+++

```{figure} calefa_solar.png
:name: calefa_solar
:alt: calefacción solar
:width: 450px
:align: center

Sistema de calefacción solar
```

+++

```{figure} esquema_calefa_solar.png
:alt: Esquema de calefacción solar
:width: 450
:align: center
:name: esquema_calefa_solar

Esquema de calefacción solar
```

+++

#### Ecosistema

Ambiente aislado compuesto por dos clases de individuos: presas (P: población de presas) y depredadores (D: población de depredadores).

Hipótesis del modelo:

1. En ausencia de depredadores (D=0), la población de presas crece exponencialmente.
1. Los depredadores sólo se alimentan de presas, por lo que en ausencia de presas (P=0), la población de depredadores se extingue exponencialmente.

+++

Un posible modelo que verifica estas hipótesis es el de **Lotka-Volterra**

$$
\begin{eqnarray}
\frac{dP(t)}{dt}&=\alpha_1P(t)-\alpha_2D(t)P(t)\\
\frac{dD(t)}{dt}&=\alpha_3P(t)D(t)-\alpha_4D(t)
\end{eqnarray}
$$

+++

## Propiedades de los sistemas

+++

### Linealidad

Un sistema es **lineal** si verifica el **Principio de Superposición**, tanto para entradas como para condiciones iniciales.

Si para una entrada $u_1$ aplicada en el instante $t_0$, con el sistema en un estado inicial $\sum_0$, la salida es $y_1$ , y para una entrada $u_2$ aplicada en el instante $t_0$, con el sistema en un estado inicial $\sum_0$, la salida es $y_2$
entonces si se aplica una $c_1u_1 +c_2u_2$  entrada en el instante $t_0$, con el sistema en un estado inicial $\sum_0$, la salida será $c_1y_1 +c_2y_2$

+++

```{figure} superposicion1.png
:alt: Hipotesis de superposición
:width: 450
:align: center
:name: hipotesis_superp

Hipótesis linealidad
```


+++

```{figure} superposicion2.png
:alt: Resultado de superposición
:width: 400
:align: center
:name: resultado_superp

Requerimiento linealidad
```

+++

* Es claro que esta propiedad, como fue definida, es imposible de verificar en la práctica, ya que no se pueden realizar los ensayos propuestos en el mismo período de tiempo.
* Debemos asumir entonces que el sistema no cambia con el tiempo (propiedad de **estacionariedad** o **invariancia en el tiempo**, que definiremos a continuación), de manera que podemos realizar los ensayos a distintos tiempos a partir del sistema en el mismo estado inicial.
* Un sistema que no verifica el principio de Superposición se denomina **no lineal**.

+++ {"slideshow": {"slide_type": "slide"}}

### Invariancia en el tiempo

Un sistema es invariante en el tiempo si su salida es siempre la misma cada vez que se aplique la misma entrada (para las mismas condiciones iniciales), sin importar el instante en que se aplique la entrada. Para dar una definición más precisa, es necesario definir el operador desplazamiento temporal que notaremos: $z_{\Delta}$  que aplicado a una función del tiempo, la desplaza temporalmente un intervalo $\Delta$, es decir:



#### Desplazamiento temporal

 
```{figure} estacionariedad.png
:alt: Desplazamiento temporal
:width: 400px
:name: desplazamiento
:align: center


Operador Desplazamiento temporal
```

Por lo tanto, el sistema es estacionario estacionario si para una entrada $u(t)$ aplicada en el instante $t_0$ resulta la salida es $y(t),$ entonces para una entrada = $z^\Delta u(t)$ aplicada en $t_0+\Delta$ la salida es $\tilde y(t) =z^\Delta y(t)$



#### Principio de estacionariedad o invariancia en el tiempo


```{figure} estacionariedad2.png
:alt: Principio de invariancia
:width: 400px
:name: invariancia
:align: center

Principio de estacionariedad
````

+++

### Sistemas SISO (Single-Input/Single-Output)

Un sistema con **una** única entrada y **una** única salida se denominan **SISO**

### Sistemas MIMO (Multiple-Input/Multiple-Output)

Sistemas con **múltiples** entradas y **múltiples** salidas se denominan **MIMO**

Existen ademas las variedades SIMO y MISO, que dejamos al lector que intuya a que se refieren esos nombres.

+++

### Sistemas Estáticos y Dinámicos

Un sistema en el cual la salida en el instante $t$ depende exclusivamente de la entrada en ese instante $t$ es llamado **Sistema Estático** o sin memoria. En contraposición, un **Sistema Dinámico** es uno en el cual la salida en el instante $t$ depende también de valores pasados y/o futuros de la entrada, además del valor en $t$.

Los sistemas que estudiaremos en esta materia son los sistemas dinámicos, es decir que el valor de la salida actual depende no solo de las entradas actuales sino también de los valores de la entradas pasadas. Aunque diseñaremos también algunos controladores que pueden considerarse estáticos, es decir que cuya salida solo depende de valores presentes de la entrada del controlador

+++

### Sistemas Causales y No causales

Un sistema es **causal** si su respuesta a una entrada no depende de valores futuros de esa entrada y/o valores futuros de salidas. Un sistema que no verifica esta propiedad es llamado **no causal**. En particular un sistema se dice **anticausal** si su respuesta a una entrada depende exclusivamente de valores futuros de esa entrada y/o valores futuros de salidas.

Todos los sistemas físicos son **causales**.

+++

## Caracterización de tipos de sistemas

Desde el punto de vista de las ecuaciones matemáticas los sistemas se puedes clasificar como:

+++

| Tipo de Sistema             |    Ecuaciones del Modelo                       |
|-----------------------------|------------------------------------------------|
|   Lineal                    |    Ecs. Lineales                               |
|   No Lineal                 |    Ecs. no Lineales                            |
|   Invariante en el tiempo   |    Ecs. a coeficientes constantes              |
|   Variante en el tiempo     |    Ecs. a coeficientes en función del tiempo   |
|   Parámetros concentrados   |    Ecs. dif. Ordinarias                        |
|   Parámetros distribuidos   |    Ecs. dif. Parciales                         |
|   de tiempo continuo        |    Ecs. diferenciales                          |
|   de tiempo discreto        |    Ecs. en diferencias                         |
|   SISO                      |    Número de Ecs. del modelo                   |
|   MIMO                      |                                                |
|   Determinístico            | x (variable determinística)                    |
|   Estocástico               | $<x>$, $\sigma$ (valor medio y desvío estándar)|         |

+++

### Ejemplo completo de un sistema electromecánico (motor eléctrico)

#### Esquema de la idealización física del motor eléctrico

```{figure} fig_circuito_motor.png
:alt: diagrama del motor de continua
:name: diagrama_motor
:align: center
:width: 450px

Diagrama idealizado del motor de corriente continua
```

+++

#### Diagrama del sistema desde el punto de vista de entradas y salidas

```{figure} esquema_motor.png
:name: motor_es
:width: 450px
:align: center
:alt: Esquema Rotacional

Esquema entrada/salida del motor de corriente continua
```

+++

#### Descripción del motor y su funcionamiento

A continuación se deja un video describiendo las partes de un motor y la forma de funcionamiento.

[![motor: descripción](motor_parte0.png)](https://youtu.be/ztMgB1UofxU "Motor eléctrico: descripción")

+++

#### Modelado del motor

Los modelos matemáticos proveen de una predicción de como el sistema se va a comportar o evolucionar. En general los modelos matemáticos **NO son exactos**. Sin embargo, serán útiles para el diseño de los sistemas de control, debido a que este deberá proveer de la robustez requerida mediante el uso de la realimentación.

Algunas  simplificaciones que consideraremos para este modelo son:

1. La resistencia, inductancia, masa (o momento de inercia) y "viscosidad" son constantes. Es decir, no contemplaremos cambios de ningún tipo, como por ejemplo el efecto de la temperatura.
1. El rozamiento viscoso es lineal. Es decir, la viscosidad es es proporcional a la velocidad ($\tau_d=D_m*\omega$).

+++

#### Desarrollo de las ecuaciones

El circuito eléctrico se relaciona con el mecánico, y viceversa, por medio de la siguientes ecuaciones:

$$
\begin{aligned}
V_b(t) &= K_b \frac{d\theta_m(t)}{dt} &\text{(fuerza contraelectromotriz)}\\
 \tau_m(t) &= K_t i_a(t) &\text{(torque del motor)}
\end{aligned}
$$

para las mismas unidades $K_t = K_b$

$$
\begin{aligned}
R_a i_a(t) + L_a \frac{di_a(t)}{dt} + V_b(t) &= e_a(t) & \text{(Ec. de la malla eléctrica de la armadura)}\\
\tau_m(t) - \tau_r(t) - D_m\frac{d\theta_m(t)}{dt} &= J_m \frac{d^2\theta_m(t)}{dt^2} & \text{(Ecs. mecánica)}
\end{aligned}
$$

+++

Reemplazando obtenemos el sistema de ecuaciones de parámetros concentrados (no depende de la ubicación espacial de los componentes del sistema), lineal (cumple con superposición) e invariante en el tiempo (su comportamiento no cambia con el tiempo). Como el sistema es lineal e invariante en el tiempo se dice que el sistema es LTI (linear time invariant).

$$
\begin{aligned}
R_a i_a(t) + L_a \frac{di_a(t)}{dt} + K_b \frac{d\theta_m(t)}{dt} &= e_a(t) \\
K_t i_a(t) - \tau_r(t) - D_m\frac{d\theta_m(t)}{dt} &= J_m \frac{d^2\theta_m(t)}{dt^2}
\end{aligned}
$$
