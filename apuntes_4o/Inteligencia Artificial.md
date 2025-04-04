___

# REPASO PARA EL EXAMEN

___

## Estructura del examen:

- *PARTE 1 - Test* (50%, 40 min) (Los fallos penalizan, no entiendo cuanto, no me queda claro con lo que pone en el enunciado)
	- 1 pregunta de desarrollo
	- 19 preguntas de elección única entre cinco opciones
		- Preguntas de todos los contenidos.
		- 2 preguntas de resolución de problemas pathfinding.
- *PARTE 2 - Supuestos Prácticos* (50%, 90 min)
	- Mapas de *influencias*
		- Aplicar **filtros**
	- *ID3* (**I**nductive **D**ecisión tree algorithm **3**)
		- Árboles de decisión
		- Árboles de comportamiento
		- Más y más árboles, árboles por todas partes

___

# PARTE 1 - TEST

___

## Preguntas de Desarrollo:

### EXAMEN ENERO 2023
1) Explicar las diferencias entre búsqueda *"informada"* y *"no informada"* en grafos, en el contexto de *"PATHFINDING"*, dando ejemplos de algún algoritmo conocido en cada caso.

<p class="border_round">
La búsqueda no informada, o "a ciegas", es típica de algoritmos como "Depth First Search" o "Breath First Search" que no hacen uso de costes en las conexiones entre los nodos del grafo. Por el contrario, algoritmos de búsqueda dirigida (al nodo objetivo) como A*, hacen uso de la información de los costes en el grafo, y además de una función heurística que permite optimizar la ruta al nodo objetivo, basada en la información de distancia desde cada nodo al objetivo, proporcionada por dicha heurística. Otro ejemplo de búsqueda informada, basada en los costes asociados a las conexiones del grafo, sería el algoritmo de Dijkstra, tan utilizado en los juegos de estrategia.
</p>

### EXAMEN ENERO 2024
1) Define el aprendizaje por refuerzo y proporciona un ejemplo de cómo se podría aplicar en un entorno de videojuegos.

2) ¿Cómo se puede utilizar la inteligencia artificial en los videojuegos para mejorar la experiencia del jugador?


## Preguntas de Resolución de Problemas:

### EXAMEN ENERO 2023
10) Dado el espacio de búsqueda de la figura de la izquierda , se requiere encontrar un camino desde el estado inicial A al estado objetivo J. La tabla de la derecha muestra el valor de la función heurística con el coste estimado, desde cada nodo al nodo objetivo J. Indicar cuál sería el primer camino encontrado por el algoritmo A* utilizando la heurística dada.

![[IA_Enero2024_Test_ej10_grafoYtabla.png|500]]

- [ ] A, B, F, G, J
- [ ] A, E, H, M, N, J
- [ ] A, E, H, M, J
- [x] A, B, C, D G, J
- [ ] A, B, C, D, G, K, J

14) Construye la *Lista de Adyacencia* asociada al grafo mostrado.

![[IA_Enero2024_Test_ej14_grafo.png|300]]

<div class="border_round">
A <b>→</b> H <b>→</b> Z    <br>
G <b>→</b> H <b>→</b> L    <br>
H <b>→</b> A <b>→</b> G <b>→</b> W  <br>
L <b>→</b> G <b>→</b> X     <br>
W <b>→</b> H <b>→</b> Z<br>
X <b>→</b> L<br>
Z <b>→</b> A → W</div>

### EXAMEN ENERO 2024
11) Construye la lista de Adyacencia del Grafo mostrado.

![[IA_Enero2024_Test_ej11_grafo.png|300]]

<div class="border_round">
1 <b>→</b> 4 <b>→</b> 6 <br>
2 <b>→</b> 4 <b>→</b> 5<br>
3 <b>→</b> 4<br>
4 <b>→</b> 1 <b>→</b> 2 <b>→</b> 3<br>
5 <b>→</b> 2 <b>→</b> 7<br>
6 <b>→</b> 1<br>
7 <b>→</b> 5</div>


12) Dado el espacio de búsqueda de la figura, se requiere encontrar un camino desde el estado inicial S al estado objetivo G. La tabla muestra tres funciones heurísticas diferentes: h1, h2, y h3. Indicar los tres aminos encontrados por el algoritmo A* utilizando cada una de las heurísticas dadas.
![[IA_Enero2024_Test_ej12_grafo.png|300]]

|Node|$h_1$|$h_2$|$h_3$|
| --- | --- | --- | --- |
|S|$0$|$5$|$6$|
|A|$0$|$3$|$5$|
|B|$0$|$4$|$2$|
|C|$0$|$2$|$5$|
|D|$0$|$5$|$3$|
|G|$0$|$0$|$0$|

- [ ] $h_1$: S, B, C, G | $h_2$: S, B, C, G | $h_3$: S, B, C, G
- [ ] $h_1$: S, B, C, G | $h_2$: S, B, D, G | $h_3$: S, B, C, G
- [x] $h_1$: S, B, C, G | $h_2$: S, B, C, G | $h_3$: S, B, D, G
- [ ] $h_1$: S, B, D, G | $h_2$: S, B, D, G | $h_3$: S, B, C, G
- [ ] Todas las anteriores son falsas.


## Preguntas tipo Test:

### EXAMEN ENERO 2023

2) Entre las iniciativas de éxito (citadas a continuación), impulsadas por la IA moderna, indicar cuál **NO** es correcta:
	- [ ] Gran auge de los niveles de autonomía en la robótica.
	- [ ] IBM, a través de la computadora Deep Blue, derrota al campeón del mundo de ajedrez.
	- [ ] Progreso significativo de las técnicas de reconocimiento de formas provenientes del paradigma conexionista.
	- [x] Gran avance del "razonamiento automatizado el sistema común" por Minsky.

3) En el contexto del proyecto *Shakey* indicar cuál de las siguientes afirmaciones es correcta:
	- [ ] Fue un sistema pionero en el desarrollo de arquitecturas reactivas.
	- [ ] El "cerebro real" ocupaba varias salas con diferentes computadoras.
	- [x] Se desarrolló el algoritmo A* para la planificación de trayectorias.
	- [ ] Shakey fue descrito en la revista Life (1970) como "first iron person".
	- [ ] Sirvió de inspiración para desarrollar el algoritmo Dijkstra.

4)  Sobre el algoritmo de cálculo de caminos A*; indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] El algoritmo A* es un algoritmo "no informado" de búsqueda en grafos
	- [ ] Calcula siempre el camino más corto.
	- [ ] Calcula siempre el camino de menor coste.
	- [x] Calcula un camino subóptimo, es decir, un camino de bajo coste, pero no siempre el de menor coste.
	- [ ] Calcula siempre una solución en el menor tiempo posible.

5) Indicar qué aspecto, de los aquí descritos, **NO** se relaciona directamente con la IA aplicada a videojuegos.
	- [ ] Extensión del tiempo de vida del videojuego.
	- [x] Sensorización y captura del movimiento.
	- [ ] Simulación completa de un jugador virtual (bot)
	- [ ] Generación de mapas y terrenos.
	- [ ] Generación de enemigos más inteligentes.

**Tengo mucahs preguntas, esta solución no tiene sentido**

6) En el contexto *Learning* ¿Cómo descubren las computadoras nuevos conocimientos?
	- [ ] Reduciendo de forma sistemática la incertidumbre.
	- [ ] Simulando estrategias evolutivas.
	- [ ] Emulando el comportamiento del cerebro.
	- [ ] Descubriendo similitudes entre lo antiguo y lo nuevo
	- [x] Todas las respuestas anteriores son correctas.

7) Acerca del algoritmo de *Dijkstra*; indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [ ] Fue originalmente diseñado para resolver un problema en la teoría matemática de grafos, denominado de forma confusa "el camino más corto".
	- [ ] Es un algoritmo muy utilizado en el análisis táctico.
	- [ ] El algoritmo de Dijkstra termina generalmente cuando la denominada lista abierta está vacía.
	- [x] Se puede modificar, de manera eficiente, para generar solo el camino que nos interesa.
	- [ ] Tiene gran aplicación en los juegos de estrategia.

8) En el contexto de la IA académica; indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] La IA es la ciencia y la ingeniería de hacer máquinas inteligentes, especialmente programas informáticos inteligentes.
	- [ ] Una máquina inteligente tenderá a construir dentro de sí misma un modelo abstracto del entorno en el que se ubica.
	- [ ] El primer texto publicado, escrito por Turing, enfocado completamente en la inteligencia de las máquinas fue "Computing Machinery and Intelligence" (1950).
	- [ ] Una medida de la inteligencia de cualquier homínido es la fracción de su corteza motora dedicada al control de su capacidad manipuladora.
	- [x] Todas las respuestas anteriores son correctas.

9) Con relación al algoritmo A*; indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] A* es un algoritmo completo, es decir, en caso de existir una solución, siempre dará con ella.
	- [ ] A* con una heurística idénticamente nula daría lugar al algoritmo de Dijkstra.
	- [ ] La diferencia con otros algoritmos es que A* también tiene en cuenta el coste desde el principio, y no simplemente el coste local del nodo visitado anterior mente.
	- [ ] Actualmente se trabaja en la generación automática de heurísticas para el A*.
	- [x] Todas las anteriores son correctas.

11) ¿En el nivel táctico de la IA para videojuegos, cuál de las siguientes afirmaciones es correcta?
	- [ ] Las localizaciones en el análisis táctico forman una representación natural del nivel del juego, especialmente en los niveles "outdoor".
	- [ ] Básicamente, el Pathfinding táctico, en lugar de buscar la ruta más corta o rápida, se focaliza en la situación táctica del juego.
	- [ ] Para el pathfinding táctico se emplean los mismos algoritmos convencionales de path-finding, y con el mismo tipo de representación gráfica.
	- [ ] En niveles "indoor", o para huegos sin análisis táctico, podemos usar los denominados "waypoint" tácticos. 
	- [x] Son correctas todas las anteriores.

12) En el contexto del denominado *Q-Learning;* indicar cual de las siguientes afirmaciones **NO** es correcta.
	- [ ] No requiere un modelo predefinido del entorno.
	- [ ] El algoritmo trabaja de forma iterativa, generando episodios sucesivos.
	- [x] Cuanto menor sea el parámetro "Gamma" más influencia tienen las recompensas futuras.
	- [ ] "Q" se puede decir que representa la "calidad" de una acción tomada en un estado dado.
	- [ ] El objetivo siempre es alcanzar el estado asociado con la mayor recompensa.

13) En el contexto de *machine learning;* ¿Qué tipo de aprendizaje es el más apropiado para generar escenarios?
	- [x] Aprendizaje no supervisado.
	- [ ] Aprendizaje supervisado.
	- [ ] Aprendizaje por refuerzo.
	- [ ] Aprendizaje aleatorio..
	- [ ] Son falsas todas las anteriores.

15) En el contexto de los planificadores; indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [ ] Un NPC percibe el entorno (el mundo de juego virtual) a través de sensores y actúa sobre él a través de actuadores (componentes de software que afectan al mundo virtual).
	- [ ] El agente reactivo deriva sus decisiones únicamente sobre la base de sus percepciones actuales en lugar de las basadas en modelos que utilizan el histórico de percepciones.
	- [ ] Históricamente, el planificador STRIPS se utilizó para guiar los movimientos de Shakey hacia sus objetivos.
	- [x] Un planificador requiere de un modelo del mundo, que utiliza exclusivamente dos ingredientes: un conjunto de estados y un conjunto de acciones.
	- [ ] Un NPC en el nivel de implementación se diseña, comúnmente, como agente.

16) En el contexto denominado *Decision Making;* indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] En las "máquinas de estado jerárquicas" (HFSM) se utilizan algoritmos iterativos para procesar toda la jerarquía..
	- [ ] El denominado "Goal-Oriented Action Planing" fue desarrollado a partir del videojuego "Halo 2".
	- [ ] Los "Árboles de Comportamiento" implementan una forma de búsqueda simple, a veces denominada planificación activa.
	- [x] Las "Condiciones" y "Acciones" de un "Árbol de Comportamiento" son tareas que ocuparán siempre las Hojas de dicha estructura.
	- [ ] Todas las anteriores son correctas.

17) En el contexto de los *Steering Behaviors;* indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [ ] Un grupo de steering behaviors se puede combinar para actuar como un solo comportamiento.
	- [ ] Arrival es análoga de Seek mientras el personaje está lejos de alcanzar su objetivo.
	- [ ] Evasion es similar a Flee excepto que ahora el objetivo es otro personaje en movimiento.
	- [x] Para calcular la dirección en path following, se realiza una predicción basada en la velocidad de la posición futura del NPC.
	- [ ] Alignment calcula una orientación 

18) En el contexto de los denominados *Pathfinding Graphs;* indicar cuál de las siguientes respuestas **NO** es correcta.
	- [ ] Existen algoritmos d búsqueda no informada, como los de búsqueda en amplitud o en profundidad, los cuales son capaces de identificar el nodo objetivo sin utilizar el coste del camino encontrado.
	- [x] Para representar un grafo se utilizan, con igual eficiencia, o bien las listas o bien las matrices de adyacencia. 
	- [ ] La esencia crucial del grafo es su conectividad.
	- [ ] El número de conexiones, en la ruta más corta del grafo que conecta dos nodos, se denomina distancia topológica entre dichos nodos.
	- [ ] Los grafos adecuados para pathfinding son grafos dirigidos, ponderados y no negativos.

19) Relativo a la "Representación del Mundo" en el Pathfinding; indicar cuál de las siguientes afirmaciones no es correcta.
	- [ ] El mecanismo necesario para convertir localizaciones del juego en nodos del grafo se denomina "Quantization".
	- [ ] El mecanismo necesario para convertir los nodos del grafo, que forman el camino encontrado, en las localizaciones del juegos se denomina "Localization".
	- [ ] La representación más simple usada para teselar el espacio será la rejilla (tile graph), que ofrece una representación del grafo elemental, aunque pueda ser poco eficiente, dado el número de nodos que suele conllevar.
	- [ ] Cuantos menos nodos haya en el grafo, y mejor ubicados, más eficiente será el comportamiento de los algoritmos pathfinding.
	- [x] La técnica manual por excelencia para teselar el espacio se basa en los denominados "Points of Visibility".

20) En el contexto de los "Árboles de Decisión"; indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] Aunque al árbol de decisión es más simple con múltiples ramas, la velocidad de ejecución no mejora significativamente.
	- [ ] Los árboles de decisión clasifican las variable continuas, creando regiones binarias a partir de umbrales.
	- [ ] Los árboles de decisión suelen ser binarios porque pueden optimizarse más fácilmente.
	- [ ] Con un árbol binario se puede resolver cualquier cosa que se pueda solucionar con un árbol más complejo, por ello los árboles de decisión suelen implementarse como binarios.
	- [x] Todas las anteriores son correctas.

### EXAMEN ENERO 2024

3) En el contexto del proyecto del robot *Shakey;* indicar cuál de las siguientes afirmaciones es correcta.
	- [x] Sirvió de inspiración en la planificación de tareas.
	- [ ] El "cerebro real" ocupaba varias salas con diferentes computadoras.
	- [ ] Se desarrolló el algoritmo de Dijkstra para la planificación de trayectorias.
	- [ ] Constituyó un hito en su capacidad senso-motora.
	- [ ] Todas las anteriores son correctas.

4) ¿Qué método de aprendizaje por refuerzo es más adecuado para entrenar un agente en un entorno de videojuego en tiempo real?

	- [ ] Aprendizaje profundo.
	- [ ] Aprendizaje supervisado.
	- [x] Q-Learning.
	- [ ] Todas las anteriores son correctas.

5) En el contexto de la IA existe un paradigma denominado IA fuerte o "strong AI" que se caracteriza por perseguir la creación de (marcar donde corresponda):
	- [ ] Un programa informático que produce el comportamiento racional más fuerte posible para tomar una decisión.
	- [x] Un programa informático capaz de modelar el razonamiento cognitivo del ser humano.
	- [ ] Un programa informático capaz de superar al ser humano en el test de Turing.
	- [ ] Un programa informático capaz de mantener una conversación con un ser humano.
	- [ ] Todas las anteriores son correctas.

6) Entre las diferentes herramientas utilizadas en IA para videojuegos existen algunas que facilitan enormemente el procesamiento desacoplado de objetivos y acciones. Indicar cuál de las siguientes sería la idónea:
	- [ ] Máquinas de estado finito.
	- [ ] Árboles binarios de decisión.
	- [x] Planificadores.
	- [ ] Árboles de comportamiento.
	- [ ] Todas las respuestas anteriores son correctas.

7) Acerca del algoritmo de *Dijkstra;* indicar cuál de las siguientes es correcta.
	- [ ] Fue originalmente diseñado para resolver un problema en la teoría matemática de grafos, denominado de forma confusa determinación del "camino más corto".
	- [ ] Es un algoritmo muy utilizado en el análisis táctico.
	- [ ] Tiene gran aplicación en los videojuegos de estrategia.
	- [ ] Este algoritmo no funciona con grafos donde aparecen costes negativos.
	- [x] Todas las respuestas anteriores son correctas.

8) Un algoritmo de búsqueda se denomina completo si (marca la correcta):
	- [ ] Siempre encuentra la solución óptima.
	- [x] Siempre encuentra una solución si ésta existe.
	- [ ] Encuentra todas las soluciones posibles.
	- [ ] Son correctas (a) y (b) pero no (c)
	- [ ] Son correctas (a), (b) y (c)

9) Con relación al algoritmo A*; indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] A* es un algoritmo completo, es decir, en caso de existir una solución siempre dará con ella.
	- [ ] A* con una heurística idénticamente nula daría lugar al algoritmo de Dijkstra.
	- [ ] La diferencia con otros algoritmos es que A* también tiene en cuenta el coste desde el principio, y no simplemente el coste local del nodo visitado anteriormente.
	- [ ] Actualmente se trabaja en la generación automática de heurísticas para A*.
	- [x] Todas las anteriores son correctas.

10) En el contexto del denominado "Pathfinding" existen una serie de propiedades necesarias para vincular los caminos encontrados en la representación típica de los grafos con la representación del mundo asociada. Indicar la respuesta correcta.
	- [ ] Cuantización/Localización; Generación; Depuración.
	- [x] Cuantización/Localización; Generación; Validación.
	- [ ] Cuantización/Localización; Implementación; Validación.
	- [ ] Son correctas (a) y (b) pero no (c)
	- [ ] Son correctas (a), (b) y (c)

13) En el contexto del denominad *Q-Learning;* indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [x] Requiere un modelo predefinido del entorno.
	- [ ] El algoritmo trabaja de forma iterativa, generando episodios sucesivos.
	- [ ] Cuanto menor sea el parámetro "Gamma" menos influencia tienen las recompensas futuras.
	- [ ] "Q" se puede decir que representa la "calidad" de una acción tomada en un estado dado.
	- [ ] El objetivo siempre es alcanzar el estado asociado con la mayor recompensa.
14) Entre las siguientes ventajas del denominado *Paradigma Conexionista;* indicar cuál **NO** es correcta.
	- [ ] La computación no se rige por reglas.
	- [ ] La información es distribuida.
	- [ ] Permite la tolerancia a fallos respecto a los datos.
	- [x] Reproducen el procesamiento en serie.
	- [ ] Todas las anteriores son correctas.

15) En el contexto de los denominados *Steering Behaviors;* indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [ ] "Seek" (o búsqueda de un objetivo estático) actúa para dirigir al personaje hacia una posición especificada en el espacio global.
	- [ ] "Flee" es simplemente la operación inversa de "Seek".
	- [ ] "Pursuit" es similar a "Seek" excepto que ahora el objetivo es otro personaje en movimiento.
	- [x] "Evasion" es análoga a "Pursuit", salvo que "Wander" se usa para alejarse de la posición futura prevista del personaje objetivo.
	- [ ] Son correctas todas las anteriores.

16) En el contexto del denominado análisis táctico se suele distinguir entre propiedades estáticas, dinámicas y evolución. Indica cuál de las siguientes afirmaciones es correcta.
	- [ ] El terreno y la topología se consideran propiedades estáticas.
	- [ ] Los recursos humanos se consideran propiedades en evolución.
	- [ ] El nivel de peligro se considera una propiedad dinámica.
	- [x] Son correctas todas las anteriores.

17) En el contexto de las denominadas *Máquinas de Estado Finito* (FSMs) se aprecian una serie de limitaciones en cuanto a su uso en videojuegos. Indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [x] Son fáciles de reutilizar en juegos diferentes.
	- [ ] El proceso de edición de la lógica de un FSM es de muy bajo nivel.
	- [ ] Operan siempre en un nodo reactivo.
	- [ ] Conllevan una mínima sobrecarga computacional.
	- [ ] Son intuitivas y se asemejan al modelo de razonamiento humano.

18) En el contexto de los denominados *Behavior Trees* (BTs) se aprecian una serie de ventajas en cuanto a su uso en videojuegos. Indicar cuál de las siguientes afirmaciones **NO** es correcta.
	- [ ] Son fácilmente escalables.
	- [ ] Permiten un alto grado de reusabilidad.
	- [x] Un referente de uso en la industria de videojuegos sería "F.E.A.R." de Monolith Productions.
	- [ ] Permiten ejecución en modo concurrente.
	- [ ] Su programación es más compleja que la de Máquinas de Estado.

19) ¿Cuál es el papel principal de los algoritmos de *pathfinding* en el contexto de los videojuegos? Indica la afirmación correcta.
	- [ ] Generar gráficos tridimensionales.
	- [ ] Tomar decisiones estratégicas.
	- [ ] Planificar la distribución de recursos.
	- [x] Encontrar rutas óptimas de movimiento.
	- [ ] Optimizar algoritmos de renderización.

20) En el contexto de los *Árboles de decisión;* indicar cuál de las siguientes afirmaciones es correcta.
	- [ ] Aunque el árbol de decisión es más simple con múltiples ramas, la velocidad de ejecución no mejora significativamente..
	- [ ] Los árboles de decisión clasifican las variables continuas, creando regiones binarias a partir de umbrales.
	- [ ] Los árboles de decisión suelen ser binarios porque pueden optimizarse más fácilmente.
	- [ ] Con un árbol binario se puede resolver cualquier cosa que se pueda solucionar con un árbol más complejo, por ello los árboles de decisión suelen implementarse como binarios.
	- [x] Don correctas todas las anteriores.

___
# PARTE 2 - PROBLEMAS
___

### EXAMEN ENERO 2023

1) En el contexto de los juegos de estrategia (RTS games) se tiene la sección de un mapa de influencia representada en la fig. (A) , a la cual se le pasa el filtro de convolución de la fig. (B).

![[IA_Enero2023_Problemas_ej1.png|400]]

-  Dicho filtro de convolución es un filtro Gaussiano y, por lo tanto, es separable como producto de las dos matrices que se indican a continuación.

$$
	\frac {1}{16}
	\begin{bmatrix}
		1 & 2 & 1 \\
		2 & 4 & 2 \\
		1 & 2 & 1
	\end{bmatrix}
	=
	\frac {1}{4}
	\begin{bmatrix}
		1 \\
		2 \\
		1 
	\end{bmatrix}
	\times
	\frac {1}{4}
	\begin{bmatrix}
		1 & 2 & 1
	\end{bmatrix}
$$

- Se demuestra que si, en lugar de realizar la convolución directamente con el filtro completo (fig. B), se realiza dicha operación en dos pasos, se llega al mismo resultado, optimizando el coste computacional.
	- a) Se pide completar las tablas siguientes, que representan el resultado de convolucionar el filtro vertical primero (izquierda), y a continuación el filtro horizontal (derecha). Dar el resultado en números enteros o racionales (no utilizar reales con decimales).

![[IA_Enero2023_Problemas_ej1a.png|400]]
- 
	- b) ¿Cómo has modificado la matriz de ambos filtros para aplicar en los bordes?

<p style="text-align: center;"><b style="color: coral;"> ES CRUACIAL APORTAR TODAS LAS OPERACIONES REALIZADAS </b></p>

### Solución apartado (A)

<div class="border_round">
<p style="text-align: center;">
	Resultado "Filtro Vertical"
	<table  id="cell_square">
	  <tr>
	    <td>26/3</td>
	    <td>17/3</td>
	    <td>10/3</td>
	  </tr>
	  <tr>
	    <td>31/4</td>
	    <td>9/2</td>
	    <td>11/4</td>
	  </tr>
	  <tr>
	    <td>20/3</td>
	    <td>13/3</td>
	    <td>8/3</td>
	  </tr>
	</table><br>
	Resultado "Filtro Horizontal"
	<table id="cell_square">
	  <tr>
	    <td>23/3</td>
	    <td>35/6</td>
	    <td>37/9</td>
	  </tr>
	  <tr>
	    <td>20/3</td>
	    <td>39/8</td>
	    <td>10/3</td>
	  </tr>
	  <tr>
	    <td>53/9</td>
	    <td>9/2</td>
	    <td>29/9</td>
	  </tr>
	</table><br>
</p>
</div>

### Explicación

Veamos ahora un caso de ejemplo.
Para la Matriz asociada al Filtro vertical: Valor esquina superior izquierda. (23/6). Dicho valor se obtiene al convolucionar la submatriz del filtro vertical $\frac {1}{3} \begin{bmatrix} 1 \\ 2\end{bmatrix}$ con $\begin{bmatrix} 9 \\ 8 \end{bmatrix}$, es decir, $\frac {1}{3} \begin{bmatrix} 18 \\ 8\end{bmatrix}=26/3$ .
Fijémonos que este valor se acaba convirtiendo en *$23/3$*, en la Matriz asociada al Filtro horizontal, ya que deviene de la convolución de la submatriz del filtro horizontal $\frac {1}{3} \begin{bmatrix} 1 & 2\end{bmatrix}$ con $\begin {bmatrix} 26/3 & 17/3 \end{bmatrix}$, obteniendo previamente para el filtro vertical, es decir, *$23/3$*

### Solución apartado (B)

<div class="border_round">
<p style="text-align: center;">
	<img width="500" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2023_Problemas_ej1b_sol.png" alt="Proceso aplicación de filtros vertical y horizontal">
</p>
</div>

2) En el contexto de un juego de estrategia, se tiene el siguiente conjunto de 10 ejemplos.

![[IA_Enero2023_Problemas_ej2.png|400]]

- a) Aplicando el algoritmo ID3 (Inductive Decision tree algorithm 3), para generar el árbol binario de decisión asociado a dichos ejemplos, se llega, tras la primera iteración, al siguiente resultado.

![[IA_Enero2023_Problemas_ej2_arbol1.png|400]]

- Aplicar la siguiente iteración del algoritmo ID3 para completar el árbol mostrado. Se aconseja mantener cuatro cifras decimales en todos los cálculos.

- b) Demostrar, utilizando la representación de reglas "IF THEN" asociada al árbol obtenido, que efectivamente contiene solución explícita a los 10 ejemplos dados.

![[IA_Enero2023_Problemas_ej2_ayuda.png|500]]

### Solución apartado (A)

<div class="border_round">
<p>
	Teniendo en cuenta la distribución inicial de las acciones, para el conjunto total de ejemplos, se calcula la <b>Entropía Global:</b><br><br>
	(Attack: 6/10; Defend 4/10), Lo que implica: <i>E = – (3/5 log2 3/5) – 2/5 log2 2/5) = 0,9710</i>
	<br><br>
	Ahora bien, en la 2ª iteración de ID3, lo que tenemos que clasificar son los 5 ejemplos identificados en el árbol anterior: {1, 2, 6, 7, 8}, cuyas acciones son: <i>(Attack: 1/5; Defend 4/5). Lo que implica: E(cover) = – (1/5 log2 1/5) – 4/5 log2 4/5) = 0,7219</i>
	<br><br>
	<table id="cell_auto_adjust">
	  <tr>
	    <td>1</td>
	    <td>With ammo</td>
	    <td>High</td>
	    <td>Defend</td>
	  </tr>
	  <tr>
	    <td>2</td>
	    <td>With ammo</td>
	    <td>High</td>
	    <td>Defend</td>
	  </tr>
	  <tr>
	    <td>6</td>
	    <td>Empty</td>
	    <td>High</td>
	    <td>Defend</td>
	  </tr>
	  <tr>
	    <td>7</td>
	    <td>With ammo</td>
	    <td>High</td>
	    <td>Defend</td>
	  </tr>
	  <tr>
	    <td>8</td>
	    <td>With ammo</td>
	    <td>Normal</td>
	    <td>Attack</td>
	  </tr>
	</table>
	<br><br>
	Nótese que la propiedad "Cover" ya ha sido tenida en cuenta como nodo raíz y, por loo tanto, se descarta del subconjunto de los 5 ejemplos que se procesan en la nueva iteración.
	<br><br>
	Así, calculamos la Ganancia para la 1ª propiedad (Ammo), que tiene dos atributos: Ammo y Empty.
	<br><br>
	<img width="400" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2023_Problemas_ej2a1.png" alt="Fórmulas como las de antes">
	<br><br>
	Calculamos ahora la Ganancia para la 2ª propiedad (Distance). Tiene dos atributos: High y Normal.
	<br><br>
	<img width="400" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2023_Problemas_ej2a2.png" alt="Fórmulas como las de antes">
	<br><br>
	Lo que implica que la máxima Ganancia en información se asocia con el atributo "Distance". Por tanto, la solución será:
	<br><br>
	<img width="400" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2023_Problemas_ej2a3.png" alt="Árbol resultante">
</p>
</div>

### Solución apartado (B)

<div class="border_round">
<p>
	<table id="cell_auto_adjust">
		<tr>
			<td style="font-weight: 750; width: 85vw;">Reglas Asociadas al Árbol de Decisión</td>
			<td style="font-weight: 750; width: 30vw;">Ejemplos</td>
		</tr>
		<tr>
			<td class="cell_align_left">IF (Cover = No) THEN Attack</td>
			<td>{3,5,9,10}</td>
		</tr>
		<tr height="5px"> <td></td> <td></td> </tr>
		<tr>
			<td class="cell_align_left">IF (Cover = Yes) ^ (Distance = N) THEN Attack</td>
			<td>{8}</td>
		</tr>
		<tr height="5px"> <td></td> <td></td> </tr>
		<tr>
			<td  class="cell_align_left">IF (Cover = Yes) ^ (Distance = H) THEN Defend</td>
			<td>{1,2,6,7}</td>
		</tr>
	</table>
</p>
</div>

### EXAMEN ENERO 2024

1) En el contexto de los juegos de estrategia (RTS games) se tiene la sección de un Mapa de Influencia representado en la fig. (A), a la cual se le pasan de forma secuencial, primero el filtro de convolución de la fig. (B), y a continuación el de la fig. (C).

![[IA_Enero2024_Problemas_ej1.png|500]]

- Se pide los siguiente:
	- a) (0,2) Demostrar que el filtro de convolución dado en (B) es separable. Es decir, puede representarse como producto de dos matrices, una vertical y otra horizontal.
	- b) (1) Aplicar, a continuación, dichos filtros de forma unidimensional (primero vertical y luego horizontal), a la sección del Mapa de Influencias previo (A). ¿Cómo has modificado la matriz de ambos filtros para aplicarla en los bordes?
	- c) (1) Aplicar, a continuación, el filtro dado en (C) a la sección del Mapa de Influencia previo (A) ¿Cómo has modificado la matriz para aplicarla en los bordes?
	- d) (0,3) Explicar las diferencias de los dos tipos de filtros dados. ¿Para qué pueden ser útiles?

### Solución apartado (A)

<div class="border_round">
<p>
	<img width="300" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2024_Problemas_ej1a.png" alt="Matriz fig B dividida en dos">
</p>
</div>

### Solución apartado (B)

<div class="border_round">
<p style="text-align: center;">
	Resultado "Filtro Vertical"
	<table  id="cell_square">
	  <tr>
	    <td>7/2</td>
	    <td>9/2</td>
	    <td>5/2</td>
	  </tr>
	  <tr>
	    <td>5</td>
	    <td>16/3</td>
	    <td>7/3</td>
	  </tr>
	  <tr>
	    <td>13/2</td>
	    <td>13/2</td>
	    <td>3</td>
	  </tr>
	</table><br>
	Resultado "Filtro Horizontal"
	<table id="cell_square">
	  <tr>
	    <td>4</td>
	    <td>7/2</td>
	    <td>7/2</td>
	  </tr>
	  <tr>
	    <td>31/6</td>
	    <td>38/9</td>
	    <td>23/6</td>
	  </tr>
	  <tr>
	    <td>13/2</td>
	    <td>16/3</td>
	    <td>19/4</td>
	  </tr>
	</table><br>
	Explicación del procedimiento:
	<img width="500" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2024_Problemas_ej1b.png" alt="Proceso aplicación de filtros vertical y horizontal">
</p>
</div>

### Solución apartado (C)

<div class="border_round">
<p style="text-align: center;">
	Resultado "Filtro C"
	<table id="cell_square">
	  <tr>
	    <td>2</td>
	    <td>6</td>
	    <td>-2</td>
	  </tr>
	  <tr>
	    <td>9</td>
	    <td>11</td>
	    <td>11</td>
	  </tr>
	  <tr>
	    <td>28</td>
	    <td>19</td>
	    <td>-1</td>
	  </tr>
	</table><br>
	Explicación del procedimiento:
	<img width="500" src="E:\universidad\Apuntes\apuntes_4o\imgs\IA_Enero2024_Problemas_ej1c.png" alt="Proceso aplicación de filtros c">
</p>
</div>

### Solución apartado (D)

<div class="border_round">
<p>
	El primer filtro (B) es de tipo "paso bajo", y básicamente se trata de un filtro que realiza un suavizado del mapa de bits (<i>blur filter</i>), asignando al píxel central la media de todos los píxeles incluidos en la ventana. La matriz de filtrado estaría compuesta por unos y el divisor sería el número total de elementos en la matriz. Se trata por tanto del denominado "filtro de media". Ayudan a homogeneizar la imagen y eliminar el ruido de fondo.
	<br><br>
	El segundo filtro (C) es de tipo "paso alto", y su objetivo es el contrario de los anteriores, resaltando las fuentes de mayor variabilidad en el mapa de bits (<i>sharpening filter</i>), ayudando por tanto a identificar las fuentes de influencia en los mapas así denominados.
</p>
</div>

2) En el contexto de un juego de estrategia, se tiene el siguiente conjunto de 5 ejemplos

___
# COSAS IMPORTANTES (chat GPT)
___

Aquí tienes ejemplos de matrices **3x3** para filtros **de paso alto** y **de paso bajo**, sin fracciones, con una breve descripción de su característica principal:

### **Filtro de Paso Bajo (Suavizado)**

El filtro de paso bajo se utiliza para suavizar la imagen, eliminando detalles finos y manteniendo las áreas suaves.

#### 1. **Filtro de Paso Bajo Simple**
$$
G = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{pmatrix}
$$
**Característica**: Filtro uniforme que suaviza la imagen de manera simple sin distinguir entre el centro y los bordes.

#### 2. **Filtro de Paso Bajo con más énfasis en el centro**
$$
G = \begin{pmatrix} 0 & 1 & 0 \\ 1 & 2 & 1 \\ 0 & 1 & 0 \end{pmatrix}
$$
**Característica**: Suaviza la imagen con mayor peso en el centro, proporcionando un desenfoque más centrado.

#### 3. **Filtro de Paso Bajo Suavizado Moderado**
$$
G = \begin{pmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{pmatrix}
$$
**Característica**: Suaviza la imagen, preservando las características de mayor escala y eliminando detalles más finos.

---

### **Filtro de Paso Alto (Realce de bordes)**

El filtro de paso alto se utiliza para resaltar los bordes y eliminar las áreas suaves de la imagen.

#### 4. **Filtro de Paso Alto Simple**
$$
G = \begin{pmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{pmatrix}
$$
**Característica**: Resalta los bordes de la imagen mediante una diferencia entre los píxeles cercanos, eliminando áreas suaves.

#### 5. **Filtro de Paso Alto con énfasis central fuerte**
$$
G = \begin{pmatrix} 0 & -1 & 0 \\ -1 & 5 & -1 \\ 0 & -1 & 0 \end{pmatrix}
$$
**Característica**: Resalta bordes más agudos, con un fuerte énfasis en el valor central para aumentar el contraste.

#### 6. **Filtro de Paso Alto Moderado**
$$
G = \begin{pmatrix} -1 & -1 & -1 \\ -1 & 4 & -1 \\ -1 & -1 & -1 \end{pmatrix}
$$
**Característica**: Realza los bordes con un poco menos de agresividad, destacando las transiciones de la imagen.

---

### Resumen:

- **Filtros de paso bajo**: Suavizan la imagen, eliminando detalles pequeños y preservando áreas más grandes y suaves.
- **Filtros de paso alto**: Realzan los bordes y detalles finos, eliminando las áreas de suavizado para destacar las transiciones bruscas.

Ambos filtros tienen aplicaciones importantes en procesamiento de imágenes, como la eliminación de ruido (paso bajo) o la detección de bordes (paso alto).

