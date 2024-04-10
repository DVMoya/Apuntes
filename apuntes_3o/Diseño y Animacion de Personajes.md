___
# ÍNDICE

- [[#TEMA 1 INTERPOLACION]]
	- [[#REPRESENTACIÓN DE CURVAS]]
		- [[#Tipos de Continuidad Geométrica]]
		- [[#Tipos de Continuidad Paramétrica]]
		- [[#Implicaciones]]
			- [[#¿Control local o global?]]
			- [[#¿Interpola o aproxima?]]
	- [[#CURVAS DE BÉZIER]]
		- [[#Representación matricial Bézier]]
		- [[#Dividir una curva de Bézier]]
		- [[#Ejercicios Bézier]]
	- [[#REPRESENTACIÓN DE LA ORIENTACIÓN]]
		- [[#Representación Matricial]]
		- [[#Representación Fixed-Angle]]
		- [[#Representación con Ángulos de Euler]]
		- [[#Representación Ángulo y Eje]]
		- [[#Cuaterniones]]
	- [[#MOVIMIENTO A LO LARGO DE UNA TRAYECTORIA CURVA]]
		- [[#Ejercicios trayectoria]]
		- [[#Método adaptativo]]
	- [[#CONTROL DE VELOCIDAD]]
		- [[#Polinomio Cúbico]]
		- [[#Función Aceleración-Tiempo]]
	- [[#INTERPOLACIÓN DE LA ORIENTACIÓN]]
	- [[#RUTAS]]
- [[#TEMA 2]]
___
# TEMA 1 : INTERPOLACION

## REPRESENTACIÓN DE CURVAS
La forma de representación de curvas que más nos interesa en la animación es la **representación paramétrica**, o sea representar una curva mediante una función.

![[representacion_parametrica.png|500]]

Para poder representar trayectorias más complejas se ha de usar polinomios:

![[representacion_polinomica.png|500]]

Para reducir el coste computacional podemos dividir la curva en segmentos con su correspondiente fórmula. Lamentablemente al dividir la curva en segmentos aparece un nuevo problema, la continuidad. Los segmento empiezan y terminan en un punto, esto significa que los segmentos no están conectados entre sí.

![[curva_segmentada.png|500]]![[no_hay_continuidad.png|200]]

### Tipos de *Continuidad Geométrica*:
- G0: Cuando el punto de unión o nudo es el último de un segmento de curva y también el primero del siguiente segmento.
![[continuidad_g0.png|200]]
- G1: Cuando el vector tangente ($t_1$) al primer segmento de curva del nudo coincide en dirección con el vector tangente ($t_2$) al siguiente segmento de curva en dicho nudo.
![[continuidad_g1.png|200]]

### Tipos de *Continuidad Paramétrica*:
- C0: Cuando se cumple la misma condición que en *G0*. *C0 y G0 son lo mismo.*
- C1: Cuando, además de cumplirse la condición preestablecida en *G1*, las tangentes son idénticas también en magnitud. (coinciden derivadas/pendientes en nudo)
![[continuidad_c1.png|200]]
- C2: Cuando en el nudo coinciden, además de las primeras derivadas, también lo hagan las respectivas segundas derivadas. Es decir, ambas curvas tienen la misma pendiente y la misma curvatura en el nudo. ej. comparación tipo *C1* y *C2*.
![[comparacion_c1_c2.png|300]]
- Cn: Cuando las *n* primeras derivadas coinciden.

### Implicaciones
- Si la continuidad de la curva es solo de tipo *C0 o G0*, cuando un objeto que recorre la trayectoria de la curva pase de un segmento al siguiente, habrá un cambio repentino en la dirección del movimiento del objeto.
- Cuando la continuidad de la curva sea de tipo *G1*, el objeto continúa en la misma dirección pero con un cambio de velocidad instantáneo, es decir, al pasar de un segmento al siguiente se produce un salto repentino en su velocidad.
- Si la continuidad de la curva es de tipo *C1*, no hay cambio de velocidad instantáneo pero sí de aceleración.
- Cuando la continuidad de la curva es de tipo *C2*, no hay cambio instantáneo ni de velocidad ni de aceleración.

#### ¿Control local o global?
Una curva tiene control local cuando al modificar un punto de la curva no se modifica toda la curva, sino solo una parte de ella. Y tiene control global justo cuando ocurre lo contrario, cuando al modificar un punto se produce una curva totalmente nueva.

#### ¿Interpola o aproxima?
Una curva interpola los puntos cuando la curva pasa por dichos puntos, y los aproxima cuando se acerca pero no pasa por ellos.
![[interpolacionVSaproximacion.png|500]]

## CURVAS DE BÉZIER
La curvas de Bézier no cumplen la condición de *C2*, pero sí cumplen las anteriores tres. 

Una curva de Bézier se define mediante cuatro puntos, dos de ellos son puntos finales, *P1* y *P4*, y los otros dos son puntos de control, *P2* y *P3*. Los puntos finales establecen de donde sale la curva, *P1*, y a dónde llega, *P4*. Mientras los puntos *P2* y *P3* son los responsables de su forma. La curva pasa por los puntos finales pero no por los puntos de control.
![[ejemplo_curvas_de_bezier.png|300]]

### Representación matricial Bézier

Representación matricial de una curva de Bézier:
$$
	f(u) = u · M_B · G_B
$$
Donde $u$ es el vector fila:
$$
	u = \begin{bmatrix} u^3 & u^2 & u & 1 \end{bmatrix},
$$
La matriz base, **$M_b$**, es siempre la misma para una curva de Bézier y ésta es.:
$$
M_b =\begin{bmatrix}
		-1 &  3 & -3 & 1 \\
		 3 & -6 &  3 & 0 \\
		-3 &  3 &  0 & 0 \\
		 1 &  0 &  0 & 0
	\end{bmatrix}
$$
El vector de geometría, **$G_b$**, es un vector columna que contiene los datos de una curva, sus cuatro puntos:
$$
G_b =\begin{bmatrix}
		P1 \\
		P2 \\
		P3 \\
		P4
	\end{bmatrix}
$$

Si desarrollamos el producto y analizamos detenidamente el polinomio obtenido, vemos que , para cualquier valor de **$u$**, un punto de la curva  no es más que una media ponderada de los puntos **$P1,\ P2,\ P3\ y\ P4$**.
$$	
	f(u) = B_0 · P1 + B_1 · P2 + B_2 · P3 + B_3 · P4
$$
A estos cuatro polinomios (**$B_0,\ B_1,\ B2,\ y\ B_3$**), se les conoce por el nombre de *polinomios de Bernstein*.
- La suma de los cuatro polinomios para cualquier valor de **$u$** siempre es **$1$**.
- Y gracias a esto, resolviendo tres de ellos es suficiente porque el cuarto lo obtendremos restando a uno la suma de los otros tres.

### Dividir una curva de Bézier
Algo útil que podemos tener en cuenta es que una curva de Bézier siempre está contenida por su envolvente convexa (*Convex Hull*).
![[convex_hull.png|300]]

Además de esto, una ventaja que tiene con respecto de otras curvas es la posibilidad de dividir una curva de Bézier en dos curvas de Bézier más pequeñas:
![[dividir_curva_bezier_paso1.png|300]]![[dividir_curva_bezier_paso2.png|300]]![[dividir_curva_bezier_paso3.png|300]] 

Este algoritmo se puede seguir aplicando indefinidamente. la idea es dejar de dividir la curva cuando las curvas obtenidas *sean virtualmente planas*. Repetir este proceso sin cabeza acaba dividiendo la curva en curvas más pequeñas de forma irregular (*algoritmo incremental*). Sin embargo existe una variación de este proceso que lo tiene en cuenta para conseguir un resultado uniforme (*algoritmo adaptativo*).
![[algoritmo_division_esquema.png|350]]

[Demo del algoritmo de división](http://cphoto.uji.es/vj1226/bezier/)

### Ejercicios Bézier
![[ejercicio_bezier1.png|500]]
![[ejercicio_bezier2.png|500]]

## REPRESENTACIÓN DE LA ORIENTACIÓN

### Representación *Matricial*
Mediante una matriz 4x4 puedes representar no solo la orientación sino también la posición de un objeto. *En la submatriz formada por las tres primeras filas y columnas se representa la orientación*, mientras que en la cuarta columna (tres primeras filas) se encuentra la posición. Al interpolar dos matrices del mismo objeto de distintos instantes de tiempo se produce un cambio de tamaño e incluso deformación.
![[interpolacion_representacion_matricial.png|500]]

[Demo de interpolación](http://cphoto.uji.es/vj1226/InterpolationMatrix/orienta.html)

### Representación *Fixed-Angle*
Este método emplea rotaciones alrededor del eje de coordenadas para expresar una orientación. La terna de valores *$(x,\ y,\ z)$* representa cuánto se ha de rotar el objeto en cada eje. Interpolar en este sistema de representación no siempre da el resultado esperado.

[Demo interpolación Fixed-Angle](http://cphoto.uji.es/vj1226/InterpolationFixedAngle/orienta.html)

### Representación con *Ángulos de Euler*
Al igual que la representación Fixed-Angle la de Ángulos de Euler también emplea una terna de ángulos, la diferencia siendo que los giros se realizan alrededor de un *sistema de coordenadas local*. 
![[representacion_euler.png|400]]

$$
	M_R = R_x(\alpha) · R_y(\beta) · R_z(\gamma)
$$

### Representación *Ángulo y Eje*
la orientación se expresa como un conjunto de dos valores; un valor *Eje* representado como vector, y un *ángulo de giro* alrededor de dicho eje.
![[angulo_y_eje.png|200]] 

Los valores intermedios los calculamos interpolando los ángulos inicial $\theta1$ y final $\theta2$ así:
$$
	 \theta i = (1 - i) · \theta 1 + i · \theta 2
$$
Respecto a los ejes, *Euler propone obtener un tercer vector, $B$,* a partir del producto vectorial de *$A1$* y *$A2$*, produciendo un Eje perpendicular a los otros dos.
![[tercer_vector_euler.png|200]]

Este nuevo eje *$B$* es el que hay que utilizar para convertir *$A1$* en *$A2$* (girando un total de *$\phi$* grados alrededor de *$B$*) produciendo de esta manera los sucesivos vectores, *$Ai$*, correctos:
$$
	Ai = R_b(\phi · i) · A1
$$
El resultado de la interpolación es el correcto, ya que *los vectores intermedios no son el resultado de la interpolación* entre *$A1$* y *$A2$*, sino el resultado de interpolar un giro alrededor del nuevo eje *$B$*. **Esto no es exactamente lo que buscamos**.

### *Cuaterniones*\*
La representación de una orientación mediante un cuaternión es equivalente a la representación mediante *Ángulo y Eje* solo que la información está dispuesta de manera matemática conveniente. Un cuaternión está formado por cuatro valores donde el primero es un valor escalar, *$s$*, y los otros tres forman un vector *$(x,\ y,\ z)$*, siendo el cuaternión: **$\begin{bmatrix} s, & x, & y, & z\end{bmatrix}$**

*\*Las operaciones con cuaterniones no nos conciernen en esta signatura.*

**la representación de dos orientaciones representadas mediante sendos cuaterniones no es más que la interpolación componente a componente de cada uno de los cuaterniones**. El resultado de esta interpolación nos proporciona la salida que visualmente consideramos correcta.

[Demo interpolación con cuaterniones](http://cphoto.uji.es/vj1226/InterpolationQuaternions/quat.html)

## MOVIMIENTO A LO LARGO DE UNA TRAYECTORIA CURVA

[Demo trayectoria a lo largo de una curva](http://cphoto.uji.es/vj1226/bezierAnimation/)

**Realiza un incremento constante del parámetro $u$ *NO* tiene por qué producir un incremento constante en el espacio recorrido y, en consecuencia, la velocidad que se obtiene *NO* es ni mucho menos constante.**

Si se desea velocidad constante es necesario que cada incremento de tiempo se corresponda con el mismo de espacio. Para ello se realiza el siguiente cálculo (*suponiendo velocidad constante $v_0$*): *$e = v_0 · t$*.

Es necesario establecer la relación entre el espacio recorrido, *$e$*, y el parámetro *$u$* para así poder obtener uno a partir de el otro. Esta relación es conocida como **Parametrización de la distancia**.
![[parametrizacion_de_la_distancia.png|300]]

### Ejercicios trayectoria
![[ejercicios_trayectoria1.png|500]]![[ejercicios_trayectoria2.png|500]]![[ejercicios_trayectoria3.png|500]]![[ejercicios_trayectoria4.png|500]]![[ejercicios_trayectoria5.png|500]]![[ejercicios_trayectoria6.png|500]]![[ejercicios_trayectoria7.png|500]]

### *Método adaptativo*
Para corregir el error sin tener que extender la tabla hasta el infinito se puede emplear un **método adaptativo.** En el proceso de construcción de la tabla mediante un proceso adaptativo podemos usar la siguiente regla: *si $(Lb + Lc) - La < \varepsilon$ entonces ya aceptamos aproximar el segmento de curva  por un tramo recto lo que significa que para ese tramo no se añaden más entradas en la tabla.*
![[metodo_adaptativo_aproximacion.png|500]]

Esta aproximación no es aplicable en el siguiente caso:
![[metodo_adaptativo_no_aplicable.png|400]]

*Para evitar este problema es necesario realizar una subdivisión al menos una vez.*

## CONTROL DE VELOCIDAD

Una **función de control de velocidad** establece la variación de la velocidad. La función decontrol de la velocidad *relaciona el tiempo transcurrido con la distancia recorrida*, esto nos permite obtener el espacio a partir de un valor de tiempo.

Uno de los controles de velocidad más conocidos es el **ease-in / ease-out** (sólo **ease** de aquí en adelante).
- Inicialmente la velocidad es *0*.
- Al principio se produce una *aceleración* constante hasta alcanzar la *velocidad máxima* (ésta puede ser mantenida).
- Después se produce el efecto *inverso*, decelera hasta pararse.

![[ease_graf1.png|300]]

$$
	p = P(U(S(t)))
$$
Siendo la distancia recorrida *$s = S(t)$*, el valor que nos permite resolver el polinomio *$u = U(s)$* y la posición en la que debemos colocar el objeto *$p = P(u)$*.

Para conseguir un resultado de tipo **ease** necesitamos aplicar una función que se le parezca. Hay varias opciones entre ellas la *función seno* o el *polinomio cúbico*.

### Polinomio Cúbico
![[polinomio_cubico.png|400]]

$$
	S = -2t^3 + 3t^2
$$

### Función Aceleración-Tiempo
![[funcion_aceleracion_tiempo_ease.png|300]]

[Demo de control tipo ease](http://cphoto.uji.es/vj1226/bezierAnimationEaseInOut/)

## INTERPOLACIÓN DE LA ORIENTACIÓN

Existe un problema al realizar una interpolación angular entre dos cuaterniones:
- **NO** se produce velocidad angular constante.

Esto es debido a que el ángulo entre cada interpolación no es regular:
![[angulos_no_regulares.png|300]]

Para solucionar este problema se realiza la interpolación denominada **en la superficie de la esfera.**
![[interpolacion_superficie_esfera.png|300]]

Para obtener las interpolaciones intermedias en la superficie de una esfera existe la función **slerp. *(no entra en el examen)***
El resultado que se produce del **slerp** no está normalizado.

$$
	slerp(q_1,q_2,u) = ((\sin((1-u)\theta))/\sin(\theta))q_1 + (\sin(u\theta)/\sin(\theta))q_2
$$

## RUTAS

El método de **Marco Frenet** establece que una vez obtenida la posición del objeto en la curva, el objeto se orienta en dirección a la tangente la curva en dicho punto, y su vector de inclinación se obtiene a partir del producto vectorial entre la tangente y el vector curva.

Si este método no nos vale, existen otras opciones.

___
# TEMA 2 : 
___
