___
# BÚSQUEDA
___

## BÚSQUEDA SECUENCIAL

Busca el elemento _e_ dentro de un vector _v_. Para ello comparo todos los elementos del vector _v_ con _e_.
El coste depende del tamaño del vector _v_ (talla del vector _N_).

### Coste Temporal

En el **mejor** de los casos el elemento _e_ se encuentra en la primera comparación. 
- $O(1)$

En el **peor** de los casos comparamos _e_ con todos los elementos del vector _v_. 
- $O(n)$

### Coste Espacial

En el **mejor** caso:
- $O(n)$

En el **peor** caso:
- $O(n)$


```cpp
int busquedaSecuencial(vector<int> v, int dato) {
	  
   for (int i = 0; i < v.size(); i++)
      if (v[i] == dato)
	 return i;
   return -1;

}
```

## BÚSQUEDA BINARIA (*ITERATIVA*)

Busca el elemento _e_ dentro de un vector _v_ ordenado. Para ello comparo el elemento que estoy buscando _e_ con el elemento del medio del vector _m_. Si son iguales termina el algoritmo, si no, dependiendo de si es mayor o menor , se toma una mitad del vector _v_ y se usa como vector _v'_ en la siguiente iteración del algoritmo. Esto se repite hasta encontrar el elemento o acabar con un vector _v'_ vacío.

### Coste Temporal

En el **mejor** de los casos encontramos el elemento en la primera comparación.
- $O(1)$

En el **pero** de loa casos repetimos el algoritmo $log(n)$ veces.
- $O(log(n))$

### Coste Espacial

En el **mejor** caso:
- $O(n)$

En el **peor** caso:
- $O(n)$

```cpp
int busquedaBinariaIterativa(vector<int> v, int dato) { 

   int inicio = 0,
       fin = v.size() - 1;

   while (inicio <= fin) {
      int medio = (inicio + fin) / 2;
      if (v[medio] < dato)
         inicio = medio + 1;
      else if (v[medio] > dato)
         fin = medio - 1;
      else
         return medio;
   }

   return -1;

}
```

___
# RECURSIÓN
___

## CALCULA FACTORIAL DE n

### Factorial Iterativo

Calcula el factorial de un número _n_ de forma iterativa.

```cpp
int factorial(int n) {
   int resultado = 1;
   for (int i = 2; i <= n; i++)
      resultado = resultado * i;
   return resultado;
}
```

```cpp
int factorial(int n) {
   if (n <= 1)
      return 1;	 
   else {	 
      int resultado = 1;
      for (int i = 2; i <= n; i++)
         resultado = resultado * i;
      return resultado;
   }
}
```

CTPC (Coste Temporal en el Peor Caso): $O(n).$
CTMC (Coste Temporal en el Mejor Caso): $O(n).$
CEPC (Coste Espacial en el Peor Caso): $O(1).$
CEMC (Coste Espacial en el Mejor Caso): $O(1).$

### Factorial Recursivo

Calcula el factorial de un número _n_ de forma recursiva.

```cpp
int factorial(int n) {
   if (n <= 1)
      return 1;
   else
      return n * factorial(n - 1);
}
```

CTPC (Coste Temporal en el Peor Caso): $O(n).$
CTMC (Coste Temporal en el Mejor Caso): $O(n).$
CEPC (Coste Espacial en el Peor Caso): $O(n).$
CEMC (Coste Espacial en el Mejor Caso): $O(n).$