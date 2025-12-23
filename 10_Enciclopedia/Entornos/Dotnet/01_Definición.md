---
status: borrador
tags:
  - dotnet
  - conceptos
  - plataforma
  - ecosistema
created: 2025-12-23
---
# 🟣 ¿Qué es [[(.NET)]]?

**[[(.NET)]]** es una plataforma de desarrollo de **[[Código Abierto]]** y multiplataforma creada por Microsoft para construir aplicaciones modernas (Web, Móvil, Escritorio, Cloud, IA).

* **Naturaleza:** No constituye un lenguaje, sino el ecosistema/runtime. Los lenguajes principales son [[C SHARP|C#]] y F#.
* **Gestión de Memoria:** Utiliza un entorno de ejecución (CLR) que gestiona la memoria automáticamente (Garbage Collection), característica que le otorga mayor seguridad frente a lenguajes como C++.
* **Comunidad:** Una comunidad activa mantiene la plataforma junto con Microsoft.

---

## ⏳ Ecosistema [[(.NET)]] (Evolución)

La plataforma ha evolucionado en tres grandes etapas. Su comprensión resulta clave para evitar confusiones con documentación antigua.

### 🏛️ .NET Framework (El Legado)
Es la implementación original lanzada en 2002.
* **Limitación:** Funciona exclusivamente en Windows.
* **Estado:** En mantenimiento. No se recomienda para proyectos nuevos, aunque muchas empresas mantienen su uso.

### 🚀 .NET Core (La Revolución)
Lanzado en 2014. Fue reescrito desde cero para ser Multiplataforma (Windows, [[Linux]], macOS) y de alto rendimiento.
* Es de **[[Código Abierto]]** y se aloja en **[[GitHub]]**.
* Fue el precursor del [[(.NET)]] moderno.

### 🟣 [[(.NET)]] (Actualidad)
A partir de 2020 (con .NET 5), Microsoft eliminó la etiqueta "Core".
* Actualmente se denomina simplemente .NET (ej. .NET 8, .NET 9).
* Unifica las ventajas de Framework y Core en una sola plataforma universal.

### 📏 .NET Standard (La Especificación)
Es un conjunto formal de **[[API|APIs]]** comunes.
* **Propósito:** Permitía crear librerías compatibles tanto con el antiguo .NET Framework como con el moderno .NET Core.
* **Nota:** En las versiones modernas (.NET 6+), su uso ha disminuido debido a la unificación de la plataforma.

---

## 🛠️ Herramientas Clave

* **[[Visual Studio]] / VS Code:** Los entornos de desarrollo (IDEs) principales.
* **[[NuGet]]:** El gestor de paquetes oficial (utilizado para descargar librerías externas).
* **[[CLI]] (Command Line Interface):** Permite crear y compilar aplicaciones desde la terminal (ej. `dotnet new`, `dotnet build`).