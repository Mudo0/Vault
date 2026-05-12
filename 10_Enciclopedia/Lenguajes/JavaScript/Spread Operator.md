---
status: final
tags:
  - javascript
  - frontend
  - es6
  - programacion
created: 2026-04-21
---

# 📑 Spread Operator (`...`)

El operador **`...`** se llama **Spread Operator** (operador de propagación) y su función es esparcir o expandir los elementos de un iterable (como un array) en lugares donde se esperan varios argumentos separados.

---

## 🛑 El Problema: Contenedor vs. Contenido

Para entender su funcionamiento, es necesario observar cómo procesa la información `Math.max()`
- **La Expectativa:** `Math.max()` fue diseñado para recibir una lista de números separados por comas: `Math.max(1, 2, 3)`.
- **La Realidad del Array:** Al crear un array `const arr = [1, 2, 3]`, se genera un único objeto que contiene esos números.
- **El Error:** Si se ejecuta `Math.max(arr)`, se le pasa un solo argumento (el objeto Array). El método intenta convertir ese objeto a número, falla y devuelve **NaN** (_Not a Number_).

---
## ✅ La Solución: El operador de propagación `...`

Al anteponer **`...`** al array, se le indica al motor de JavaScript que tome los elementos internos y los pase como argumentos individuales.

- **Código escrito:** `Math.max(...[1, 2, 3])`
- **Interpretación de JS:** `Math.max(1, 2, 3)`

### 🍬 Analogía para visualizarlo

Imagina que `Math.max` es una persona encargada de contar caramelos que solo puede contar los que están sueltos sobre una mesa.

- Si le entregas una **bolsa cerrada** (`[1, 2, 3]`), la persona no puede acceder a ellos y no puede contar.
- El operador **`...`** equivale a **abrir la bolsa y vaciar los caramelos** sobre la mesa. Ahora, la persona puede ver el 1, el 2 y el 3 individualmente e identificar el mayor.

---
## 🚀 Utilidad y Aplicaciones

Es una herramienta fundamental para manipular colecciones de forma elegante y legible, evitando métodos antiguos y complejos como `.concat()` o `.apply()`:

- **Combinar arrays:** `const nuevo = [...arr1, ...arr2];`
- **Copiar arrays:** `const copia = [...original];`
- **Agregar elementos:** `const lista = [0, ...arr, 4];`