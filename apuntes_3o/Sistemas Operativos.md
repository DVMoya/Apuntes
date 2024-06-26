___
# ÍNDICE
___

- [[#TEMA 1 PROCESOS]]
- [[#TEMA 2 PROCESOS EN POSIX]]
- [[#TEMA 3 FICHEROS Y COMUNICACIONES EN UNIX]]
- [[#TEMA 4 PLANIFICACIÓN DE PROCESOS]]
- [[#TEMA 5 VIRTUALIZACIÓN]]
- [[#TEMA 6 THREADS]]
- [[#TEMA 7 SINCRONIZACIÓN]]

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

## DESCRIPCIÓN DE LA FUNCIÓN *fork()*

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
- **Al proceso hijo:** *0.*
- **Error:** *-1.*

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

### LA FUNCIÓN *exit()*

```c
void exit(int estado);
```
- Esta función finaliza la ejecución del proceso que la invoca.
- No es imprescindible, pero sí recomendable.
- No devuelve ningún valor, pero el valor asignado al parámetro *estado* puede ser utilizado para ser procesado.

### LA FUNCIÓN *wait()*

- Suspende (bloquea) su ejecución hasta que uno de sus procesos hijos (cualquiera) termine. Con **waitpid()** es posible especificar el hijo al que se espera.
- Si no tiene hijos, o los hijo han terminado, no tiene efecto.
- Si algún proceso hijo se encuentra en estado **zombie**, entonces recoge el estado de dicho proceso y tampoco se bloquea.

```c
wait(int *estado);
```
Devuelve:
- El PID del hijo que ha finalizado (-1 si hay error).
- Parámetro *estado.*

### SINCRONIZACIÓN ENTRE *exit()* Y *wait()*

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

> Ficheros en UNIX

___

## OPERACIONES E/S

En UNIX la mayor parte de las operaciones de entrada/salida se realizan mediante el uso de **ficheros.**
- En Linux cada **PCB** mantiene un puntero (llamado *files*) a una tabla de ficheros (llamada *files_struct*), que contiene información de los ficheros que dicho proceso tiene abiertos.
- Cada entrada en **files_struct** está formada por un descriptor de fichero *(fd)*, y un puntero a la dirección de memoria de dicho fichero.

## DESCRIPTORES DE FICHEROS (FD)

Los **fd** pueden referenciar no sólo ficheros "normales", sino dispositivos, directorios, sockets, etc.

- Los **fd** adoptan valores enteros no negativos (-1 si hay error).
- El máximo número de procesos que pueden ser abiertos por un proceso es de **1.024** (se puede configurar hasta 1.048.576).
- Cuando se crea un proceso, por convención, éste tendrá tres descriptores de ficheros abiertos:
	- *Entrada estándar* (descriptor 0).
	- *Salida estándar* (descriptor 1).
	- *Error estándar* (descriptor 2).
- Los procesos hijos heredan una copia de la tabla de ficheros de sus padres.

## ESTRUCTURA DE FICHEROS

![[estructura_fichero_1.png|300]]

## CREACIÓN DE FICHEROS

### Función *creat()*
```c
int creat(const char *nombre, mode_t permisos);
```

- Crea un fichero cuyo nombre es *nombre*, y cuya máscara de permisos es *permisos.*
- Devuelve:
	- Un descriptor de fichero. *Siempre elige el menor número posible.*
	- Si hay error: -1.

### Permisos de Ficheros

- Los permisos de ficheros se representan mediante una máscara de 9 bits, y se suele expresar en octal mediante un número de 3 dígitos.
- **Formato octal:** permiso de *lectura, escritura y ejecución* para el usuario *propietario,* el *grupo de usuarios* al que el usuario pertenece, y el *resto de usuarios.*
*$$	
	rwx\ rwx\ rwx
$$*

## APERTURA DE FICHEROS

### Función *open()*
```c
int open(const char *nombre, int modo, [mode_t permisos]);
```

- Abre el fichero *nombre*, en modo *modo* y con permisos *permisos.*
- Devuelve:
	- Un descriptor de fichero. *Siempre elige el menor número posible.*
	- Si hay error: -1.
- Parámetro **modo:** O_READONLY(*0*), O_WRONLY(*1*), O_RDWR(*2*), O_CREAT, O_TRUNC, O_APPEND, O_EXCEL.

## CIERRE DE FICHEROS

### Función *close()*

**int close(int fd);**

- Cierra el fichero con descriptor *fd.*
- Devuelve:
	- Si todo ha ido bien: 0.
	- Si hay error: -1.

## ESCRITURA DE FICHEROS

### Función *write()*
```c
int write(int fd, const void *dato, size_t n_bytes);
```

- Descripción:
	- En el fichero con descriptor *fd* se escribe, a partir de la posición actual del *puntero de escritura del fichero,* los *n_bytes* que hay en memoria a partir de la posición *dato.*
	- Modifica el valor del *puntero de escritura del fichero:* indica la posición a partir de la cual se escribe el fichero (en nuestro caso, al final del fichero).
- Devuelve:
	- El número de bytes escritos.
	- Si hay error: -1.
- Ejemplo:
```c
n = write(fd, "XXX YYY ZZZ\0", 12);
```

## LECTURA DE FICHEROS

### Función *read()*

```c
int read(int fd, void *dato, size_t n_bytes);
```

- Descripción:
	- Lee los *n_bytes* siguientes a la posición actual del *puntero de lectura del fichero* con descriptor *fd,* y los almacena a partir de la posición de memoria *dato.*
	- Modifica el valor del *puntero de lectura del fichero:* indica la posición a partir de la cual se lee el fichero.
- Devuelve:
	- El número de bytes que ha podido leer. Si no se ha leído nada o se ha alcanzado el final del fichero devuelve 0.
	- Si hay error: -1.
- Ejemplo:
```c
n = read(fd, &i, sizeof(i));
```

## EJEMPLO *fichero_1.c*

> Ejemplo simple de creación, cierre, escritura y lectura de un fichero.

```c
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>

int main() {
	int i , fd , dato; /* (a) */
	
	fd = creat ("prueba " ,0600); /* (b) */
	
	for (i = 0;i < 10;i++)
		write(fd ,&i,sizeof (i));
	close (fd); /* (c) */
	
	fd = open("prueba ",O_RDONLY ); /* (d) */
	while (read(fd ,&dato ,sizeof (int )) > 0)
		printf ("Leído el número %d\n",dato);
	close (fd);
	
	exit (0);
}
```

___

> Comunicación entre procesos.

___

## TUBERÍAS *(Pipes)*

Los procesos en UNIX se comunican mediante **tuberías.**

- Las tuberías *(pipes)* son un tipo de *pseudo-ficheros* manejados por el sistema operativo: son estructuras que se crean en *memoria principal,* no en disco.
- Cada proceso ve a la tubería como un conducto con dos extremos, uno para escribir y otro para leer.
- la lectura y escritura en tuberías se realiza mediante los servicios estándar de lectura/escritura de ficheros.

### Servicios POSIX para la Creación de Tuberías

```c
int pipe(int tubo[2]);
```

- Descripción:
	- Crea una tubería denominada *tubo.*
	- Crea un *descriptor de lectura* de tubo: tubo[0].
	- Crea un *descriptor de escritura* de tubo: tubo[1].
- Devuelve:
	- Si todo ha ido bien: 0.
	- Si hay error: -1.

> Las tuberías se utilizan para la comunicación entre padres e hijos, o procesos emparentados. Para ello hay que crear la tubería (con *pipe()*) antes de ejecutar *fork().*

### Escritura y Lectura en Tuberías

**Escritura en una tubería:**
- En una tubería se escribe mediante la función *write().*
- Si la tubería está llena o se llena durante la escritura en curso, la operación bloquea el proceso escritor hasta que se pueda completar.

**Lectura en una tubería:**
- Una tubería se lee mediante la función *read().*
- Una vez realizada la lectura se vacía el contenido leído de la tubería.
- Si la tubería está vacía, la operación bloquea al proceso lector hasta que:
	- O bien se pueda completar la operación.
	- O bien se haya alcanzado el *final del fichero:* devuelve 0.

> En una tubería, *el final del fichero* se alcanza cuando la tubería está vacía, y **ADEMÁS** no hay ningún proceso con la tubería abierta para escritura.

> Es conveniente cerrar todos los descriptores de tubería cuando vayan a ser utilizados ya que así evitamos problemas.

## EJEMPLO *tuberías_2.c*

**ENUNCIADO:**
Realizar un programa que cree dos procesos: el proceso padre generará los 100 primeros números pares (y los imprimirá por pantalla) y el hijo los 100 primeros números impares (y también los imprimiré por pantalla). Los números han de mostrarse en orden creciente. Utilizaremos una tubería para pasar un testigo, que indicará qué proceso debe imprimir.

**SOLUCIÓN:**
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#define MAX 200

int main() {
	int i, testigo = 1, t[2];
	pipe(t);
	if(fork () != 0) {
		write(t[1], &testigo, sizeof(int));
		i=1; /* El padre imprime los impares */
		while (i <= MAX) {
			read(t[0], &testigo, sizeof(int));
			printf ("Proceso %d: %d\n", getpid(), i);
			i = i + 2;
			write(t[1],& testigo , sizeof (int ));
		}
		close(t[0]);
		close(t[1]);
	} else {
		i=0; /* El hijo imprime los pares */
		while (i <= MAX) {
			read(t[0], &testigo, sizeof(int));
			printf ("Proceso %d: %d\n", getpid (), i);
			i = i + 2;
			write(t[1], &testigo, sizeof(int));
	}
	close(t[0]);
	close(t[1]);
}
exit
```

**ESQUEMA:**
![[ejemmplo_tuberias_1.png|500]]![[ejemplo_tuberias_2.png|500]]

___
# TEMA 4 : PLANIFICACIÓN DE PROCESOS
___

## COMPORTAMIENTO DE LOS PROCESOS

![[comportamiento_procesos.png|500]]

## PLANIFICACIÓN

### Situaciones Reales

- Varios procesos pueden requerir la CPU al mismo tiempo.
- Algunos procesos pueden querer utilizar la CPU por mucho tiempo.
- Puede que todos los procesos estén esperando para realizar operaciones de E/S al mismo tiempo.

### Objetivos

1. **Justicia (*fairness*):** que cada proceso obtenga una proporción de CPU justa o razonable.
2. **Eficiencia:** que la CPU esté ocupada y no gaste mucho tiempo decidiendo.
3. **Throughput:** conseguir que la mayor parte de los procesos acabe lo antes posible.
4. **Tiempo de respuesta:** minimizar el tiempo que los usuarios deben esperar a obtener alguna respuesta.
5. **Fiabilidad:** evitar perder datos, reaccionar en tiempo límite, etc.
6. **Predecibilidad:** degradación no brusca.

### Planificador *(Scheduler)*

El panificador *(scheduler)* está formado por dos componentes:
- **Algoritmo de planificación:** decide que proceso utilizará la CPU durante un determinado intervalo de tiempo.
- **Dispatcher:** mecanismo encargado de realizar los cambios de contexto.

### Situaciones en que Actúa

1. El proceso actual *termina.*
2. El proceso actual pasa de un estado de *ejecución* a uno de *bloqueado.*
3. El proceso actual pasa de *bloqueado* a *listo.*
4. Una *interrupción* le indica al planificador que un proceso en *ejecución* debe pasar a *listo.*

Las causas 3 y 4 solo se dan en **planificadores expulsivos (*preemptive*):** el planificador puede desalojar el proceso en ejecución y cambiarlo por otro.

## ALGORITMOS DE PLANIFICACIÓN

### First-Come, First-Served *(FIFO)*

- Primero en llegar, primero en ser servido.
- *No es expulsivo.*
- *Ventajas:*
	- Bastante **justo.**
	- Fácil de implementar y rápido de ejecutar: cola FIFO.
- *Inconvenientes:*
	- Puede provocar un **efecto convoy** (un proceso pesado puede bloquear muchos otros procesos).

![[esquema_FIFO.png|400]]

### Round Robbin *(RR)*

- **RR** consiste en realizar una asociación por turnos. Cada proceso tiene un tiempo límite de uso de la CPU, llamado *q.*
- *Es exclusivo.*

![[esquema_round_robbin.png|400]]

*Descripción detallada:*
- Los procesos cuyo estado es **listo** se organizan en una **cola FIFO.**
- Se elige el primero de la cola para ser ejecutado.
- Si un proceso *p* se está ejecutando y alcanza el quantum *q*, entonces se pasa el primero de la cola FIFO a la CPU, y se inserta *p* al final.
- Un temporizador (reloj), se encarga de activar el planificador cada cierto tiempo.

*Ventajas/Inconvenientes:*
- Los procesos reciben la *misma cantidad de CPU* 
- El comportamiento depende del quantum:
	- Si es muy grande, se reduce la interactividad.
	- Si es muy grande, provoca muchos cambios de contexto.
- Fácil de implementar.
- Fácil cómputo del tiempo de respuesta medio.
- Asume que todos los procesos son igualmente importantes.

### Linux Completely Fair Scheduler *(CFS)*

El objetivo de la política **CFS** es doble:
- Permitir que existan prioridades en la ejecución de los procesos.
- Garantizar un determinado **tiempo de respuesta** para todos los procesos: máximo intervalo de tiempo que cualquier proceso podrá estar sin ser ejecutado. 

_
- En **CFS,** cada proceso en el sistema tiene un *peso* en función de un valor **nice** que se le asigna.
- El valor **nice** va de -20 a 19 (el valor por defecto es 0, y a menos valor mayor *peso*).

Para determinar el tiempo que cada proceso utilizará la CPU, CFS utiliza el concepto de **latencia objetivo** del sistema:
> La **latencia objetivo** se define como el intervalo de tiempo en el que **DESEAMOS** que todos los procesos sean, parcialmente, ejecutados.

Para evitar la pérdida de prestaciones, debido al gran número de cambios de contexto, CFS utiliza una **granularidad mínima:** es un tiempo mínimo de ejecución de cada proceso cuando coge la CPU.

```c
int getpriority(int which, pid_t pid);
```
- Devuelve el valor de *nice* del proceso *pid.*
- El valor de *which* indica si nos referimos al pid del proceso, grupo o usuario efectivo (PRIO_PROCESS, PRIO_PGRP o PRIO_USER).

```c
int setpriority(int which, pid_t pid, int v);
```
- Asigna *v* como valor de *nice* del proceso *pid.*

#### Ejemplo: cambio de valor de *nice* de un proceso
nice.c
```c
#define _GNU_SOURCE
#include <unistd.h>
#include <stdio .h>
#include <sys/time .h>
#include <sys/resource .h>
#include <sched .h>

int main () {
	int valor ;
	
	valor = getpriority(PRIO_PROCESS, 0);
	printf("Prioridad del proceso %d: %d\n",getpid(), valor );
	
	setpriority(PRIO_PROCESS, 0, -4);
	valor = getpriority(PRIO_PROCESS, 0);
	printf("Nueva prioridad del proceso %d: %d\n" ,getpid(), valor);
}
```
*% ./nice*
Prioridad del proceso 3386: 0
Nueva prioridad del proceso 3386: -4

### Otros Planificadores de Propósito General

- **Brain Fuck Scheduler** (BFS)
- **Budget Fair Queuing** (BFQ)

### Planificadores en Tiempo Real

- **Rate Monotonic** (RM)

## COLAS MULTINIVEL

- Una **cola multinivel** está formada por un conjunto de varias colas, de manera que cada una de ellas esté gestionada por un planificador.
- Cada proceso es asignado a una cola.
- Cada cola tiene una *prioridad.*

![[esquema_colas_multinivel.png|400]]

En Linux se utiliza una cola multinivel (con cuatro niveles) sin realimentación, con algunas características propias:
- Todos los procesos tienen una **prioridad estática.**
- El planificador elige el proceso con *mayor* prioridad estática.

Tipos de prioridades estáticas:
- **FIFO y RR:** de 1 a 99.
- **CFS:** prioridad estática *fija* de 0, solo se ejecutan si no hay procesos FIFO o RR.
- **Batch:** los procesos de esta cola se ejecutan si no hay procesos en las otras colas listos para ser ejecutados.

### Obtención del Planificador
```c
int sched_getscheduler(pid_t pid);
```
- Devuelve la política de planificación del proceso *pid.*
- Si *pid = 0* devuelve la política de planificación del proceso que realiza la llamada.

### Selección del Planificador
```c
int sched_setscheduler(pid_t pid, int pilicy, const struct sched_param *sp);
```
- Selecciona la política de planificación *policy* del proceso *pid* con los parámetros especificado en *sp* (solo contiene la prioridad).

*Ejemplo planificación_2.c:*
```c
#define _GNU_SOURCE
#include <unistd.h>
#include <stdio .h>
#include <sys/time .h>
#include <sys/resource .h>
#include <sched .h>

int main () {
	int policy, ret, x;
	struct sched_param sp;
	
	sched_getparam(0, &sp); // Obtenemos la prioridad estática de 0
	printf("Pol´ıtica CFS. Prioridad est´atica : %d\n",sp.sched_priority);
	
	sp.sched_priority = 1;
	sched_setscheduler(0, SCHED_RR, &sp); // RR con prioridad 1
	sp.sched_priority = 11; // Aquí aún no hemos cambiado la prioridad a 11
	sched_setparam(0, &sp); // Ahora cambiamos la prioridad a 11
	policy = sched_getscheduler(0);
	switch(policy) {
	case SCHED_OTHER:
		printf("Pol´ıtica CFS. Prioridad est´atica : %d\n", sp.sched_priority);
		break ;
	case SCHED_RR:
		printf("Pol´ıtica RR. Prioridad est´atica : %d\n", sp.sched_priority);
		break ;
	case SCHED_FIFO:
		printf("Pol´ıtica FIFO . Prioridad est´atica : %d\n", sp.sched_priority);
	};
}
```

*% ./planificación_2*
Política CFS. Prioridad Estática: 0
Política RR. Prioridad estática: 11

## AFINIDAD

### Planificación con Multiprocesadores

- Ejecutar un proceso en distintas CPUs tiene un coste.
- Si un proceso está asignado a una CPU y es cambiado a otra, puede ocurrir que datos almacenados en la caché local se pierdan.

### Afinidad

**Afinidad del Proceso (Process Affinity):** característica de un proceso que hace que sea posible/preferible su ejecución en una determinada CPU.

Tipos de afinidad:
- **Fuerte:** se fuerza a un proceso a ejecutarse en la misma CPU.
- **Débil:** se intenta que el proceso esté en la misma CPU, pero puede ser replanificado a otra diferente:
	- Se mantiene una lista de procesos por cada CPU *(runqueue).*
	- Se intenta que la carga de las CPUs esté balanceada:
		- **Pull migration:** si la lista de procesos de una CPU está vacía se coge un proceso de otra lista.
		- **Push migration:** se hace una comprobación periódica de la carga del sistema, si no está *balanceada*, se mueven procesos entre CPUs para que lo esté.

### Afinidad en Linux

Linux utiliza por defecto una **afinidad débil** con **push migration,** regularmente se invoca a la función *load_balance().*

Mecanismo de balanceo de carga usado por Linux:
1. Por cada CPU se emplea una *runqueue* diferente.
2. Los procesos se mantienen en la misma *runqueue*, pero si hay más de un 25% de diferencia en el número de procesos entre dos *runqueue,* se transfieren algunos procesos para equilibrar la carga: **la carga es el número de procesos.**
3. Actúa cada 1 ms, si alguna *runqueue* se vacía, o 200 ms en general.

### Obtención de Afinidad

```c
int sched_getaffinity(pid_t pid, size_t len, cpu_set_t *set);
```

- Al conjunto *set* se le asigna la afinidad del proceso *pid.*
- *len* debe especificar el tamaño de *cpu_set_t* (sizeof(set)).

### Selección de Afinidad

```c
int sched_setaffinity(pid_t pid, size_t len, cpu_set_t *set);
```

- Al proceso *pid* se le asigna la afinidad especificada en *set.*
- *len* debe especificar el tamaño de *cpu_set_t* (sizeof(set)).
- Para trabajar con *set* se utilizan las siguientes macros:
```c
	CPU_ZERO(cpu_set_t *set); // inicializa el conjunto "set" vacío
	CPU_SET(int cpu, cpu_set_t *set); // añade "cpu" a "set"
	CPU_CLR(int cpu, cpu_set_t *set); // elimina "cpu" de "set"
```

### Ejemplo: Cambiar Afinidad de un Proceso
afinidad.c
```c
int main () {
	int i, cpus = GetCPUCount();
	cpu_set_t set;
	
	sched_getaffinity(0, sizeof(set), &set);
	printf ("CPUs afines al proceso %d:", getpid());
	for (i = 0; i < cpus; i++)
		if (CPU_ISSET (i ,&set )) printf (" %i",i);
		
	CPU_ZERO (&set);
	CPU_SET (1, &set); // Sólo añadimos la CPU #1
	sched_setaffinity(0, sizeof(set), &set);
	printf ("\nCPUs afines al proceso %d:", getpid());
	for (i = 0; i < cpus; i++)
		if (CPU_ISSET (i, &set)) printf(" %i",i);
	printf ("\n");
}
```

*% ./afinidad*
CPUs afines al proceso 2375: 0 1 2 3
CPUs afines al proceso 2375: 1

## INTERACCIÓN SOFTWARE-HARDWARE

### Buffer Overflow

buffer_overflow.c
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int check_authentication(char *password) {
	int auth_flag = 0;
	char password_buffer [16];
	strcpy(password_buffer, password);
	if(strcmp(password_buffer, "mazinger") == 0)
		auth_flag = 1;
	return auth_flag ;
}

int main(int argc, char *argv[]) {
	if(check_authentication(argv[1]))
		printf ("\nAccess Granted .\n");
	else printf ("\nAccess Denied .\n");
}
```

*% ./buffer overflow mazinger*
Access Granted.

*% ./buffer overflow perroflauta*
Access Denied.

*% ./buffer overflow aaaaaaaaaaaaaaaaaaaa*
Access Denied.

*% ./buffer overflow aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa*
Segmentation fault (core dumped)

*% ./buffer overflow aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa*
Access Granted.

___
# TEMA 5 : VIRTUALIZACIÓN
___

## ¿QUÉ ES LA VIRTUALIZACIÓN?

La **virtualización** es el conjunto de técnicas que proporcionan un nivel de abstracción adicional entre la máquina y las aplicaciones que se ejecutan sobre la misma.

Objetivos:
- Conseguir que múltiples recursos físicos parezcan un solo recurso lógico.
- Conseguir que un solo recurso físico parezca múltiples recursos lógicos.

## ¿QUÉ ES UNA MÁQUINA VIRTUAL?

LLamamos **máquina virtual** a la implementación de una máquina que ejecuta programas o sistemas como si fuese una máquina real.

## VENTAJAS E INCONVENIENTES DE LA VIRTUALIZACIÓN

- **Ventajas:**
	- Flexibilidad
	- Portabilidad
	- Aislamiento/Seguridad
	- Utilización del hardware
- **Inconvenientes:**
	- Complejidad
	- Prestaciones

## TIPOS DE MÁQUINAS VIRTUALES

1. **Máquinas virtuales de proceso:** se ejecutan como aplicaciones normales sobre un sistema operativo, y su objetivo es abstraer los detalles del hardware subyacente.
2. **Máquinas virtuales del sistema:** permiten la compartición del hardware subyacente entre sistemas operativos diferentes.

### Máquinas Virtuales de *Proceso*

Entorno en que un programa es independiente de la máquina subyacente.

- El entorno virtual se crea cuando el programa es ejecutado, y termina cuando éste acaba.
- Permite que un programa se ejecute siempre de la misma forma, independientemente de la plataforma en la que se esté ejecutando.
- La máquina virtual de proceso se implementa como si fuese un intérprete: el programa que se ejecutará sobre la máquina virtual de proceso no se compila sino que se interpreta.

### Máquinas Virtuales del *Sistema*

Plataforma que permite la ejecución de múltiples sistemas operativos.

- Permite la compartición de hardware subyacente entre distintos sistemas operativos.
- Cada sistema operativo permanece aislado de los otros sistemas operativos.

### El *Hipervisor*

El **hipervisor** (Virtual Machine Monitor (VMM)) es el programa encargado de la virtualización. Presenta un conjunto de dispositivos virtuales a cada sistema operativo, y se encarga de arbitrar el acceso de los distintos sistemas a los recursos compartidos reales.

Hay dos tipos básicos de hipervisores:
1. **Hipervisores nativos.**
	- El VMM se ejecuta directamente sobre el hardware.
![[hipervisor_nativo.png|250]]
1. **Hipervisores con anfitrión.**
	- El VMM se ejecuta sobre un sistema operativo anfitrión.
![[hipervisor_con_anfitrion.png|250]]

### Dispositivo Virtual

Un **dispositivo virtual (virtual appliance)** es un conjunto de componentes empaquetados para ser ejecutados sobre un hipervisor.

![[dispositivo_virtual.png|400]]

### Virtual Box

Hipervisor con *anfitrión.*

### Rosetta

Los ordenadores Mac utilizaron **Rosetta** durante un tiempo para realizar la transición de procesadores PowerPC a Intel.

## CONTAINERS

Los **containers** proporcionan a cada aplicación un entorno aislado en el que ejecutarse:

![[container.png|400]]

Loa containers ofrecen un entorno similar al que se puede obtener utilizando una máquina virtual por cada aplicación, pero sin la carga asociada a ejecutar un sistema operativo por cada una de ellas (solo se ejecutan las partes que hacen falta).

Containers en casos reales:
- *Google search*
- *Electronic Arts* (servidores de juegos)
- *Pokemon Go* (cada personaje usa un container)

___
# TEMA 6 : THREADS
___

## CONCEPTOS GENERALES

- Un **thread** consiste en una **unidad de ejecución** de un código **ya cargado en memoria.**
- Se pueden lanzar varios threads *al mismo tiempo.*
- Los **thread** se diferencian de los *fork()* en que no producen una clonación completa del proceso. Cada instancia se ejecuta de forma autónoma.

**Proceso:** cada niño lee su propio libro, que es el mismo, aunque puede que en capítulos diferentes.

![[niños_1.png|300]]

**Thread:** todos leen el mismo libro al mismo tiempo, aunque puede que en capítulos distintos.

![[niños_2.png|300]]

## IMAGEN VIRTUAL DE UN THREAD

Los *thread* no comparten:
- ID del thread.
- **Puntero de instrucciones.**
- Máscara de señales y registros propios.
- Información de planificación.
- **Stack y puntero de acceso al mismo.**

La visión que cada thread tiene de sí mismo es la de una unidad de ejecución completamente independiente a la de los demás threads.

> Cada thread realmente actúa como si dicho código, memoria, etc., fuese únicamente suyo.

## THREADS VS PROCESOS

- El **código** que ejecutará cada thread se incluye en una **función asociada:** no es necesario utilizar *fork().*
- La **creación de threads** es menos costosa.
- El **cambio de contexto entre threads** es mucho más rápido.
- La **comunicación entre threads** es más sencilla: podemos utilizar *variables compartidas* a las que todos los threads puedan acceder.

## THREADS DEL KERNEL VS THREADS DEL USUARIO

**Kernel Level Threads:**
- Son unidades de procesamiento soportadas directamente por el SO.
- El SO se encarga de su creación, planificación y sincronización.

**User Level Threads:**
- La aplicación se encarga de su creación, organización y planificación.
- *Flexibles.*
- El kernel *no es consciente* de la existencia de threads.

## PROCESOS/THREADS/TASKS EN LINUX

**En UNIX:**  Cada *PCB* contiene uno o más **TCBs** (**T**hread **C**ontrol **B**lock), que contienen:
- Thread ID.
- Valores de registros propios.
- Información propia de cada Thread: máscara de señales e información de planificación.

**En Linux** no se distingue entre procesos y threads todo son tareas **(tasks).** 

Tanto la función **fork()** como **pthread_create()** llaman a la función **clone().**

Al crear un *thread* en Linux se crea una nueva tarea y:
- Se especifica la función que ejecutará el thread.
- Se especifica cuál es el stack del thread.
- Se especifica lo que se comparte.

Cada thread creado a partir del mismo proceso tiene una imagen virtual de memoria propia y distinta, que se mapea a direcciones de memoria física.

En Linux todas las tareas se tratan igual, aunque antes de realizar un cambio de contexto se comprueba si éste debe ser completo o sólo parcial.

> Para obtener el TID (Task ID) de una tarea usa **gettid().**

## SINTAXIS DE *pthread_create()* y *pthread_exit()*

```c
int pthread_create(pthread_t hilo, NULL, void *(*func)(void *), (void *) arg);
```

> Crea el thread **hilo** que ejecutará la función **func().**

```c
int pthread_exit(0);
```

> Finaliza la ejecución del thread que invoca la función.

## SINTAXIS DE *pthread_self()* y *pthread_join()*

```c
pthread_t pthread_self(void);
```

> Devuelve el identificador del thread que ejecuta la llamada.

```c
int pthread_join(pthread_t hilo, NULL);
```

> Suspende la ejecución del thread hasta que termine el thread **hilo.**

## *exit()* VS *pthread_exit()*

Al usar **exit():**
- La ejecución de las funciones hijo que éste ha creado no se ven afectadas.
- Por el contrario, todos los threads que éste ha creado también finalizarán (es importante finalizar los threads antes del proceso principal).

## EJEMPLO CREACIÓN DE THREADS

thread1.c
```c
#include <stdio.h>
#include <pthread .h>
#define MAX_THREADS 10

void *func() {
	printf ("Thread %u\n", pthread_self());
	/* Realmente , pthread_self() no es de tipo %u */
	pthread_exit(0);
}

int main() {
	int i;
	pthread_t hilo[MAX_THREADS];
	for (i = 0; i < MAX_THREADS; i ++)
		pthread_create(&hilo[i], NULL, func, NULL);
		
	for (i = 0; i < MAX_THREADS; i ++)
		pthread_join(hilo[i], NULL );
	exit (0); /* Finaliza todos los threads , si quedase alguno */
}
```

Para compilar código con threads es necesario enlazar con la librería de pthreads:
```shell
gcc thread1.c -o thread1 -Ipthread
```

*% ./thread1*
Thread 55803904
Thread 56340480
Thread 56877056
Thread 57413632
Thread 57950208
Thread 58486784
Thread 59023360
Thread 59559936
Thread 60096512
Thread 60633088

## PLANIFICACIÓN DE THREADS

¿Qué identificadores usan los thread?
- **PID** --> getpid()
- **ID** del thread --> pthread_self()
- **TID** --> gettid()

## UTILIZACIÓN DE THREADS

*Objetivo:* pasar un argumento a la función *func()*, que contendrá el código de un thread *hilo.*

1. Supongamos que el argumento es de tipo entero.
```c
int argumento;
pthread_create(&hilo, NULL, func, (void * ) &argumento);
```
> Se le pasa un puntero sin tipo a la dirección **argumento.**

2. El formato de la función **func()** que recibirá dicho argumento es del tipo:
```c
*func((void * ) arg)
```
> **(void \*) arg** es un puntero sin tipo que a punta a la dirección de **&argumento.**

Por lo tanto en la función **func()** habrá que hacer una conversión de tipos, ya que no trabajaremos con un puntero a una dirección, sino con una variable de tipo entero.
```c
int parametro;
parametro = *((int * ) arg)
```

## EJEMPLO PASO DE ARGUMENTOS A THREADS

arg_bien.c
```c
#include <stdio .h>
#include <pthread .h>
#define MAX_THREADS 6
void *func (void * arg) {
	int parametro;
	parametro = *((int * ) arg );
	printf("Thread %u lee %d\n", pthread_self(), parametro);
	pthread_exit(0);
}
int main() {
	int i, v[MAX_THREADS];
	pthread_t hilo[MAX_THREADS];
	for (i = 0; i < MAX_THREADS; i++) v[i] = i;
	for (i = 0; i < MAX_THREADS; i++)
		pthread_create(&hilo[i], NULL, func, (void * ) &v[i]);
	for (i = 0; i < MAX_THREADS; i++)
		pthread_join (hilo [i], NULL);
	exit (0);
}
```

*% ./arg_bien*
Thread 67641344 lee 1
Thread 67104768 lee 0
Thread 68177920 lee 2
Thread 68714496 lee 3
Thread 69251072 lee 4
Thread 69787648 lee 5

___
# TEMA 7 : SINCRONIZACIÓN
___

## CONDICIONES DE CARRERA (RACE CONDITIONS)

**Condición de Carrera:** es un *bug* que se produce cuando tareas concurrentes acceden a un determinado recurso compartido al mismo tiempo, resultando impredecible el resultado final debido a como se han realizado dichos accesos.

El resultado debido a una condición de carrera puede depender de:
- El orden de intercalación de operaciones.
- El funcionamiento de las memorias caché.
- Los datos en las cachés.
- La forma en que se produce la compilación.

## SINCRONIZACIÓN

- **Sección crítica:** región de un programa dónde pueden existir condiciones de carrera.
- **Exclusión mutua:** consiste en permitir acceso a una sección crítica a una sola tarea simultáneamente. *Requisitos:*
	- - *Progreso (liveness/progress):* una tarea fuera de la sección crítica no puede impedir el acceso a otra.
	- *Espera acotada (no starvation):* denegación permanente del acceso a la sección crítica.
	- *Libre de interbloqueos (no deadlocks):* varias tareas se bloquean mutuamente de forma permanente.

## CERROJOS

> Un **cerrojo** es un *mecanismo* que permite que varias tareas compartan un recurso, accediendo al mismo de manera atómica.

Funcionamiento:
1. Cerrar el **cerrojo** antes de acceder a una sección crítica, y liberarlo después.
2. Esperar, si no se puede cerrar el **cerrojo.**

## IMPLEMENTACIÓN DE CERROJOS

### Cerrojos Creados por Software

Se utiliza una variable compartida que actúa como cerrojo:
```c
while(locked);
locked = 1;
/* do critical section */
locked = 0;
```
- *Ventaja:* fácil de usar.
- *Desventaja:* contiene un bug.

### Desactivación de Interrupciones

Se deshabilitan las interrupciones del sistema antes de entrar en la sección crítica y se habilitan antes de salir.

*Ventajas:*
- Simple.
- Fácil de implementar.

*Desventajas:*
- Se le da a la tarea un gran control del sistema.
- Complicada en sistemas multiprocesadores.

### Soporte Hardware

Se utilizan instrucciones proporcionadas por la CPU, que garantiza que se ejecutarán de manera óptima. Por ejemplo:

- **Test-and-set** coge el cerrojo, pero sólo en el caso en que nadie lo haya cogido antes.
```c
int test_and_set(int *x){
	last_value = *x;
	*x = 1;
	return last_value;
}

/* it's used as follows: */
while(test_and_set(&lock));
/*  do critical section  */
lock = 0;
```
- **Compare-and-swap**
- **Fetch-and-increment**

**Problemas** uso instrucciones proporcionadas por la CPU:
- Hay que incluir la implementación de los cerrojos.
- Portabilidad.

## CERROJOS EN POSIX

> El paquete **Pthreads** proporciona el tipo de datos *pthread_mutex_t* para representar cerrojos.

Operaciones sobre el conjunto **mutex:**
```c
// inicializar cerrojo
int pthread_mutex_int(pthread_mutex_t *mutex, NULL);

// destruir cerrojo
int pthread_mutex_destroy(pthread_mutex_t *mutex);

// cerrar cerrojo
int pthread_mutex_lock(pthread_mutex_t *mutex);

// abrir cerrojo
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

## SPINLOCKS

La implementación de cerrojos está basada en **spinlocks:** de forma repetitiva, se comprueba si un cerrojo está disponible. 

> Las soluciones basadas en *spinlocks* requieren espera activa, con lo cual se desperdician ciclos de CPU.

