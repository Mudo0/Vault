---
status: borrador
tags:
  - csharp
  - dotnet
  - sintaxis
  - clean-code
created: 2025-12-12
---
# 🧩 Pattern Matching en [[C SHARP]]

El **Pattern Matching** (coincidencia de patrones) en [[C SHARP]] es una característica que permite evaluar una expresión para determinar si posee una cierta "forma" y, de ser así, extraer información de ella.

Se puede conceptualizar como una estructura condicional (`if` o `switch`) avanzada: no solo comprueba si una variable es igual a un valor, sino que permite verificar su tipo, propiedades y valores internos en una sola línea y de manera segura.

---

## 1. 🧐 Análisis de Caso: Property + Relational Pattern

Se analiza el siguiente fragmento de código:

```csharp
if (errors is { Count: > 0 }) 
{ 
    return errors; 
}
```

Esto constituye un **Property Pattern** (Patrón de Propiedades) combinado con un **Relational Pattern** (Patrón Relacional).

### Desglose paso a paso

- `errors`: Objeto evaluado (ej. `List<String>`, `Dictionary` o colección de una [[API]]).
- `is`: Operador de coincidencia. Pregunta si el objeto cumple con el esquema.
- `{ ... }`: Indica a C# que inspeccione las propiedades del objeto.
- `Count`: Busca la propiedad llamada "Count" dentro de `errors`.
- `: > 0`: Evalúa si el valor de dicha propiedad es mayor que cero.

### Comparativa de Seguridad

La ventaja principal radica en la seguridad y concisión frente a métodos antiguos:

- **Forma antigua (Peligrosa):**

    ```csharp
    // Si 'errors' es null, lanza NullReferenceException 💥
    if (errors.Count > 0) { ... }
    ```

- **Forma antigua (Segura pero extensa):**

    ```csharp
    // Requiere validación explícita de null
    if (errors != null && errors.Count > 0) { ... }
    ```
    
- **Con Pattern Matching (Recomendada):**
    
    ```csharp
    // ✅ SEGURO y CONCISO
    // Si 'errors' es null, la expresión devuelve 'false' sin excepciones.
    if (errors is { Count: > 0 }) { ... }
    ```

> **Resumen:** La instrucción indica: "Si la colección no es nula Y posee más de 0 elementos, se ejecuta el bloque".

---

## 2. 🛠️ Tipos de Pattern Matching en [[ASP.NET]]

En el desarrollo moderno con [[(.NET)]] (versiones recientes), se utilizan frecuentemente los siguientes patrones:

### A. Declaration Pattern (Comprobar y asignar)

Resulta útil en controladores de [[API]] al recibir un `object` o interfaz.

```csharp
public IActionResult Procesar(object datos)
{
    // Verifica si es string Y crea la variable 'texto' en un solo paso
    if (datos is string texto)
    {
        return Ok($"Es un texto de largo: {texto.Length}");
    }
    return BadRequest("No es texto");
}
```

### B. Logical Patterns (`and`, `or`, `not`)

Permite escribir lógica compleja de forma legible.

```csharp
int edad = 25;

// Verifica si la edad está en un rango
if (edad is >= 18 and < 65) 
{
    Console.WriteLine("Es adulto en edad laboral");
}

// Verifica nulos de forma elegante (estándar en C# moderno)
if (usuario is not null) 
{ 
    // ... 
}
```

### C. Switch Expressions

En [[ASP.NET]], reemplaza a las sentencias `switch` tradicionales. Es muy utilizado para mapear respuestas o estados.

```csharp
var mensaje = estadoPedido switch
{
    Estado.Pendiente => "Estamos procesando tu pago",
    Estado.Enviado   => "Tu paquete está en camino",
    Estado.Entregado => "Disfruta tu compra",
    _                => "Estado desconocido" // _ actúa como 'default'
};
```

### D. Positional Patterns (Para Records)

Si se utilizan `records` (común en Clean Architecture para DTOs), se puede realizar matching por la posición de los valores.

```csharp
public record Coordenada(int X, int Y);

var punto = new Coordenada(0, 5);
var descripcion = punto switch
{
    (0, 0) => "Origen",
    (0, _) => "En el eje Y", // _ indica "ignorar este valor"
    (_, 0) => "En el eje X",
    _      => "En algún lugar"
};
```

---

## ✅ Resumen

El uso de Pattern Matching en [[C SHARP]] favorece un código:

1. **Más expresivo:** Facilita la lectura (ej. `is not null`, `is > 0`).
2. **Más seguro:** Evita `NullReferenceException` automáticamente en la mayoría de los escenarios.
3. **Más conciso:** Reduce la cantidad de líneas necesarias para validar estructuras de datos complejas.