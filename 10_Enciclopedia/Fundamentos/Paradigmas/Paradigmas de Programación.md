---
status: final
tags:
  - conceptos
  - paradigmas
  - programacion
created: 2025-12-10
---
# 🧠 ¿Qué es un Paradigma de Programación?

Un **paradigma de programación** es un estilo, enfoque o "forma de pensar" para resolver problemas computacionales. No constituye un lenguaje en sí mismo, sino el conjunto de principios y reglas que sigue un lenguaje (o un programador) para estructurar y organizar el código.

### 🍳 Analogía: La Cocina

Para ilustrar el concepto, se puede considerar la preparación de una cena:

* **[[Paradigma Imperativo]]:** "Seguir una receta paso a paso".
* **[[Paradigma Declarativo]]:** "Contratar un servicio de catering y solicitar el menú" (se solicita el resultado sin preocuparse por el proceso de elaboración).

---

## 🏗️ Principales Ejemplos de Paradigmas

Aunque existen múltiples enfoques, los cuatro más relevantes en la industria actual son:

### 1. [[Paradigma Imperativo|Programación Imperativa]] (El "Cómo")
Es el estilo más clásico. Se proporcionan a la computadora instrucciones detalladas paso a paso para modificar el estado del programa.

* **Enfoque:** Controlar el flujo de ejecución y manipular variables.
* **Lenguajes típicos:** C, Pascal, BASIC.
* **Ejemplo:** "Crea una variable x. Súmale 1. Si x es mayor a 10, detente."

### 2. Programación Orientada a Objetos ([[P.O.O]])
Organiza el código en unidades llamadas **Objetos**, que combinan datos (atributos) y comportamientos (métodos). Su objetivo es modelar entidades del mundo real.

* **Enfoque:** Encapsular datos y reutilizar código mediante clases y herencia.
* **Lenguajes típicos:** [[Java]], [[C SHARP]], [[Python]], [[C++|C++]].
* **Ejemplo:** Se dispone de un objeto `Coche` con atributos como `color` y métodos como `acelerar()`.

### 3. Programación Funcional
Trata la computación como la evaluación de funciones matemáticas. Evita cambiar el estado de los datos (inmutabilidad).

* **Enfoque:** Utilizar funciones puras donde la misma entrada siempre produce la misma salida, sin efectos secundarios.
* **Lenguajes típicos:** Haskell, Elixir, Scala (y de uso frecuente en JavaScript/React moderno).
* **Ejemplo:** En lugar de modificar una lista existente, se crea una nueva lista aplicando una transformación a la original.

### 4. Programación Declarativa (El "Qué")
Se describe el resultado deseado, sin especificar explícitamente los pasos para lograrlo. La lógica interna de ejecución permanece oculta.

* **Enfoque:** Prioriza la lógica sobre el control de flujo.
* **Lenguajes típicos:** [[SQL]] (Base de datos), [[HTML]]/CSS.
* **Ejemplo ([[SQL]]):**
    ```sql
    SELECT nombre FROM usuarios WHERE edad > 18;
    ```
    *(Se indica qué datos se requieren, no cómo recorrer la base de datos para hallarlos).*

---

## 🆚 Comparación Visual Rápida

Supóngase que se desea filtrar los números pares de una lista `[1, 2, 3, 4]`.

**Estilo Imperativo (Paso a paso):**
```python
numeros = [1, 2, 3, 4]
pares = []
for n in numeros:
    if n % 2 == 0:
        pares.append(n)
# Resultado: la lista 'pares' ahora contiene los datos

```

Estilo Funcional / Declarativo (Resultado directo):

```python
numeros = [1, 2, 3, 4]
pares = filter(lambda n: n % 2 == 0, numeros)
# Se define QUÉ se quiere (filtrar pares), no cómo iterar.
```
