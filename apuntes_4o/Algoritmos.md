___
# BÚSQUEDA EN VECTOR
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

___
# LISTAS ENLAZADAS
___

## TIPOS ABSTRACTOS DE DATOS (*TAD*)

### TAD Pila

pila.cpp
```cpp
  
#include <iostream>
#include <string>
using namespace std;

#include "Pila.h"

Pila::Nodo::Nodo(int d, Nodo * s) : dato{d}, siguiente{s} {
}

Pila::Pila() : laCima{nullptr}, laTalla{0} {

}
  
void Pila::apilar(int unDato) {
   laCima = new Nodo(unDato, laCima);
   laTalla++;
}

void Pila::desapilar() {
   if (laCima == nullptr)
      throw string("Intentando desapilar en una pila vacia");

   Nodo * basura = laCima;
   laCima = laCima->siguiente;
   delete basura;
   laTalla--;
}

int Pila::cima() const {
   if (laCima == nullptr)
      throw string("Intentando consultar la cima en una pila vacia");
   return laCima->dato;
}

void Pila::mostrar() const {
   cout << "[";
   for (Nodo * actual = laCima; actual != nullptr; actual = actual->siguiente) {
      cout << actual->dato;
      if (actual->siguiente != nullptr)
	 cout << ", ";
   }
   cout << "]";
}

int Pila::talla() const {
   return laTalla;
}

bool Pila::estaVacia() const {
   return laCima == nullptr;
}
```

pila.h
```cpp
  
class Pila {

   struct Nodo {
      int dato;
      Nodo * siguiente;
      Nodo(int, Nodo *);
   };

   Nodo * laCima;
   int laTalla;

public:

   Pila();
  
   void apilar(int);

   void desapilar();

   int cima() const;

   void mostrar() const;

   int talla() const;

   bool estaVacia() const;

};
```

testPila.cpp
```cpp
  
#include <iostream>
using namespace std;

#include <cstdlib>   // rand

#include "Pila.h"

int main () {
   Pila pila;
   int i;

   for (i = 11; i < 100; i += 11) {
      cout << "Insertando " << i << ": Pila=";
      pila.apilar(i);
      pila.mostrar();
      cout << "\tTalla=" << pila.talla() << endl;
   }

   cout << endl;

   while ( ! pila.estaVacia()) {
      cout << "Eliminando " << pila.cima() << ": Pila=";
      pila.desapilar();
      pila.mostrar();
      cout << "\tTalla=" << pila.talla() << endl;

      int unDatoCualquiera = rand() % 100;
      cout << "Insertando " << unDatoCualquiera << ": Pila=";
      pila.apilar(unDatoCualquiera);
      pila.mostrar();
      cout << "\tTalla=" << pila.talla() << endl;

      cout << "Eliminando " << pila.cima() << ": Pila=";
      pila.desapilar();
      pila.mostrar();
      cout << "\tTalla=" << pila.talla() << endl;
   }

   try {
      cout << "Eliminando " << pila.cima() << ": Pila=";
   } catch (string mensaje) {
      cout << "Probando excepcion: " << mensaje << endl;
   }
  
   try {
      pila.desapilar();
   } catch (string mensaje) {
      cout << "Probando excepcion: " << mensaje << endl;
   }
  

}
```

### TAD Cola

### TAD Cola de Prioridad

___
# ÁRBOLES
___

Un árbol es una conexión de nodos que o bien está vacía o bien se compone de un nodo raíz. Una raíz puede tener sub árboles conectados a modo de hijos. Los enlaces que conectan a los nodos son arcos. Las raíces sin hijos son hojas. La profundidad de un nodo son los pasos que hay que tomar desde la raíz hasta la hoja. La profundidad del árbol es la profundidad de la más profunda de sus hojas. La altura es lo mismo pero al revés.

## ÁRBOLES BINARIOS DE BÚSQUEDA (ABB)

Un árbol cuyas raíces tienen máximo dos hijos. Los hijos se ordenan a izquierda o a derecha dependiendo de si su valor es mayor o menor que el del nodo raíz.