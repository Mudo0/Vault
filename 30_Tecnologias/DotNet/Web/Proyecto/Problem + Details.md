
# Patrón Problem Details (RFC 7807) en [[ASP.NET]] Core

El patrón estándar para devolver errores en [[API|APIs]] [[HTTP]], conocido como "Problem Details for HTTP APIs " (RFC 7807). En lugar de crear estructuras [[JSON]] personalizadas, se utiliza este formato universalmente aceptado.

  

## 1. Estructura del JSON (Type + Details)

El objeto [[JSON]] estándar contiene los siguientes campos:

• `type` ([[URI]]): Enlace a la documentación del tipo de error (ej. `[https://tools.ietf.org/html/rfc7231#section-6.5.1]`).
• `title` ([[String]]): Resumen corto y legible (ej. "Saldo Insuficiente").
• `status` ([[Int]]): Código de estado HTTP (ej. 400, 404, 500).
• `detail` ([[String]]): Explicación específica para la ocurrencia actual.
• `instance` ([[URI]]): Referencia única a la petición (útil para logs).

Ejemplo:

```json
{
  "type": "[enlace sospechoso eliminado]",
  "title": "Bad Request",
  "status": 400,
  "detail": "El formato del email no es válido.",
  "instance": "/api/usuarios/crear",
  "traceId": "00-98237..."
} 
```

  

## 2. Implementación en [[ASP.NET]] Core

### A. Forma Manual (En Controlador)
Usando el helper `Problem()`:

```csharp
[HttpPost("pagar")]
public IActionResult Pagar(decimal monto){

    if (monto <= 0){
        return Problem(
            detail: "El monto debe ser mayor a cero.",
            title: "Monto Inválido",
            statusCode: StatusCodes.Status400BadRequest
			        );}
    return Ok();
}
```

  

### B. Forma Automática (Validaciones)
[[ASP.NET]] Core usa Problem Details por defecto para errores de `ModelState` en controladores con `[ApiController]`. Para habilitarlo explícitamente en `[Program.cs](http://program.cs)`:

  

```csharp
builder.Services.AddControllers();
builder.Services.AddProblemDetails();
```

  

### C. Forma Global (IExceptionHandler) - Recomendada

Intercepta excepciones no controladas de forma limpia (disponible desde .NET 8).
Definición del Handler:

  ```csharp

public class GlobalExceptionHandler : IExceptionHandler
{
    // ... inyección de logger ...
    public async ValueTask<bool> TryHandleAsync(HttpContext httpContext, Exception exception, CancellationToken cancellationToken){
        var problemDetails = new ProblemDetails{
            Status = StatusCodes.Status500InternalServerError,
            Title = "Error Interno del Servidor",
            Detail = "Ocurrió un problema procesando tu solicitud."
	        };

        httpContext.Response.StatusCode = problemDetails.Status.Value;
        await httpContext.Response.WriteAsJsonAsync(problemDetails, cancellationToken);
        return true;
    }
}
```

Registro en [[Program.cs]]:
```csharp
builder.Services.AddExceptionHandler<GlobalExceptionHandler>();

builder.Services.AddProblemDetails();

var app = builder.Build();

app.UseExceptionHandler();

app.MapControllers();
app.Run();
```


## Ventajas

1. Estandarización: Facilita el consumo por parte del frontend.
2. Claridad: Separa el tipo de error de los detalles específicos.
3. Extensibilidad: Permite agregar campos personalizados sin romper el estándar.