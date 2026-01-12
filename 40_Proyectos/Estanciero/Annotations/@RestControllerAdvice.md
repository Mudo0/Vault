---
status: borrador
tags:
  - java
  - spring-boot
  - errores
  - backend
  - api
  - mvc
created: 2026-01-11
---
# 🛡️ @ControllerAdvice vs @RestControllerAdvice

En el manejo de errores en **[[Spring Boot]]**, la diferencia principal entre estas anotaciones radica en el tipo de respuesta que devuelven por defecto.

* **`@ControllerAdvice`:** Diseñado para aplicaciones **[[MVC]]** tradicionales (retorno de vistas **[[HTML]]**).
* **`@RestControllerAdvice`:** Diseñado para **[[API|APIs]]** **[[REST]]** (retorno de datos **[[JSON]]** o **[[XML]]**).

---

## 1. 🎭 @ControllerAdvice (Enfoque Clásico)

Es la anotación base utilizada para interceptar excepciones en toda la aplicación.

* **Comportamiento por defecto:** Los métodos dentro de esta clase asumen que se devolverá el nombre de una vista (por ejemplo, una página **[[HTML]]** usando **[[Thymeleaf]]** o **[[JSP]]**).
* **Para devolver [[JSON]]:** Si se utiliza esta anotación y se requiere devolver **[[JSON]]**, es obligatorio agregar la anotación `@ResponseBody` sobre cada método (o sobre la clase).

---

## 2. 🤖 @RestControllerAdvice (Enfoque Moderno para APIs)

Es una anotación de conveniencia que combina dos elementos:

$$@RestControllerAdvice = @ControllerAdvice + @ResponseBody$$

* **Comportamiento por defecto:** Los métodos asumen automáticamente que el valor de retorno debe serializarse directamente en el cuerpo de la respuesta **[[HTTP]]** (generalmente como **[[JSON]]**).
* **Ventaja:** Evita la necesidad de escribir `@ResponseBody` en cada método manejador de excepciones.

---

## 🆚 Tabla Comparativa

| Característica               | @ControllerAdvice                          | @RestControllerAdvice                            |
| :--------------------------- | :----------------------------------------- | :----------------------------------------------- |
| **Uso principal**            | Aplicaciones Web **[[MVC]]** (Vistas)      | [[API]] [[REST]]ful (**[[JSON]]**/**[[XML]]**)   |
| **Retorno por defecto**      | Nombre de Vista (`String` -> **[[HTML]]**) | Objeto **[[Java]]** (serializado a **[[JSON]]**) |
| **Anotación interna**        | `@Component`                               | `@ControllerAdvice` + `@ResponseBody`            |
| **Necesita `@ResponseBody`** | Sí, para devolver datos/**[[JSON]]**       | No, lo incluye implícitamente                    |

---

## 👨‍💻 Ejemplos en Código

### Caso A: Usando `@RestControllerAdvice` (Ideal para APIs)
Escenario común para backends de React, Angular o aplicaciones móviles.

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UsuarioNoEncontradoException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ErrorDTO handleUserNotFound(UsuarioNoEncontradoException ex) {
        // Al usar RestControllerAdvice, este objeto se convierte 
        // automáticamente a JSON
        return new ErrorDTO(404, ex.getMessage());
    }
}
// Resultado (JSON): {"codigo": 404, "mensaje": "Usuario no encontrado"}
```

### Caso B: Usando `@ControllerAdvice` (Ideal para Vistas)

Escenario utilizado si la aplicación sirve el **[[HTML]]** directamente (Monolito clásico).

```java
@ControllerAdvice
public class MvcExceptionHandler {

    @ExceptionHandler(Exception.class)
    public String handleException(Model model, Exception ex) {
        model.addAttribute("error", ex.getMessage());
        // Esto busca un archivo llamado "error-page.html"
        return "error-page"; 
    }
}
// Resultado: Renderiza la plantilla error-page.html.
```

---

## ✅ Guía de Selección

### Usar `@RestControllerAdvice` si:

- Se está desarrollando una **[[API]]** **[[REST]]**.
- El frontend espera recibir errores en formato **[[JSON]]** para mostrarlos en alertas o modales.
- Se busca un código más limpio sin necesidad de renderizar **[[HTML]]** desde el servidor.

### Usar `@ControllerAdvice` si:

- La aplicación utiliza **[[Thymeleaf]]**, **[[JSP]]** o Freemarker.
- Se desea redirigir al usuario a una página de error visual (ej. página 404 personalizada con diseño).

> **Nota:** Es posible usar `@ControllerAdvice` para **[[API|APIs]]** agregando `@ResponseBody` manualmente, aunque se considera una práctica redundante.