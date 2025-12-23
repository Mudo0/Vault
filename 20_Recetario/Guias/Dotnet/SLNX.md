---
status: final
tags:
  - dotnet
  - visual-studio
  - configuracion
  - arquitectura
created: 2025-12-16
---
# 📄 Formato de Solución [[SLNX|.slnx]]

El formato **.slnx** representa la modernización de los archivos de solución en el ecosistema Microsoft, siendo una funcionalidad muy esperada por los desarrolladores de **[[(.NET)]]**.

---

## 🧐 ¿Qué es .slnx?

Es el sucesor moderno, basado en [[XML]], del clásico archivo de solución `.sln`.

Históricamente, el archivo `.sln` no utilizaba un formato estándar (no era [[XML]] ni [[JSON]]), sino una estructura propia y rígida que apenas ha evolucionado en dos décadas. El `.slnx`, en cambio, adopta una estructura limpia y legible, similar a la apariencia de los archivos de proyecto modernizados (`.csproj`).

---

## 🚀 Ventajas Clave

Su propósito principal es simplificar la gestión de soluciones, especialmente en equipos de trabajo.

* **Legibilidad:** Al ser [[XML]] puro, se puede abrir con cualquier editor y comprender su contenido instantáneamente.
* **Git-Friendly (Cero Conflictos):** El `.sln` clásico generaba conflictos de fusión (*merge conflicts*) complejos debido al uso de GUIDs y su dependencia del orden de las líneas. El `.slnx` elimina la necesidad de GUIDs para los proyectos, facilitando la fusión en **[[Git]]**.
* **Concisión:** Reduce drásticamente el "ruido". Un archivo que anteriormente requería 50 líneas de configuración críptica puede reducirse a unas 10 líneas de [[XML]] claro.
* **Soporte de Rutas Relativas:** Maneja las rutas de los proyectos de manera más intuitiva.

---

## 🆚 Comparación Visual

**El viejo .sln (Difícil de leer):**
```sln
Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "MiApp", "MiApp\MiApp.csproj", "{A1B2C3D4-E5F6-...}"
EndProject
Global
    GlobalSection(SolutionConfigurationPlatforms) = preSolution
        Debug|Any CPU = Debug|Any CPU
    ...


```


**El nuevo .slnx (Limpio y claro):**

```XML
<Solution>
  <Folder Name="/Items de Solución/">
    <File Path=".editorconfig" />
  </Folder>
  <Project Path="MiApp\MiApp.csproj" />
  <Project Path="MiApp.Tests\MiApp.Tests.csproj" />
</Solution>
```

---

## 🛠️ Cómo implementarlo

Actualmente (en el ecosistema [[(.NET)]] 8/9 y VS 2022), esta funcionalidad se encuentra en estado _Preview_, por lo que debe habilitarse manualmente.

### Paso 0: Prerrequisitos

Se requiere **Visual Studio 2022** (versión 17.10 o superior recomendada).

### Paso 1: Habilitar la característica

1. Abrir Visual Studio.
2. Dirigirse a **Herramientas > Opciones**.
3. En el menú izquierdo, buscar **Entorno > Características de versión preliminar** (_Preview Features_).
4. Marcar la casilla: **"Use Solution File Persistence Model"** (o "Usar modelo de persistencia de archivos de solución").
5. Reiniciar Visual Studio.

### Escenario A: Crear un proyecto nuevo

Por defecto, Visual Studio continúa creando archivos `.sln`. El procedimiento actual consiste en crear la solución y posteriormente modificarla.

1. Crear el proyecto de forma habitual (_Archivo > Nuevo > Proyecto_).
2. En el Explorador de Soluciones, hacer clic derecho sobre el nombre de la solución (raíz del árbol).
3. Seleccionar **"Guardar solución como..."** (_Save Solution As..._).
4. En el tipo de archivo, seleccionar `.slnx`.
5. Al guardar, Visual Studio cambiará el contexto para utilizar el nuevo archivo.

### Escenario B: Migrar una solución existente

1. Asegurar la activación de la _Preview Feature_ (Paso 1).
2. Abrir la solución `.sln` actual.
3. Hacer clic derecho en la solución dentro del explorador y elegir **"Guardar solución como..."**.
4. Cambiar la extensión a `.slnx`.
5. **Importante:** Eliminar (o renombrar como respaldo) el archivo `.sln` antiguo.
6. Verificar el nuevo archivo con un editor de texto para asegurar la corrección de las rutas.

---

## ⚠️ Consideraciones de Uso

Dado que es una característica en _Preview_, el soporte en herramientas de CI/CD (como GitHub Actions, Azure DevOps) o en la **[[CLI]]** de dotnet puede no estar completamente maduro sin configuraciones adicionales.

> **Recomendación:** Se aconseja su uso en proyectos personales o pruebas de arquitectura para aprovechar la limpieza en el control de versiones. Para entornos corporativos grandes, se sugiere esperar al lanzamiento oficial para evitar inconvenientes en las tuberías de despliegue.