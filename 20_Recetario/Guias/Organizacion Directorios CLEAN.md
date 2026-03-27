---
status: final
tags:
  - productividad
  - windows
  - wsl
  - dev-environment
  - buenas-practicas
created: 2026-03-26
---
## 🏗️ 1. Estrategia de Carpetas (Método de Aislamiento)

La regla fundamental es evitar el almacenamiento de archivos sueltos en la raíz del usuario (`C:\Users\Usuario` o `~`). Todo debe residir en un contenedor específico.

### Estructura sugerida para el Workspace:
Se recomienda centralizar el código en `C:\Users\Usuario\Workspace\` o `~/workspace/` (**WSL**), agrupando por ecosistemas:

* **`/dotnet`:** Proyectos en **[[C#]]**, **[[API|APIs]]**, SignalR y **[[(.NET)]]**.
* **`/java`:** Proyectos de **[[Java]]** y **[[Spring Boot]]** (ej. backend de juegos de mesa).
* **`/frontend`:** Proyectos de **[[Angular]]**.
* **`/infra`:** Archivos `docker-compose.yml`, configuraciones de contenedores de **[[Docker]]** y scripts para el servidor **[[Ubuntu]]**.

### Otras ubicaciones críticas:
* **`Knowledge/`:** Reservado exclusivamente para la bóveda de **[[Obsidian]]**.
* **`Downloads/`:** Se debe aplicar una política de vaciado semanal. Los archivos útiles se mueven a su destino final; el resto se elimina.



---

## 🐚 2. Optimización de la Terminal y "Dotfiles" en WSL

En entornos **Linux**, es común que el directorio *Home* (`~`) se sature con archivos de configuración ocultos (`.m2`, `.nuget`, `.ssh`, etc.).

### A. Adopción del estándar XDG
Este estándar dicta que las configuraciones deben residir en `~/.config`, el caché en `~/.cache` y los datos en `~/.local/share`. Se puede forzar este comportamiento agregando variables de entorno en el `.bashrc` o `.zshrc`:

```bash
export XDG_CONFIG_HOME="$HOME/.config"
export XDG_CACHE_HOME="$HOME/.cache"
export XDG_DATA_HOME="$HOME/.local/share"

# Ejemplo para herramientas de desarrollo:
export NPM_CONFIG_USERCONFIG="$XDG_CONFIG_HOME/npm/npmrc"
export NUGET_PACKAGES="$XDG_CACHE_HOME/NuGetPackages"
```

## B. Gestión de Dotfiles con GNU Stow

Se recomienda centralizar las configuraciones reales en una carpeta `~/dotfiles` y utilizar **GNU Stow** para generar enlaces simbólicos automáticos a sus destinos originales, manteniendo todo versionado y ordenado.

## C. Visualización Moderna

Sustituir el comando `ls` por herramientas como `eza` o `lsd`. Estos reemplazos modernos incluyen iconos, colores y formato en árbol, facilitando la lectura visual de los directorios.

---

## 📦 3. Gestores de Paquetes (Package Managers)

Para mantener el sistema libre de instaladores manuales y ejecutables dispersos, el uso de gestores de paquetes es vital.

| **Entorno**          | **Herramienta Recomendada**     | **Razón Principal**                                                                                                                                                                                                           |
| -------------------- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Windows (Dev)**    | **Scoop**                       | Instala todo en la carpeta del usuario. No ensucia el PATH global ni requiere permisos de admin. Ideal para **[[Java]]**, **[[(.NET)]]** SDKs, etc.                                                                           |
| **Windows (Gral)**   | **Winget**                      | Excelente para aplicaciones de uso diario (navegadores, herramientas de comunicación).                                                                                                                                        |
| **WSL ([[Ubuntu]])** | - apt<br>- homebrew<br>- docker | - Usa **APT** solo para lo básico del sistema.<br>-Usa **Homebrew** para utilidades de terminal.<br>- Levanta servicios pesados (Bases de datos, colas de mensajes) exclusivamente con **Docker**, nunca los instales en WSL. |

> **💡 Consejo Pro:** Para bases de datos o servicios temporales, utilizar **[[Docker]]**. Al finalizar el uso, se elimina el contenedor y el sistema permanece inmaculado.

---

## 🛠️ 4. Herramientas de Mantenimiento

- **WizTree (Windows):** Permite identificar visualmente qué carpetas ocupan más espacio (útil para detectar `node_modules` pesados o cachés antiguos).
- **ncdu (WSL):** Interfaz interactiva para la terminal que permite navegar y eliminar archivos pesados en el entorno **Linux**.
- **PowerToys (Windows):** Utilizar "PowerToys Run" (`Alt + Espacio`) para lanzar programas y buscar archivos, permitiendo mantener un escritorio completamente libre de accesos directos.    
