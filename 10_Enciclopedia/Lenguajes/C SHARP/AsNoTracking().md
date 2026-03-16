---
status: final
tags:
  - csharp
  - dotnet
  - entity-framework
  - backend
  - rendimiento
  - base-de-datos
created: 2026-03-03
---
# 🚀 Optimización de Consultas: .AsNoTracking() en [[Entity Framework]]

En el desarrollo de aplicaciones y APIs con **[[ASP.NET]]** y **[[(.NET)]]**, la optimización del acceso a datos es crucial. Un patrón estándar para mejorar el rendimiento en operaciones de solo lectura es el uso de `.AsNoTracking()`.

```csharp
public async Task<IEnumerable<User>> GetAllAsync()
{
    // Se añade .AsNoTracking() antes de materializar la lista
    return await _context.Users.AsNoTracking().ToListAsync();
}
```

---

## 🔍 ¿Por qué es necesario agregarlo?

## 1. El comportamiento por defecto (Tracking)

Por defecto, cuando **[[Entity Framework]]** recupera datos de la base, realiza un seguimiento (_tracking_) de esas entidades en memoria. Este mecanismo existe para detectar si se modifica alguna propiedad del objeto y, de ser así, generar el comando `UPDATE` correspondiente al invocar `_context.SaveChangesAsync()`.

Este proceso en segundo plano consume considerables recursos de memoria y tiempo de CPU.

## 2. El comportamiento optimizado (No-Tracking)

Dado que un _endpoint_ de lectura (como obtener una lista para mostrar 500 usuarios) tiene el propósito exclusivo de consultar y no de modificar, el seguimiento de cambios resulta innecesario.

Al añadir `.AsNoTracking()`, se instruye a **[[Entity Framework]]**: _"Recuperar los datos con la mayor rapidez posible y omitir su almacenamiento en el rastreador de cambios"_.

---
## 📈 Impacto en el Rendimiento

La omisión del _tracking_ aporta beneficios directos:

- **Menor consumo de memoria:** El sistema no necesita guardar copias del estado original de las entidades.
- **Mayor velocidad de ejecución:** Se evita el procesamiento adicional por parte del _Change Tracker_ interno.
- **Escalabilidad:** El rendimiento mejora significativamente, notándose un impacto mucho mayor a medida que el volumen de datos de la lista comienza a crecer.