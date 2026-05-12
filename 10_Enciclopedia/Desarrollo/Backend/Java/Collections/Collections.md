---
status: final
tags:
  - java
  - backend
  - colecciones
  - utn
created: 2026-04-07
---
# 🏗️ Java Collections Framework (JCF)

En **[[Java]]**, el **Java Collections Framework** (**JCF**) es una arquitectura unificada para representar y manipular colecciones de datos. Básicamente, es un conjunto de interfaces y clases que te permiten manejar grupos de objetos de manera mucho más eficiente que usando simples arrays.

Antes de que existiera este framework (en versiones muy viejas de **[[Java]]**), cada desarrollador tenía que escribir sus propias estructuras de datos, lo cual era un caos de interoperabilidad.

---
## 🌳 La Jerarquía de [[Collections]]

Para entender **Java Collections**, hay que visualizarlo como un árbol. En la cima está la interfaz **Iterable**, seguida por **Collection**. Sin embargo, es más útil dividirlo por el tipo de comportamiento que ofrecen sus interfaces principales:


### 1. [[List]] (Interfaz)
Es una colección ordenada que permite elementos duplicados. Puedes acceder a los elementos por su índice (posición).
* **[[ArrayList]]**: La implementación más común. Es excelente para lecturas rápidas por índice, pero lenta para insertar o eliminar elementos en el medio de la lista.
* **[[LinkedList]]**: Ideal si necesitas insertar o eliminar elementos frecuentemente en cualquier posición, ya que funciona como una lista doblemente enlazada.

### 2. [[Set]] (Interfaz)
Es una colección que no permite duplicados. Es ideal para modelar abstracciones matemáticas de conjuntos.
* **[[HashSet]]**: No garantiza ningún orden específico. Es extremadamente rápido para búsquedas.
* **[[TreeSet]]**: Mantiene los elementos ordenados (según su orden natural o un comparador).
* **[[LinkedHashSet]]**: Mantiene el orden de inserción.


### 3. [[Queue]] (Interfaz)
Diseñada para retener elementos antes de procesarlos, usualmente siguiendo el principio **FIFO** (*First-In, First-Out*).
* **[[PriorityQueue]]**: Los elementos se procesan según su prioridad, no necesariamente por el orden en que llegaron.



### 4. [[Map]] (Interfaz)
Aunque técnicamente no hereda de la interfaz **[[Collections]]**, se considera parte del framework. Almacena datos en pares de **clave-valor**. Las claves deben ser únicas.
* **[[HashMap]]**: El estándar. Rápido y permite una clave nula.
* **[[TreeMap]]**: Mantiene las claves ordenadas.

---

## ✨ Ventajas de usar [[Collections]]

* **Reducción del esfuerzo:** No tienes que reinventar la rueda programando una lista enlazada o un árbol de búsqueda.
* **Rendimiento:** Las implementaciones están altamente optimizadas.
* **Interoperabilidad:** Todas las librerías de **[[Java]]** entienden estas interfaces, lo que facilita pasar datos de un módulo a otro.
* **Algoritmos integrados:** La clase de utilidad `Collections` (en plural) ofrece métodos estáticos para ordenar, buscar, mezclar o invertir elementos de forma inmediata.

---
