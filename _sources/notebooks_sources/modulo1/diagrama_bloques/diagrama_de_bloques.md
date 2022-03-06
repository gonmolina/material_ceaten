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

# Diagramas de bloques

+++

## Diagrama de bloques: concepto

Una forma esquemática de representar los sistemas de control es a través de los diagramas de bloques. En dicho diagrama identificamos los principales componentes como bloques, omitiendo detalles y mostrando la dirección principal de la información y la relación de causalidad entre componente y otro.

En la siguiente figura podemos ver el diagrama de bloques genérico del sistema de control realimentado.


```{figure} fig1.png
:name: diagrama-general
:alt: Diagrama de control general de sistema controlado
:width: 60%
:align: center

Diagrama de control general de sistema controlado
```

Decimos que este sistema está realimentado, por que podemos ver que usamos la salida, que para este caso en particular es la medición de temperatura, para calcular y/o modificar la entrada al sistema. En este diagrama de bloques el resultado del sensor de salida se compara, mediante una resta con el sensor de la referencia.

+++

### Ejemplo de sistema de control representado por diagrama de bloques

Sn la siguiente figura mostramos como ejemplo de diagrama de bloques el sistema de control de una caldera controlado por un termostato.


```{figure} fig2.png
:name: control_general
:alt: Sistema de control general
:width: 80%
:align: center

Diagrama de control de temperatura
```

+++

## Diagramas de bloques como representación matemática

Los diagramas de bloques, no solo pueden ser conceptuales, sino que también pueden ser usados para representar matemáticamente los sistemas.

En un diagrama de bloques cada bloque del diagrama representa matemáticamente una parte del sistema, y las lineas son las señales de entrada y de salida de cada una de las partes del sistema. Así el sistema es dividido en subsistemas más pequeños y fáciles de resolver.

+++

## Reducción de los diagramas de bloques usando algebra de bloques

Podemos encontrar diversos sistemas de control, representados con diagramas de bloques complejos. Dichos diagramas los podemos reducir a un simple bloque empleando las reglas del algebra de bloques.

A continuación demostraremos estas reglas mediante operaciones algebraicas.

+++

### Bloques en serie

```{figure} fig3.png
:name: bloques-serie
:alt: BLoques en serie
:align: center

Bloques en serie
```

$$ G(s) = \frac{Y(s)}{U(s)} = \frac{G2(s).X(s)}{U(s)} = \frac{G2(s).(G1(s).U(s))}{U(s)} = {G1(s).G2(s)} $$

+++

### Bloques en paralelo


```{figure} fig4.png
:name: bloques-paralelo
:alt: Bloques en paralelo
:align: center

Bloques en serie
```

$$ G = \frac{Y(s)}{U(s)} = \frac{X1(s)+X2(s)}{U(s)} = \frac{G1(s).U(s)+G2(s).U(s)}{U(s)} = \frac{(G1(s)+G2(s)).U(s)}{U(s)} = G1(s) + G2(s) $$

+++

### Sistema realimentado

$$X1(s)  = U(s) - X2(s) = U(s) - Y(s).G2(s) $$

$$Y(s) = X1(s).G1(s) = \left(U(s) - Y(s).G2(s)\right).G1(s) = U(s).G1(s) - Y(s).G2(s).G1(s)$$

$$Y.(1+G1(s).G2(s)) = U(s).G1(s)$$

$$G = \frac{Y(s)}{U(s)} =\frac{G1(s)}{(1+G1(s).G2(s))}$$


```{figure} fig5.png
:name: bloques-realimentados
:alt: Bloques realimentados
:align: center

Bloques realimentados
```

+++

### Otras transformaciones útiles en el algebra de diagramas de bloque

```{figure} fig6.png
:name: transformaciones-utiles
:alt: transformaciones útiles
:align: center

Transformaciones útiles
```

+++

### Ejemplo de diagrama de bloques

+++

Tenemos el diagrama de bloques de la figura, el cual queremos reducir.

```{figure} fig7.png
:name: ejemplo1
:alt: ejemplo
:align: center

Ejemplo de simplificación de diagrama de bloques
```

+++

#### Resolución a mano

+++

En las siguientes dos figuras mostramos dos reducciones sucesivas al diagrama del ejemplo.

```{figure} fig8.png
:name: primer-paso
:alt: primer-paso
:align: center

Primer paso de simplificación
```

+++


```{figure} fig9.png
:name: segundo-paso
:alt: segundo-paso
:align: center

Segundo paso de simplificación
```

+++

Finalmente, en la siguiente figura obtenemos la función de transferencia $G(s) = \dfrac{Y(s)}{R(s)}$:

$$ G(s) = \dfrac{Y(s)}{R(s)}=\dfrac{\dfrac{G_1.G_2}{1-G_1.G_3}}{1+\dfrac{G_1G_2G_4}{1-G_1G_3}}\left(G_5+\frac{G_6}{G_2}\right)$$

$$ G(s)=\dfrac{G_1G_2G_5+G_1G_6}{1-G_1G_3+G_1G_2G_4} $$

+++

