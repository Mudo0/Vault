---
status: borrador
tags:
  - csharp
  - dotnet
  - cqrs
  - mediatr
  - patrones-diseño
  - arquitectura
created: 2026-03-02
---
# 🧅 Pipeline Behaviour y Handlers ([[CQRS]] / [[MediatR]])

En el desarrollo de software, específicamente al implementar patrones como **[[CQRS]]** (Command Query Responsibility Segregation) o al utilizar librerías como **[[MediatR]]** en **[[(.NET)]]**, un *Pipeline Behaviour* actúa como un intermediario o **[[Middleware]]** que envuelve la ejecución de una tarea.

Se puede conceptualizar utilizando la analogía de una cebolla: el núcleo representa la lógica de negocio, mientras que las capas exteriores son los *behaviours* que inspeccionan, modifican o detienen la petición antes de que alcance el centro.

---
## 1. ⚙️ ¿Qué es un Pipeline Behaviour?

Es un patrón que permite implementar **[[Cross-Cutting Concerns]]** (aspectos transversales). En lugar de duplicar código en múltiples áreas de la aplicación, la lógica genérica se escribe una sola vez en un "comportamiento" del *pipeline*.

**Ejemplos comunes de implementación:**
* **Validación:** Comprobar la integridad y corrección de los datos antes de procesarlos.
* **Logging:** Registrar automáticamente el inicio y fin de una operación.
* **Caching:** Devolver un resultado almacenado previamente sin necesidad de llegar al *handler*.
* **Manejo de errores:** Capturar excepciones de forma global y estandarizada.

---
## 2. 🤝 Relación con los Handlers

La relación entre ambos componentes se basa en jerarquía y flujo.

* **El Handler:** Es el destino final. Contiene la lógica de negocio específica para una acción (ej. `CrearUsuarioHandler`). Ignora el contexto exterior; su única responsabilidad es recibir una orden y ejecutarla.
* **El Behaviour:** Funciona como el "escolta" del *Handler*. El mensaje (*Command* o *Query*) debe atravesar obligatoriamente el *pipeline* de *behaviours* antes de ser recibido por el *Handler*.

---
## 3. 🌊 Flujo de Ejecución

El ciclo de vida de una petición sigue una secuencia estricta:

1.  **Request:** Se envía un comando (ej. "Registrar Producto").
2.  **Pipeline Step 1 (Logging):** Se registra el evento (ej. "Iniciando registro de producto").
3.  **Pipeline Step 2 (Validación):** Se verifican las reglas de negocio (ej. "Precio > 0"). Si la validación falla, el flujo se interrumpe en este punto.
4.  **Handler:** Si las validaciones previas son exitosas, el *Handler* ejecuta la acción principal (ej. *insert* en la base de datos).
5.  **Respuesta:** El resultado retorna atravesando nuevamente los *behaviours* (hacia afuera), permitiendo registrar tiempos de ejecución o transformar la respuesta final.

---
## 🆚 Comparativa Rápida

| Característica | Pipeline Behaviour | Handler |
| :--- | :--- | :--- |
| **Propósito** | Lógica genérica y transversal (Seguridad, Logs, Caché). | Lógica de negocio específica e individual. |
| **Reutilización** | Alta (se aplica a múltiples comandos o *queries*). | Baja (existe uno por cada acción específica). |
| **Orden de ejecución** | Se ejecutan en una secuencia definida antes y después. | Es el punto final y central de la secuencia. |

> **💡 Ventaja Arquitectónica:** La principal virtud de este sistema es que mantiene al *Handler* completamente "limpio" y enfocado. No requiere lidiar con validaciones de campos o apertura de conexiones; se limita exclusivamente a su responsabilidad principal.