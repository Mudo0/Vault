---
status: borrador
tags:
  - csharp
  - dotnet
  - jwt
  - seguridad
  - backend
  - api
created: 2026-02-28
---
# 🔐 Conceptos Clave de [[JWT]]: SecretKey, Issuer y Audience

Para comprender el funcionamiento de un **[[JWT]]** (JSON Web Token), resulta útil la analogía de una "entrada VIP" para un evento exclusivo. Tras un inicio de sesión exitoso (validación de credenciales), el servidor emite esta "entrada" (el Token).

Para evitar la falsificación o el uso indebido de este token, el servidor implementa medidas de seguridad criptográficas. Aquí es donde intervienen tres conceptos fundamentales:

---
## 1. 🔑 SecretKey (La Clave Secreta)

Es la medida de seguridad más crítica. Funciona como un sello holográfico irrompible o una firma digital en el token.

* **¿Para qué sirve?** Se utiliza para firmar criptográficamente el token. Cuando el cliente envía el **[[JWT]]** en una petición, el servidor emplea esta misma clave secreta para verificar su autenticidad.
* **¿Por qué es crucial?** Si un usuario malintencionado decodifica su token y altera sus datos (ej. modificando su ID o asignándose permisos de "Admin"), la firma matemática se rompe. Al recibir el token, el servidor recalcula la firma con la `SecretKey`. Si la firma resultante no coincide con el contenido, el token es rechazado instantáneamente por haber sido alterado.
* **⚠️ Regla de oro:** ¡NUNCA debe salir del backend! Si la `SecretKey` es comprometida, un atacante puede fabricar tokens válidos con cualquier nivel de permisos.

---
## 2. 🏢 Issuer (El Emisor)

Representa a la entidad, empresa o sistema que generó el token.

* **¿Para qué sirve?** Indica el origen del token (ej. `ChatRealtimeApp`).
* **¿Por qué se usa?** En ecosistemas grandes con múltiples proveedores de identidad (el propio servidor, Google, Microsoft, etc.), la **[[API]]** lee el `Issuer` para identificar qué sistema lo generó. Permite al servidor validar: *"Este token fue generado por un servidor de login de confianza"*. Se rechazarán tokens válidos pero provenientes de emisores desconocidos.

---
## 3. 🎯 Audience (La Audiencia)

Define el destinatario final que tiene permitido aceptar y procesar el token.

* **¿Para qué sirve?** Indica en qué sistema es válido el token (ej. `ChatRealtimeUsers`).
* **¿Por qué se usa?** Previene que un token emitido para una aplicación sea utilizado en otra distinta. Si una empresa posee una "App de Chat" y una "App de Finanzas" que comparten el mismo servidor de login (mismo `Issuer` y `SecretKey`), validar la `Audience` evita que un token generado para chatear conceda acceso a la **[[API]]** de finanzas.

---
## 📝 Resumen de Validación

* **SecretKey:** Evita la falsificación o alteración de los datos del token.
* **Issuer:** Asegura que el token fue creado por la fuente esperada.
* **Audience:** Asegura que el token se está utilizando en el sistema para el cual fue emitido.

> **Nota de Implementación:** Al configurar el bloque `TokenValidationParameters` en la clase `Program.cs` de **[[ASP.NET]]**, se instruye al framework para denegar el acceso si la firma es inválida, si el emisor difiere del esperado, o si la audiencia no corresponde a la aplicación actual.