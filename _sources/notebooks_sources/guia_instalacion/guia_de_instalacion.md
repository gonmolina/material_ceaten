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

