---
status: final
tags:
  - dotnet
  - arquitectura
  - backend
  - buenas-practicas
created: 2025-12-12
---
# 🛡️ Manejo de Errores de Dominio con ErrorOr

La librería **ErrorOr** facilita la implementación del patrón Result en [[(.NET)]]. Permite manejar el flujo de control de manera explícita sin abusar de las excepciones (reservándolas para casos excepcionales), logrando un código más expresivo y limpio.

A continuación, se detalla la estructura para centralizar errores de dominio.

---

## 📦 Paso 1: Instalación

Si no se dispone del paquete, es necesario instalarlo mediante el CLI:

```bash
dotnet add package ErrorOr
```

---

## 🏗️ Paso 2: Definición Centralizada (`DomainErrors`)

La práctica recomendada consiste en crear una clase estática `DomainErrors` y, dentro de ella, clases estáticas anidadas para cada entidad (User, Product, Order, etc.). Esto genera una estructura organizada (ej. `DomainErrors.User.DuplicateEmail`).

Se utiliza `public static readonly Error` para definir los errores, asegurando inmutabilidad y rapidez en la instanciación.

C#

```csharp
using ErrorOr;

namespace MiProyecto.Domain.Common.Errors;

public static class DomainErrors
{
    // Agrupación de errores de Usuario
    public static class User
    {
        // Error tipo "Conflict" (409)
        public static readonly Error DuplicateEmail = Error.Conflict(
            code: "User.DuplicateEmail",
            description: "El correo electrónico ya está en uso.");

        // Error tipo "NotFound" (404)
        public static readonly Error NotFound = Error.NotFound(
            code: "User.NotFound",
            description: "El usuario con el ID especificado no existe.");

        // Error tipo "Validation" (400) - Reglas de negocio
        public static readonly Error InvalidPassword = Error.Validation(
            code: "User.InvalidPassword",
            description: "La contraseña no cumple con los requisitos de seguridad.");
        
        // Error tipo "Unexpected" (500)
        public static readonly Error DatabaseFailure = Error.Unexpected(
            code: "User.DatabaseFailure",
            description: "Error inesperado al acceder a los datos del usuario.");
    }
}
```

> **Nota:** El `code` debe ser único y legible por máquinas (útil para el frontend), mientras que `description` está destinado a la lectura humana.

---

## ⚙️ Paso 3: Implementación en la Capa de Aplicación

En el servicio o handler, en lugar de lanzar una excepción (`throw new Exception`), se retorna un `ErrorOr<User>`.

```csharp
using ErrorOr;
using MiProyecto.Domain.Common.Errors;
using MiProyecto.Domain.Entities;

public class UserService : IUserService
{
    private readonly IUserRepository _userRepository;

    public UserService(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }

    // El retorno es ErrorOr<User> (puede ser un Usuario O una lista de Errores)
    public async Task<ErrorOr<User>> Register(string email, string password)
    {
        // 1. Validar si el email ya existe
        if (await _userRepository.ExistsByEmailAsync(email))
        {
            // Se retorna el error específico definido en DomainErrors
            return DomainErrors.User.DuplicateEmail;
        }

        // 2. Validar fortaleza de contraseña
        if (password.Length < 8)
        {
            return DomainErrors.User.InvalidPassword;
        }

        // 3. Crear el usuario (Happy Path)
        var user = new User { Email = email, Password = password };
        await _userRepository.AddAsync(user);

        // Conversión implícita: se retorna el objeto directamente
        return user; 
    }
    
    public async Task<ErrorOr<User>> GetById(Guid id)
    {
        var user = await _userRepository.GetByIdAsync(id);

        if (user is null)
        {
            return DomainErrors.User.NotFound;
        }

        return user;
    }
}
```

---

## 🎮 Paso 4: Manejo en el Controlador ([[API]])

En la [[API]] (Controller o Minimal API), se decide la respuesta [[HTTP]] a devolver basándose en el resultado. `ErrorOr` proporciona el método `.Match` para este fin.

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase 
{
    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpPost("register")]
    public async Task<IActionResult> Register(RegisterRequest request)
    {
        ErrorOr<User> authResult = await _userService.Register(request.Email, request.Password);

        // Match recibe dos funciones: 
        // 1. Qué hacer si es éxito (value) -> 200 OK
        // 2. Qué hacer si es error (errors) -> Problem Details
        return authResult.Match(
            user => Ok(MapToDto(user)),             
            errors => Problem(errors)               
        );
    }

    // Método auxiliar para mapear errores a respuesta HTTP
    private IActionResult Problem(List<Error> errors)
    {
        var firstError = errors[0];

        var statusCode = firstError.Type switch
        {
            ErrorType.Conflict => StatusCodes.Status409Conflict,
            ErrorType.Validation => StatusCodes.Status400BadRequest,
            ErrorType.NotFound => StatusCodes.Status404NotFound,
            _ => StatusCodes.Status500InternalServerError
        };

        return Problem(statusCode: statusCode, title: firstError.Description);
    }
}
```

---

## ✅ Ventajas del Enfoque

- **Centralización:** La modificación de mensajes de error se realiza en un único lugar (`DomainErrors`).
- **Intellisense:** Al escribir `DomainErrors.User.`, el IDE sugiere todos los errores posibles, evitando "magic strings".
- **Semántica:** Diferencia claramente entre tipos de errores (ej. Validación vs. Conflicto).
- **Flujo Limpio:** La lógica de negocio se lee linealmente, sin bloques `try-catch` que oscurezcan la intención del código.