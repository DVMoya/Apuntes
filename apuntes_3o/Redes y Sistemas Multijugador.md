___
# ÍNDICE
___

- [[#BLOQUE 1 - REDES]]
	- [[#TEMA 1 INTRODUCCIÓN A LAS REDES DE COMPUTADOR]]
		- [[#- 1 - Definición de red de comunicación de datos]]
		- [[#- 2 - VISIÓN GENERAL DE INTERNET]]
		- [[#- 3 - Modelo de Comunicación]]
		- [[#- 4 - Arquitectura de Red]]
		- [[#- 5 - Resumen]]
	- [[#TEMA 2 EL NUVEL DE RED]]
- [[#BLOQUE 2 - SISTEMAS MULTIJUGADOR]]
	- [[#TEMA 5 LA CAPA DE APLICACIÓN]]
	- [[#TEMA 6 LA CAPA DE TRANSPORTE]]
	- [[#TEMA 7 SISTEMAS DISTRIBUIDOS - CONCURRENCIA - DESARROLLO DE APLICACIONES EN RED]]
- [[#BLOQUE 3 - REDES]]
	- [[#TEMA 3 EL NIVEL DE ENLACE EN DATOS]]
	- [[#TEMA 4 SEGURIDAD ACLs]]

___
# BLOQUE 1 - REDES
___

___
# TEMA 1 : INTRODUCCIÓN A LAS REDES DE COMPUTADOR
___

## - 1 - Definición de red de comunicación de datos

### Definición de Red
Una red es una colección interconectada de computadoras autónomas.

### Son redes **(Requisitos)**

- 2 PCs
	- Conexión directa *TCP/IP*
	- ¡Deben estar identificados en la misma red!
	- Necesitan *direcciones IP* y *máscara de red*/subred
- 2 PCs o más
	- Conexión mediante dispositivos: *HUB, SWITCH*
	- Se deben controlar las *colisiones de paquetes.*
	- Necesarias *direcciones IP* y *máscara de red*/subred, direcciones *MAC* y dirección *broadcast.*

### Características de una Red

*ELEMENTOS:*

==NODO== ---> Una máquina conectada a la red
==HOST== ----> Un nodo que actúa como PC

*IDENTIFICACIÓN DE DISPOSITIVOS*

- Cada nodo debe estar identificado en la red. 
- **Dirección:** Secuencia de Bytes única que lo identifica.
	- Dirección *física* (Ethernet o Hardware)
		- **MAC** (Media Access Control) --> Asignada por el fabricante.
	- Dirección *lógica* (de internet o IP)
		- Asignada por el host o administrador de red
		- Se le puede asignar un nombre. El nombre se traduce a IP por DNS.

*CONEXIONES*

- Enlaces de comunicación: **(medios físicos de conexión a host)**
	- tasa de transmisión de datos = *ancho de banda*
- Conexión de un host a un enlace
	- Uso de *HUB* (enlace con colisiones) y *SWITCH* (enlace sin colisiones)
- Conexión entre redes diferentes
	- Uso de *Routers* (dispositivo de reenvío de paquetes, conecta por LAN o WAN)

*REGLAS DE COMUNICACIÓN*
- *Protocolos:* Reglas que definen la comunicación entre host. Reenvío y recepción de datos.
- Definen el formato de direcciones, empaquetado de datos... 
- Protocolos: tcp, ip, http, ftp, ppp...
- Un protocolo concreto define un aspecto concreto de la comunicación.

## - 2 - VISIÓN GENERAL DE INTERNET

### Estructura de Internet

**Extremos de la red**
- **Host** ejecutan programas de aplicación: web, correo...
- **Modelo cliente servidor** solicitud de un *host cliente* de un servicio de recepción a un *host servidor*: web, correo, juegos en red...

**Núcleo de la red**
- **Maya de Routers** interconectados.
- **Transmisión** por comunicación de circuitos (red telefónica) o computación de paquetes (envío de grupos de datos)
- **División** de frecuencia o de tiempo.

**Redes de acceso, medios físicos**
- Modem telefónicos, ADSL (línea de subscripción digital asimétrica).

## - 3 - Modelo de Comunicación

![[modelo_comunicacion.png|500]]

(veremos este proceso en profundidad más adelante)

## - 4 - Arquitectura de Red

**¿Cómo se diseña una red teniendo en cuenta la anterior?**
⭣
Organiza las tareas de la red por capas.
⭣
Cada capa realiza una serie de tareas
⭣
Se usan *entidades* (elementos activos de una capa), *interfaces* (operaciones y servicios que una capa ofrece a la superior) y *protocolos* (reglas que rigen comunicaciones entre entidades).
⭣
**Dos arquitecturas de red: OSI y TCP/IP.**

### Arquitectura TCP/IP

Cada capa toma los datos de la anterior y añade información de **cabecera** de la nueva capa para crear una nueva unidad de datos **PDU.**

![[arquitectura_tcp_ip.png|500]]

- **Capa física**
- **Capa de enlace de datos**
- **Capa de red**
- **Capa de transporte**
- **Capa de aplicación**

## - 5 - Resumen

- Para estudiar una red de computadora es fundamental la identificación
de los sistemas terminales, tanto de forma física, en la capa de enlace,
como de forma lógica, en la capa de red. DIRECCIONAMIENTO.
- También el necesario saber de que manera los datos van desde el origen
al destino atravesando diversas redes. ENRUTAMIENTO.
- En relación con lo anterior es conveniente conocer algunos protocolos
de control de Internet.
- En los siguiente capítulos estudiaremos aspectos de cada una de las
capas que constituyen la arquitectura TCP/IP.
- Comenzaremos por estudiar en el próximo capítulo el nivel de red en
Internet (capa de red, capa de internet).

___
# TEMA 2 : EL NUVEL DE RED
___

___
# BLOQUE 2 - SISTEMAS MULTIJUGADOR
___

___
# TEMA 5 : LA CAPA DE APLICACIÓN
___

## - 1 - Introducción

## - 2 - Principios de las Aplicaciones en Red

El desarrollo de una aplicación en red implica escribir programas que se ejecutan en distintos **sistemas terminales** y que **se comuniquen entre sí** a través de la **red.**

Tipos de arquitectura para desarrollar aplicaciones en red:
- La arquitectura *cliente-servidor.*
- La arquitectura *P2P.*

### Arquitectura *Cliente-Servidor*

- Siempre hay un host activo denominado **servidor** que da servicio a las solicitudes de otros host, los **clientes.**
- El servidor tiene una dirección fija conocida, su IP.
- Se puede utilizar como servidor una agrupación de hosts, **cluster,** que se denomina centro de datos, creando un *servidor virtual* de gran capacidad.

### Arquitectura *P2P*

- Comunicación directa entre parejas de hosts de forma intermitente, conocidos como **peers.**
- Los pares son computadoras de usuario cualesquiera.
- Los pares se comunican entre sí sin pasar por un servidor dedicado, por eso la arquitectura se llama *peer-to-peer (P2P).*
- Principal característica *auto-escalabilidad.*
- Buena relación coste-prestaciones.
- **Problemas:** los usuarios tienen ancho de banda asimétrico, la seguridad y que los usuarios deben prestar gratuitamente recursos de ancho de banda.

## - 3 - Proceso de Comunicación

> Una aplicación en red consta de parejas de procesos que intercambian mensajes. Se etiqueta un proceso como **cliente** y al otro como **servidor.**

- Los procesos se comunican entre sí usando la capa de aplicación.
- Los procesos envían mensajes a la red y los recibe de la red a través de una *interfaz* software denominada **socket** (*API*, Application Software Interface).

## - 4 - Servicios de Transporte

Al desarrollar una aplicación hay que elegir el protocolo de transporte a usar (los servicios se clasifican según cuatro parámetros):

1. **Transferencia de datos fiable.**
	- Hay aplicaciones en las que es importante no perder paquetes, se desea *"ENTREGA DE DATOS GARANTIZADA"* proceso a proceso.
	- En otras se pueden permitir pérdidas *"TOLERANTES A PÉRDIDAS."*
2. **Tasa de transferencia.**
	- Hay aplicaciones que requieren garantía de un cierto ancho de banda o tasa de transferencia mínima (bits/s) y otras no.
3. **Temporización.**
	- Hay aplicaciones que requieren de un tiempo mínimo para transferencia de 1 bit. 
4. **Seguridad.**
	- en ciertas aplicaciones interesa la confidencialidad (cifrado de datos), la garantía de integridad de datos, mecanismos de autentificación, etc.

Las redes TCP/IP ponen a disposición de las aplicaciones dos protocolos de transporte: **TCP y UDP**.

### Servicio de Transporte **TCP**

*ORIENTADO A CONEXIÓN*

- Antes de que los procesos comiencen a comunicarse se inicia una fase de negociación, reconocimiento, y establecimiento de conexión TCP entre los socket de los dos procesos (full-dúplex). Cliente y servidor se preparan para el intercambio de paquetes. Tras el intercambio se desactiva la conexión.

*TRANSFERENCIA DE DATOS FIABLE*

- Se envían datos sin errores, ordenados y sin duplicidad.
- Existen mecanismos de control de congestión que regulan la velocidad de transmisión (ancho de banda) → *Esto puede no ser bueno para aplicaciones en tiempo real que pueden preferir UDP*

### Servicio de Transporte **UDP**

*NO ORIENTADO A CONEXIÓN*

- Si un proceso envía un mensaje a un socket UDP, el protocolo no garantiza que llegue el mensaje, ni que esté ordenado.

*TRANSFERENCIA DE DATOS NO FIABLE*

- No existen mecanismos de control de congestión por lo que no hay límite en las velocidades del emisor.
- **PROBLEMAS:** muchos cortafuegos bloquean las aplicaciones con tráfico UDP *por lo que algunos diseñadores de aplicaciones multimedia en tiempo real pueden preferir TCP.*

## - 5 - Direccionamiento Entre Procesos

- Los procesos se comunican usando los servicios de la capa de transporte.
- El proceso se identifica usando dos elementos:
	- Un host se identifica por Nombre o Dirección IP
	- Un proceso que se ejecute en un host se identifica por un número de puerto.
- Las aplicaciones populares populares tienen asignados números de puertos fijos (hasta 1024) llamados *"puertos bien conocidos" (well-known ports).*

___
# TEMA 6 : LA CAPA DE TRANSPORTE
___

___
# TEMA 7 : SISTEMAS DISTRIBUIDOS - CONCURRENCIA - DESARROLLO DE APLICACIONES EN RED
___

___
# BLOQUE 3 - REDES
___

___
# TEMA 3 : EL NIVEL DE ENLACE EN DATOS
___

___
# TEMA 4 : SEGURIDAD ACLs
___

___