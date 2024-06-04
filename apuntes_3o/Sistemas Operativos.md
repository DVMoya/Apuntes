___
# ÍNDICE
___

- [[#TEMA 1 PROCESOS]]

___
# TEMA 1 : PROCESOS
___

## CONCEPTO DE PROCESO

- **Programa:** Colección de instrucciones y datos, almacenados en un fichero *(estructura pasiva).*
- **Proceso:** Instancia de un programa en ejecución, requiriendo para ello unos recursos *(estructura activa).*
- En los sistemas operativos actuales podemos instanciar varios programas al mismo tiempo.
- Aunque su ejecución parezca simultánea, en realidad la CPU salta de un proceso a otro. Dicha ejecución se denomina **concurrente.**
	- Cuando hay varias CPUs además podemos tener ejecuciones **paralelas:** varios procesos se ejecutan a la vez.

## TIPOS DE PROCESOS

Los procesos se pueden clasificar en función de distintos criterios:

- **Acceso a CPU y recursos**
	- Apropiativos
	- No apropiativos
- **Permanencia en memoria**
	- Residentes
	- Intercambiables
- **Nivel de privilegio (no en todos los SOs)**
	- Privilegiados
	- No privilegiados

## KERNEL VS PROCESOS DE USUARIO

- **Kernel**
	- El corazón del SO.
	- Proporciona distintos servicios a los procesos de usuario.
- **Procesos de usuario**
	- Ejecutan sus propias operaciones, sin acceso directo a operaciones que puedan provocar problemas en el kernel o en otros procesos.

## SISTEMA OPERATIVO UNIX/LINUX

![[unix1.png|500]]![[unix2.png|500]]

- *UNIX: familia de SOs con características propias.*
- *Todas las distribuciones de GNU/Linux tienen el mismo kernel*
- Android, Chrome OS, Steam OS.
- MacOS/IOS
- PS3 y PS4 (probablemente la PS5 también)
- Tesla
- Routers
- Gran Colisionador de Hadrones (LHC)
- Windows (tiene un subsistema que ejecuta el kernel de Linux)

## EJECUCIÓN DE PROGRAMAS

- Cada máquina emplea un formato diferente.
- Linux utiliza el formato **ELF** (Executable and Linkable Format).
- ELF es el formato de una estructura pasiva.
- Otros formatos:
	- Windows: *PE* (Portable Executable)
	- MacOS: *Mach-o*

![[formato_elf.png|300]]

Cuando un SO carga un programa para ser ejecutado debe:
1) Asignarle un **identificador** único.
2) Asignar un **espacio de memoria** para el programa.
3) Actualizar las **estructuras del kernel** para gestionarlo.
4) Pasarlo a la **cola de preparados.**

## UN PROCESO EN MEMORIA

- **Se carga un único proceso y se ejecuta al mismo tiempo.**
	- Podrá usar toda la memoria.
	- Una zona en memoria dedicada al sistema operativo.
	- No se pueden ejecutar varios procesos al mismo tiempo.

![[memoria_un_proceso.png|100]]

### Particiones Múltiples

El **sistema de particiones múltiples** consiste en dividir la memoria en múltiples segmentos (tamaño variable) y situar los procesos dentro de los mismos

![[particiones_multiples_1.png|400]]

*Problema 1 - Creación de Huecos*

![[particiones_memoria_2.png|270]]

*Problema 2 - Crecimiento de Procesos*

Los procesos aumentan de tamaño con el tiempo, si no hay espacio contiguo se necesita una comparación de memoria artificial (no es eficiente).

### Direccionamiento Artificial

El **direccionamiento artificial** consiste en realizar una translación de las direcciones de memoria utilizadas por los procesos *(direcciones lógicas/virtuales)* a direcciones reales en memoria física *(direcciones físicas).*

> El SO hace creer al proceso que todo el espacio de direcciones físicas es suyo.

Funcionamiento básico:
1) La imagen virtual de cada proceso se divide en pequeños trozos de memoria denominados *páginas lógicas.*
2) Se divide de la misma forma la memoria física en *páginas físicas.*
3) Se realiza un mapeo entre páginas lógicas y páginas físicas.

pag11