---
status: borrador
tags:
  - angular
  - frontend
  - http
  - middleware
  - jwt
  - arquitectura
created: 2026-03-17
---
# 🛑 HTTP Interceptors en [[Angular]]

Para establecer un paralelismo directo con el backend (como en **[[(.NET)]]** o **[[Java]]**), la forma más sencilla de comprender un interceptor en el frontend es conceptualizarlo como un *[[middleware]]* o un filtro de peticiones.

Un interceptor es un bloque de código que se sitúa entre la aplicación cliente (**[[Angular]]**) y el servidor backend. Su función principal es "atrapar" o interceptar las peticiones **[[HTTP]]** salientes antes de que viajen a la red, y las respuestas **[[HTTP]]** entrantes antes de que alcancen los componentes o servicios que las solicitaron.

Esta arquitectura es sumamente útil porque permite modificar, registrar o cancelar peticiones y respuestas de manera global y centralizada, eliminando la duplicación de código en cada servicio que realice una llamada **[[HTTP]]**.

---
## 🎯 Casos de Uso Principales

A continuación se detallan las implementaciones más comunes en el desarrollo:

### 1. Inyección de Tokens de Autenticación ([[JWT]])
En lugar de agregar manualmente el encabezado `Authorization: Bearer <token>` en cada una de las llamadas a una API en **[[C#]]** o **[[Java]]**, se crea un interceptor que clona la petición saliente, inyecta el token si existe, y permite que continúe su flujo.

```typescript
// Ejemplo de un Interceptor Funcional en Angular (versiones modernas)
import { HttpInterceptorFn } from '@angular/common/http';

export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const token = localStorage.getItem('jwt_token');

  if (token) {
    // Las peticiones son inmutables, se requiere clonarlas para modificarlas
    const clonedRequest = req.clone({
      setHeaders: {
        Authorization: `Bearer ${token}`
      }
    });
    return next(clonedRequest); // Pasa la petición modificada
  }

  return next(req); // Pasa la petición original si no hay token
};
```

## 2. Manejo Global de Errores

Permite interceptar las respuestas provenientes del servidor y actuar en consecuencia antes de que la excepción afecte al usuario.

- **Error 401 Unauthorized:** El interceptor puede redirigir automáticamente a la pantalla de Login y limpiar la sesión local.
- **Error 500 Internal Server Error:** Se puede disparar una alerta genérica o notificación (_toast_) indicando "Error de conexión con el servidor".
    

## 3. Mostrar un "Loading Spinner" Global

Al iniciar una petición, se puede indicar a un servicio de estado que active una variable `isLoading = true` (mostrando un indicador de carga en la **[[UI]]**). Utilizando operadores de **[[RxJS]]** como `finalize`, se puede establecer `isLoading = false` en el interceptor cuando la petición concluya, ya sea con éxito o con error.

## 4. Agregar Cabeceras Estándar o Transformar Datos

Si el backend requiere consistentemente ciertas cabeceras (por ejemplo, `Accept: application/json` o un `Tenant-ID` para arquitecturas _multi-tenant_), el interceptor es el lugar ideal para centralizarlo. También se emplea frecuentemente para formatear fechas provenientes del servidor antes de su entrega a los componentes.
