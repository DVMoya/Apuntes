___
# ÍNDICE
___

- [[#TEMA 1 PROCESOS]]
- [[#TEMA 2 PROCESOS EN POSIX]]
- [[#TEMA 3 FICHEROS Y COMUNICACIONES EN UNIX]]

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

### Utilización de los Distintos Segmentos de Memoria

- **Stack**
	- *Ventajas:*
		- Acceso muy rápido.
		- No es necesario eliminar las variables una vez utilizadas.
		- Uso eficiente del espacio y la memoria no queda fragmentada.
	- *Desventajas:*
		- Sólo variables locales.
		- Tamaño del segmento limitado.
		- Las variables no pueden ser redimensionadas.
- **Heap**
	- *Ventajas:*
		- Variables globales.
		- Tamaño del segmento muy grande.
		- Variables pueden ser redimensionadas.
	- *Desventajas:*
		- Acceso más lento.
		- Uso ineficiente del espacio y memoria almacenada.
		- El encargado de reservar y liberar memoria es el propio proceso: explícitamente con un *garbage collector.*

## INFORMACIÓN SOBRE LOS PROCESOS EN EL SO

Al cargarse un proceso, se crea en memoria su **bloque de control de proceso (PCB)**. Los PCBs sólo son accesibles desde el kernel, y se almacenan en el espacio de direcciones de éste.

### Estructura de un PCB

El PCB de un proceso contiene información de varios tipos:
- *Identificación* (del proceso, usuario, grupo...)
- *Planificación/Control* 
- *Información de ejecución* 

En los sistemas UNIX estándar se distingue entre el PCB (información que siempre está disponible para el kernel) y el *u-area* (información solo necesaria cuando el procesa está en ejecución). Por el contrario, en Linux no existe tal diferencia (solo se trabaja con PCBs).

### Lista de PCBs en Linux

- En UNIX estándar los PCBs se acceden utilizando una estructura denominada **tabla de procesos.**
- En Linux los PCBs se acceden utilizando una **lista circular doblemente enlazada.**
- Dicha lista es gestionada por el **scheduler.**

![[pcb_linux_lista.png|400]]

## MODOS DE EJECUCIÓN DE PROCESOS DE USUARIO

La ejecución de un proceso de usuario en sistemas UNIX está dividida en dos niveles:
- **Modo usuario:** el proceso puede acceder a sus propios datos e instrucciones, pero no a los del kernel u otros procesos.
- **Modo kernel:** si un proceso quiere ejecutar una operación privilegiada debe realizar una llamada al kernel, que será el que realmente la ejecute. Decimos que el proceso de usuario está *temporalmente* en modo kernel.

El cambio de modo usuario a kernel se realiza, fundamentalmente, por dos motivos:
- Por una **interrupción del sistema:** interrupciones de reloj, pulsaciones de una tecla, movimiento del ratón, etc.
- Por una **llamada al sistema:** leer/escribir en un fichero, abrir una conexión red, etc.

> Cuando se cambia de modo usuario a modo kernel se ha de salvar el *modo del proceso* para poderlo restaurar posteriormente.

Para permitir o restringir los accesos a las distintas funciones del sistema se utilizan los **niveles de protección** proporcionados por la CPU.

![[niveles_de_proteccion.png|400]]

## ESTADOS DE EJECUCIÓN DE UN PROCESO

Cuando un proceso se ejecuta pasa por diferentes estados de ejecución:
- *Nuevo*
- *Listo o Preparado*
- *En Ejecución*
- *Bloqueado*
- *Finalizado*

### Estructura de Datos para Gestionar la Ejecución de los Datos del Proceso

1. Puntero al PCB que está usando la CPU (puntero *current*).
2. Listas de los PCBs que se encuentran en distintos estados.
3. Puntero a la cola de descriptores de recursos.
4. Identificadores de las rutinas para tratar interrupciones de hardware o software, o errores indeseados.

## PLANIFICACIÓN DE PROCESOS

### Activación

En sistemas con multiprocesamiento hay que cambiar regularmente la CPU de un proceso *(task)* a otro.

- Un proceso deja voluntariamente la CPU.
- Ha terminado el tiempo asignado al proceso en ejecución.
- Interrupción de hardware.

### Mecanismos

La decisión de cuando hay que pasar un proceso de listo a ejecución, y viceversa, es tomada por un elemento del kernel del sistema operativo denominado planificador *(scheduler).*

Tiene dos partes:
- **Algoritmo de planificación.**
- **Dispatcher.**

### Cambio de Contexto

El **contexto de un proceso** consiste en el conjunto de estados necesarios para que éste se ejecute.

- Cuanto un proceso se está ejecutando, su contexto reside en los registros del computador.
- Cuando no se está ejecutando, este contexto reside en memoria (PCB del proceso), para ser restaurado cuando vuelva a ser ejecutado.

Lo que realmente hace el *dispatcher* es realizar loa *cambios de contexto* de los distintos procesos. 

Las operaciones de cambio de contexto son más costosas que las de cambio de modo del proceso.

Pasos a realizar para realizar un cambio de contexto:
1. Salvar el estado del procesador.
	1. Contador de programa (PC).
	2. Registros de la CPU.
	3. Recursos que está utilizando.
2. Actualizar los campos PCB.
3. Mover el PCB a la cola apropiada (Listo o Bloqueado).
4. Selección del nuevo proceso a ejecutar: realizado por el planificador.
5. Actualizar el PCB del proceso elegido (estado En Ejecución).
6. Actualizar estructuras de datos de gestión de memoria.
7. Restaurar el estado del procesador  al mismo estado en que se interrumpió el nuevo proceso elegido para ejecutarse.

___
# TEMA 2 : PROCESOS EN POSIX
___

## SERVICIOS POSIX PARA GESTIÓN DE PROCESOS

- **POSIX** (**P**ortable **O**perating **S**ystem **I**nterface)
- Son una *familia de estándares* de llamadas al sistema operativo.
- Persiguen generalizar las interfaces de los sistemas operativos para que una misma aplicación pueda ejecutarse en diferentes plataformas.

## JERARQUÍA DE PROCESOS EN POSIX

Todo proceso tiene asociados dos números desde su creación:
- **PID** (Process Identifier)
- **PPID** (Parent Process Identifier)

## DESCRIPCIÓN DE LA FUNCIÓN fork()

- La función **fork()** sirve para crear un nuevo proceso a partir de uno ya existente.
	- *Proceso padre:* el que invoca el fork().
	- *Proceso hijo:* el nuevo proceso, hijo del padre.
- El proceso hijo es una réplica exacta del padre *(clon).* 

![[fork.png|300]]

Tras la clonación:
- El proceso hijo ocupa una zona de memoria independiente, pero con el mismo contenido que el padre.
- El contador de programa *(PC)* de ambos procesos tiene el mismo valor. La ejecución de cada proceso continúa después del fork().
- Ambos procesos comparten los punteros de posición de los ficheros abiertos en ese momento.

> Los cambios que se realizan posteriormente en cada uno de ellos **NO** afectará al otro.

**fork();** devuelve:
- **Al proceso padre:** el *PID* del hijo.
- **Al proceso hijo:** *0*.
- **Error:** *-1*.

**getpid();** devuelve: el PID del proceso que realiza la llamada.

**getppid()** devuelve: el PPID, o sea, el PID del proceso padre.

> Sincronización entre procesos (tema 7 de la asignatura): funciones *exit()* y *wait().*

## TERMINACIÓN DE PROCESOS

La terminación de un proceso padre no afecta a sus procesos hijos, aunque éstos quedan *huérfanos* y son adoptados por el proceso *init* (sus PPIDs serán 1).

![[procesos_huerfanos.png|500]]

La terminación de un proceso hijo sí que puede afectar a un proceso padre:
- Si el proceso padre está en espera debido a una función *wait().*
- El proceso que invoca la función *exit()* queda en estado **zombie** hasta que el padre ejecute la función *wait()* o finalice.
	- Cuando un proceso se encuentra en estado **zombie** libera el espacio de memoria que ocupaba, excepto su PCB.

### LA FUNCIÓN exit()

- **void exit(int estado);**
- Esta función finaliza la ejecución del proceso que la invoca.
- No es imprescindible, pero sí recomendable.
- No devuelve ningún valor, pero el valor asignado al parámetro *estado* puede ser utilizado para ser procesado.

### LA FUNCIÓN WAIT()

- Suspende (bloquea) su ejecución hasta que uno de sus procesos hijos (cualquiera) termine. Con **waitpid()** es posible especificar el hijo al que se espera.
- Si no tiene hijos, o los hijo han terminado, no tiene efecto.
- Si algún proceso hijo se encuentra en estado **zombie**, entonces recoge el estado de dicho proceso y tampoco se bloquea.

**wait(int *estado);** devuelve:
- El PID del hijo que ha finalizado (-1 si hay error).
- Parámetro *estado.*

### SINCRONIZACIÓN ENTRE exit() Y wait()

![[exit_y_wait_sync.png|500]]

Ejemplo sincronización simple (exit_wait.c):

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
int main() {
	int estado ;
	if (fork ()!=0) {
		wait(& estado );
		printf ("Soy el padre\n");
	}
	else printf ("Soy el hijo\n");
	exit (0);
}
```

*% ./exit_wait*
Soy el hijo
Soy el padre

## PATRÓN DE CREACIÓN DE PROCESOS

- El proceso padre ejecuta tantos **fork()** como hijos queramos crear.
- Los hijos, una vez ejecutado su código, deben finalizar (con un **exit()**).

Al tener procesos independientes estos pueden ser ejecutados, al mismo tiempo, en distintas CPUs.

![[patron_de_proceso.png|200]]

> En el tema 4 veremos como es posible decidir la prioridad de cada uno de los procesos, así como las CPUs en las que se ejecutarán.

___
# TEMA 3 : FICHEROS Y COMUNICACIONES EN UNIX
___

