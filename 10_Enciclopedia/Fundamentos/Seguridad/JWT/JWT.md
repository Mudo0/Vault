---
status: borrador
tags:
  - jwt
  - seguridad
  - backend
  - api
  - arquitectura
created: 2026-03-02
---
# 🎟️ ¿Qué es un [[JWT]]?

Un **JSON Web Token ([[JWT]])** es un estándar abierto (RFC 7519) que define una forma compacta y autónoma de transmitir información de forma segura entre dos partes (como un cliente y un servidor) mediante un objeto **[[JSON]]**. Esta información puede ser verificada y validada porque está firmada digitalmente.

---

## 🧩 Estructura: Las Tres Partes

Un token **[[JWT]]** en su forma compacta consiste en tres cadenas de texto separadas por puntos (`.`), adoptando la siguiente estructura: `xxxxx.yyyyy.zzzzz`.

Cada sección cumple un propósito específico:

### 1. Header (Encabezado)
Normalmente consta de dos partes: el tipo de token (JWT) y el algoritmo de firma utilizado (ej. HMAC SHA256 o RSA). Este **[[JSON]]** se codifica en Base64Url para formar la primera parte del token.

### 2. Payload (Carga útil)
Contiene los *claims* (afirmaciones). Los *claims* son declaraciones sobre una entidad (generalmente, el usuario) y datos adicionales (como su ID, rol o fecha de expiración). Este **[[JSON]]** también se codifica en Base64Url para formar la segunda parte.
> **⚠️ Nota de Seguridad:** Aunque esta información está protegida contra modificaciones gracias a la firma, **no está encriptada**. Cualquiera puede decodificar el Payload, por lo que nunca se debe incluir información confidencial (como contraseñas).

### 3. Signature (Firma)
Para generar la firma, el servidor toma el Header codificado, el Payload codificado, un secreto (una clave que solo el servidor conoce) y el algoritmo especificado. La firma garantiza que el mensaje no fue alterado en tránsito. Si el Payload es modificado, la firma matemática se rompe y el servidor rechaza el token.

---
## 🛡️ Autenticación vs. Autorización

Es común confundir estos términos, pero representan etapas distintas en la seguridad. **[[JWT]]** se utiliza principalmente en la etapa de autorización.

| Concepto | ¿Qué pregunta responde? | Ejemplo Práctico |
| :--- | :--- | :--- |
| **Autenticación** | ¿Quién eres? | Ingresar correo y contraseña en un login para demostrar identidad. |
| **Autorización** | ¿Qué tienes permitido hacer? | Verificar si el usuario logueado tiene permisos de "Administrador" o solo de "Lector". |

**El flujo con [[JWT]]:** Tras una autenticación exitosa (credenciales correctas), el servidor devuelve un **[[JWT]]**. En las peticiones subsecuentes, el cliente envía ese token para autorizar el acceso a rutas o recursos protegidos.

---

## ☁️ ¿Por qué [[JWT]] es Stateless (Sin Estado)?

Se define a **[[JWT]]** como *stateless* porque libera al servidor de la necesidad de almacenar un registro de las sesiones activas en su base de datos o memoria.

* **El enfoque tradicional (con estado):** El servidor guarda un ID de sesión en memoria y entrega una cookie al cliente. En cada petición, el servidor debe consultar su base de datos para relacionar el ID con el usuario.
* **El enfoque [[JWT]] (sin estado):**


1.  **Es autocontenido:** Toda la información necesaria para identificar al usuario y sus roles viaja dentro del propio token (en el Payload).
2.  **Validación matemática:** Al recibir el token, el servidor no consulta ninguna base de datos. Utiliza su "clave secreta" para verificar la firma. Si es válida y no ha expirado, el servidor confía en la identidad del usuario y concede el acceso.

**Ventaja principal:** Facilita enormemente la escalabilidad horizontal. Cualquier servidor que posea la clave secreta puede validar el token, eliminando la dependencia de una base de datos centralizada para compartir sesiones.