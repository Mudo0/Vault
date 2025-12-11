---
status: final
tags:
  - conceptos
  - paradigmas
  - poo
created: 2025-12-10
---
# 📦 Programación Orientada a Objetos ([[P.O.O]])

La **Programación Orientada a Objetos** es un [[Paradigmas de Programación|paradigma]] que organiza el diseño de software en torno a datos u "objetos", en lugar de funciones y lógica. Se basa en el concepto de que el software debe modelar las entidades del mundo real y sus interacciones.

Este paradigma permite estructurar programas complejos de manera que sean más fáciles de mantener, escalar y reutilizar, ocultando la complejidad interna a través de la encapsulación. Lenguajes como [[C SHARP]], [[Java]] y [[C++]] son fundamentalmente orientados a objetos.

---

## 🗝️ Conceptos Clave (Clase vs Objeto)

Para comprender la [[P.O.O]] es fundamental distinguir entre **[[Clase]]** y **[[Objeto]]**:

* **La Clase (El Molde):** Es la definición abstracta. Es comparable al **plano de una casa** o un **molde para cortar galletas**. Define qué propiedades (atributos) y comportamientos (métodos) tendrá la entidad, pero no existe físicamente en la memoria ejecutada.
* **El Objeto (La Instancia):** Es la materialización de la clase. Siguiendo el ejemplo, representa **la casa construida** o **la galleta horneada**. Se pueden crear múltiples objetos diferentes (casas de distintos colores) utilizando la misma clase (el mismo plano).

---

## 🏛️ Los 4 Pilares de la P.O.O

Para que un lenguaje se considere orientado a objetos, debe implementar estos cuatro principios:

1. **Encapsulamiento:** Ocultación de los detalles internos para proteger la integridad de los datos (mediante el uso de modificadores como `private` o `public`).
2. **Abstracción:** Extracción de las características esenciales de un objeto, ignorando los detalles menos relevantes para el contexto actual.
3. **Herencia:** Capacidad de crear nuevas clases basadas en clases existentes, reutilizando su código.
4. **Polimorfismo:** Capacidad de que objetos de diferentes clases respondan al mismo mensaje o método de maneras distintas.