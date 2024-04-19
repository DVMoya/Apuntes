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