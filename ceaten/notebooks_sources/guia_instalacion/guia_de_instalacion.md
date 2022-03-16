# Guía de instalación de las herramientas computacionales

## Verificación del tipo de sistema operativo (32 o 64 bits)

### En Windows 10 y Windows 8.1

Selecciona el botón Inicio y después, ``Configuración > Sistema > Acerca de``. A la derecha, en Especificaciones del dispositivo, consulta Tipo de sistema.

### En Windows 7

Selecciona el botón Inicio, haz clic con el botón derecho en  
``Equipo`` y selecciona `Propiedades`. En `Sistema`, consulta el `tipo de sistema`.

## Descargar Miniconda de acuerdo al tipo de sistema operativo

Seguir el enlace de [Miniconda](https://docs.conda.io/en/latest/miniconda.html) y elegir la versión de `Python 3.X` (donde X es un número entero) que este acorde al tipo de sistema operativo instalado es su máquina según lo averiguado en el punto anterior.

## Instalar Miniconda

Seguir las recomendaciones por defecto dadas por el instalador. Una vez terminada la instalación tendremos Python instalado en nuestro sistema. Además tendremos en el menú de inicio un ítem
que se llama **Anaconda Powershell Prompt**, el cual abriremos para continuar con la instalación de las herramientas del curso.



## Instalación de las herramientas especificas del curso

Para continuar con la instalación necesitaremos descargar el archivo [eecc.yml](https://drive.google.com/file/d/1iM5ek6PpSaf1t52QbAi_dWPjV-lvdqVK/view?usp=sharing) haciendo clock sobre el enlace anterior. Una vez descargado, dirigirse con la consola de Anaconda Powershell Prompt abierta a la carpeta de descargas donde se encuentra el archivo `eecc.yml` descargado anteriormente. En general, para dirigirse a esta carpeta debemos tipear en la consola de Anaconda Powershell:

```bash
cd ~\Downloads\
```

Para verificar que el archivo se encuentre ahí, podemos tipear:

```bash
dir eecc.yml
```

Si nos encontramos en la carpeta donde está el archivo este deberá aparecer luego del comando anterior.

Finalmente para instalar todas las herramientas necesarias en el curso debemos ejecutar en este comando:

```bash
conda env create --file eecc.yml
```

````{warning} 
En caso de que el comando anterior falle, deberá abrir una nueva consola de PowerShell como Administrador y ejecutar

```powershell
set-executionpolicy unrestricted
```
Luego debe contestar Si a Todo. Ahora podremos cerrar la consola de PowerShell como Administrador y continuar con la instalación.
````

Una vez terminado este paso tendremos instaladas todas las herramientas necesarias para la materia. Es necesario tener paciencia ya que este paso puede tardar un tiempo largo dependiendo de la velocidad de conexión. 

### Crear acceso directo a Jupyter Lab

Una vez instaladas todas las herramientas podremos utilizar `jupyter-lab` abreindo la consola de Anaconda Powershell y ejecutando el siguiente comando:

```powershell	
conda activate eecc
jupyter lab
```

Para algunas personas no habituadas a utilizar la consola de comandos esto puede resultar engorroso. Para simplificar esto podemos generar un enlace directo a Jupyter Lab en el escritorio.Los pasos para hacerlo son los siguientes:

1. Sobre el escritorio hacer click con el botón secundario y seleccionar `Nuevo > Acceso directo`.
1. Escribir `%windir%\System32\cmd.exe "/K"  C:\Users\%username%\Miniconda3\Scripts\activate.bat eecc &&  jupyter-lab && exit` donde se pide la `Ubicación del elemento`.
1. Escribir `JupyterLab` donde se pide el nombre del elemento. Luego de esto el enlace debería estar funcionando. Sin embargo, podemos personalizarlo un poco más.
1. Hacemos click secundario sobre el Enlace recién creado y seleccionamos `Propiedades`. Donde está el campo `Iniciar en:` escribimos la ruta de la carpeta donde guardamos todos los cuadernos, por ejemplo `C:\Users\%username%\Documents\elementos_de_control`. De esta forma no será necesario navegar hasta la ruta donde se encuentran los cuadernos cada vez que se abre el Jupyter Lab (o al menos estaremos más cerca).
1. Podemos también cambiar el ícono que se muestra en el escritorio. Para esto podemos descargar este [archivo](https://raw.githubusercontent.com/jupyter/design/master/logos/Favicon/favicon.ico) y luego continuamos la edición de las propiedades del enlace. Seleccionamos la opción `Cambiar icono` y seleccionamos el archivo que acabamos de descargar.

Ahora deberíamos tener un acceso directo a Jupyter Lab en el escritorio. 

## NUEVO! Aplicación JupyterLab de escritorio

Recientemente se lanzó una nueva aplicación JupyterLab de escritorio. Esta aplicación crea un lanzador desde el menu de inicio en windows y se pueden abrir los Notebooks con esta aplicación directamente desde el explorador de archivos. Para instalarlos de debe descargar el siguiente [instalador](https://github.com/jupyterlab/jupyterlab-desktop/releases/latest/download/JupyterLab-Setup-Windows.exe) y ejecutarlo.

Para poder visualizar correctamente los cuadernos del curso será necesario instalar dos paquetes de Python extra. Para esto, po única vez cuando se abra la aplicación JupyterLab se de hacer lo siguiente:

1. Abrir el lanzador de JupyterLab. Para esto seleccionar desde la barra de menú de la aplicación `File > New Launcher`. Deberías ver ahora las al menos algo similar a esta figura (con menos opciones):
```{figure} JupyterLabLauncher.png
:width: 400px
:align: center
:alt: JupyterLabLauncher

Lanzador de JupyterLab
```
2. En la ventana que aparece, seleccionar la opción Python3 (ipykernel), puede ser tanto la que se encuentra debajo de `Notebook` como la que se encuentra debajo de `Console`.
3. Se deberá ejecutar el siguiente comando:
```python
!pip install jupyterlab-myst jupytext
```
Tanto en consola como en un cuaderno copiar y pegar el comando anterior y presionar `Mayúscula + Enter`.
4. Cerrar la consola o el cuaderno y comenzar a utilizar la aplicación.

Recordar que una vez abierto el cuaderno con que el se quiere trabajar se debe seleccionar el kernel `Python 3 (eecc)`, ya que este kernel es el que tiene todas las herramientas de la materia. Esto se hace haciendo click en el recuadro rojo que se muestra en la figura:

```{figure} KernelSelect.png
:width: 400px
:align: center
:alt: KernelSelect

Selector de Kernel en JupyterLab
```











