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

![[Pasted image 20250102190757.png|300]]

<div class="border_round">
A <b>→</b> H <b>→</b> Z    <br>
G <b>→</b> H <b>→</b> L    <br>
H <b>→</b> A <b>→</b> L <b>→</b> W  <br>
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
	- [ ] "Evasion" es análoga a "Pursuit", salvo que "Wander" se usa para alejarse de la posición futura prevista del personaje objetivo.
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