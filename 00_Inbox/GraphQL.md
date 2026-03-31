---
status: final
tags:
  - graphql
  - api
  - frontend
  - backend
  - query-language
created: 2026-03-31
---
# 🕸️ [[GraphQL]]

**[[GraphQL]]** es un lenguaje de consultas (*Query Language*) para **[[API|APIs]]** y un tiempo de ejecución (*runtime*) para completar esas consultas con tus datos existentes. Fue desarrollado por Facebook en 2012 y liberado como código abierto en 2015.

A diferencia de **[[REST]]**, donde los recursos están divididos en múltiples URLs, **[[GraphQL]]** permite a los clientes definir exactamente qué estructura de datos necesitan y el servidor devuelve solo eso.

---
## 🎯 ¿Para qué sirve?

Su propósito principal es hacer que la comunicación entre el **[[Frontend]]** y el **[[Backend]]** sea más eficiente y flexible. Aquí se detallan sus funciones clave:

### 1. Evitar el Over-fetching y Under-fetching
Este es el mayor problema que resuelve:
* **Over-fetching:** Cuando el servidor envía más datos de los que necesitas (ej. pides un usuario y llega su dirección, historial y bio, cuando solo querías el nombre).
* **Under-fetching:** Cuando un endpoint no da suficiente información y se deben realizar múltiples llamadas a diferentes URLs para completar una vista.

### 2. Un solo Punto de Entrada (Endpoint)
En **[[REST]]** se suele tener `/users`, `/posts`, `/comments`. En **[[GraphQL]]**, generalmente existe un único endpoint (normalmente `/graphql`). Se envía una consulta describiendo lo que se desea de diferentes entidades y el servidor lo resuelve en una sola respuesta.

### 3. Tipado Fuerte y Autodocumentación
**[[GraphQL]]** utiliza un sistema de tipos para definir qué es posible en la **[[API]]**:
* Se conoce exactamente qué campos existen y de qué tipo son (String, Int, Boolean, etc.).
* Herramientas como **GraphiQL** o **Apollo Studio** permiten explorar la **[[API]]** y probar consultas con autocompletado de forma nativa.

---
## 🏛️ Conceptos fundamentales

Para entender cómo funciona en la práctica, se deben conocer estos tres pilares:

* **Schema (Esquema):** Es el contrato entre el cliente y el servidor. Define qué datos se pueden consultar y qué relaciones tienen.
* **Queries (Consultas):** Son las peticiones de lectura. Es el equivalente al `GET` en **[[REST]]**. Se escribe un **[[JSON]]**-ish indicando los campos deseados.
* **Mutations (Mutaciones):** Son las peticiones de escritura (crear, actualizar, eliminar). Equivalente a `POST`, `PUT` o `DELETE`.

---
## 📝 Ejemplo rápido

Si se deseara obtener el nombre de un usuario y los títulos de sus últimos 2 posts, la consulta se vería así:
```graphql
query {
  user(id: "123") {
    name
    posts(limit: 2) {
      title
    }
  }
}
```

El servidor respondería exactamente con esa estructura en **[[JSON]]**:
```json
{
  "data": {
    "user": {
      "name": "Mateo",
      "posts": [
        { "title": "Aprendiendo GraphQL" },
        { "title": "Backend vs Frontend" }
      ]
    }
  }
}
```

---

## 🚀 ¿Cuándo deberías usarlo?

- Cuando tienes aplicaciones móviles donde el ahorro de datos y la reducción de latencia son críticos.
- Cuando tu **[[Frontend]]** es muy dinámico y los requisitos de datos cambian frecuentemente.
- Si tienes un sistema de **[[Microservicios]]** y quieres una capa intermedia (_Gateway_) que unifique la información para el cliente.