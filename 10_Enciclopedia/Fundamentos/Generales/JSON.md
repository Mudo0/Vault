---
status: final
tags:
  - conceptos
  - datos
  - web
created: 2025-12-10
---
# 📄 ¿Qué es [[JSON]]?

**[[JSON]]** (siglas de JavaScript Object Notation) es un formato de texto sencillo diseñado para el intercambio de datos.

Aunque su nombre hace referencia a JavaScript, es independiente del lenguaje. Esto significa que prácticamente cualquier lenguaje de programación moderno puede leer y crear archivos [[JSON]]. Se le considera el "idioma universal" o el "envase estándar" que utilizan las aplicaciones para transferir información de forma rápida y ordenada entre ellas.

---

## 🚀 Funciones Principales

Su función primordial es servir de puente para mover información entre un servidor (donde se alojan los datos) y un cliente (una página web o una aplicación móvil).

Se utiliza comúnmente para:

* **[[API|APIs]] y Servicios Web:** Cuando una aplicación muestra datos (como el clima), dicha información probablemente se transmitió desde el servidor en formato [[JSON]].
* **Archivos de Configuración:** Muchos programas almacenan sus preferencias (como temas o atajos) en este formato.
* **Bases de Datos NoSQL:** Bases de datos como MongoDB guardan la información en una estructura casi idéntica.

---
## 👁️ Estructura y Ejemplo
Es legible para los humanos y se organiza en pares de "clave": valor.
A continuación, un ejemplo de la representación de un usuario:

```json
{
  "nombre": "Juan Pérez",
  "edad": 28,
  "es_estudiante": false,
  "habilidades": ["Python", "HTML", "SQL"],
  "direccion": {
    "calle": "Av. Siempreviva",
    "numero": 742
  }
}

```

### Puntos clave:
- Se utilizan **llaves** `{ }` para contener objetos.
- Se utilizan **corchetes** `[ ]` para listas (arrays).
- Los textos se delimitan con **comillas** `" "`.