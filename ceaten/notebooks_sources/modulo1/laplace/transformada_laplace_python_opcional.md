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

# Transformada de Laplace

+++ {"lang": "es", "tags": [], "jp-MarkdownHeadingCollapsed": true}

## Definición

Es una función matemática que utilizaremos para transformar señales en el dominio temporal a un dominio de frecuencia generalizada, que llamaremos dominio transformado de *Laplace*.

La transformada de Laplace se define como

$$F(s) = \mathcal{L}\{f(t)\} = \int_0^\infty f(t) e^{-st} \mathrm{dt}$$

donde $s$ es una variable compleja $s = \sigma + j\omega$.

+++ {"slideshow": {"slide_type": "slide"}}

## Antitransformada de Laplace

Se puede demostrar que teniendo la función transformada $F(s)$, se puede recuperar la función en el dominio temporal $f(t)$ aplicando la antitransformada de Laplace:

$$f(t)=\mathcal{L}^{-1}\{F(s)\} =\frac{1}{2\pi j} \int_{\sigma-j\omega}^{\sigma+j\omega} F(s) e^{st} ds .$$

+++

```{figure} bg2.png
:name: tabla_laplace
:width: 600px
:align: center
:alt: Tabla de transformas de Laplace

Tabla de transformas de Laplace
```

+++

## Propiedades de la Transformada de Laplace

- **Linealidad**: $\mathcal{L}\{kf(t)\} = k F(s)$; $\mathcal{L}\{f_1(t)+f_2(t)\} = F_1(s)+F_2(s)$
- **Corrimiento en frecuencia**: $\mathcal{L}\{e^{-at}f(t)\}=F(s+a)$
- **Corrimiento en el tiempo**: $\mathcal{L}\{f(t-T)\}=e^{-sT}F(s)$
- **Escaleo Temporal**: $\mathcal{L}\{f(at)\}=\dfrac{1}{a}e^{-sT}F\left(\dfrac{s}{a}\right)$

+++

- **Derivada**: $\mathcal{L}\left\{\dfrac{df(t)}{dt}\right\}=sF(s)-f(0)$
- **Derivada segunda**: $\mathcal{L} \left\{ \dfrac{d^2f(t)}{dt^2} \right\}=s^2F(s)-sf(0)-f'(0);$
- **Derivada de orden n**: $\mathcal{L} \left\{ \dfrac{d^nf(t)}{dt^n} \right\}= s^n F(s)- s^{n-1}f(0) - s^{n-2}f'(0) - \ldots - sf^{n-2}(0)-f^{n-1}(0)$
- **Integral**: $\mathcal{L} \left\{ \int_0^tf(\tau)d\tau \right\} =\dfrac{F(s)}{s}$
- **Teorema de valor final**: $f(\infty)=\lim_{s\rightarrow 0}sF(s)$
- **Teorema de valor inicial**: $f(0)=\lim_{s\rightarrow \infty}sF(s)$

El **teorema del valor final** lo estaremos usando en las próximas clases para analizar que sucede con la salida de cun sistema luego de un tiempo muy largo (infinito).

+++
