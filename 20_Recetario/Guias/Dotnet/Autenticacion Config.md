---
status: borrador
tags:
  - csharp
  - dotnet
  - jwt
  - seguridad
  - backend
  - aspnet-core
created: 2026-03-02
---
# 🛡️ Configuración de Autenticación [[SecretKey, Issuer y Audience]] en [[(.NET)]]

Configurar la seguridad en **[[(.NET)]]** puede resultar confuso, pero las líneas de configuración iniciales actúan como el "director de orquesta" del sistema. Básicamente, instruyen a la aplicación: *"A partir de este momento, la identificación de usuarios se realizará mediante [[SecretKey, Issuer y Audience]]"*.

A continuación se desglosa la función exacta de cada componente en el contenedor de dependencias: [[Program.cs Config]]

---

## 1. ⚙️ AddAuthentication

Esta función registra los servicios base necesarios para que el sistema de autenticación de **[[ASP.NET]]** opere. Sin esta instrucción, el framework omitirá por completo cualquier intento de verificar quién es el usuario.

---

## 2. 🔍 DefaultAuthenticateScheme

Esta línea instruye a la aplicación sobre **cómo verificar la identidad**.

Al asignarle el valor `JwtBearerDefaults.AuthenticationScheme`, el servidor comprende que, ante cada petición HTTP entrante, debe buscar un token en el encabezado `Authorization`.
* Si el token es encontrado y es válido, el servidor procede a crear la identidad del usuario en memoria (construyendo el objeto `ClaimsPrincipal`).

---
## 3. ⛔ DefaultChallengeScheme

Esta línea instruye a la aplicación sobre **qué acción tomar si el usuario no tiene permiso**.

El *"Challenge"* (Desafío) es la respuesta que emite el servidor cuando una petición intenta acceder a una ruta protegida (marcada con el atributo `[Authorize]`) sin estar autenticada.
* Al configurarlo específicamente para **[[SecretKey, Issuer y Audience]]**, el servidor responderá automáticamente con un código HTTP **401 Unauthorized**, indicándole al cliente (el frontend) que requiere enviar un token válido para acceder.

---
## 🏛️ ¿Por qué son estrictamente necesarias?

Se puede utilizar la analogía de un edificio equipado con múltiples tipos de cerraduras (JWT, Cookies, OAuth). Si no se define un método por defecto (*Default*), cuando una petición llega a la puerta, el sistema de seguridad de **[[ASP.NET]]** no sabrá qué tipo de credencial debe solicitar.

**Consecuencias de omitir estas configuraciones globales:**

1.  **Redundancia en el código:** Sería obligatorio especificar manualmente el esquema a utilizar en cada controlador o endpoint de la aplicación:
    `[Authorize(AuthenticationSchemes = JwtBearerDefaults.AuthenticationScheme)]`
2.  **Comportamiento erróneo de la API:** El sistema podría recurrir al comportamiento por defecto original (basado en Cookies), lo que provocaría que intente redirigir la petición a una página web de "Login" HTML (inexistente en una **[[API]]** REST), en lugar de devolver el error HTTP 401 que la aplicación cliente necesita procesar.