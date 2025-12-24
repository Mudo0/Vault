---
status: borrador
tags:
  - docker
  - devops
  - navegacion
  - moc
  - indice
created: 2025-12-23
---
# 🐳 Hub Docker
> Plataforma de containerización para desarrollo y despliegue.

## 🧠 Teoría y Fundamentos
*Conceptos de arquitectura y virtualización ligera.*

### Core
- [[10_Enciclopedia/Entornos/DevOps/Docker/01_Definición|Definición]] y [[Arquitectura|Arquitectura]]
- [[Contenedor|Imagen vs Contenedor]] (Diferencia clave)
- [[Docker Daemon]]
- [[Volúmenes]] (Persistencia de datos)
- [[Redes en Docker]] (Bridge, Host, Overlay)

### Conceptos Relacionados
- [[Microservicios]]
- [[Virtualización vs Containerización]]

---

## 🛠️ Recetario (Cómo se hace...)
*Comandos, configuración de entornos y scripts.*

### ⚙️ Configuración e Instalación
- [[Instalar Docker en Linux]] (Ubuntu/Debian)
- [[Docker Desktop]] (Configuración en Windows)
- [[Post-installation steps]] (Permisos de usuario sin sudo)

### 🧱 Snippets y Comandos
- **Gestión de vida:** [[Comandos Básicos Docker]] (run, stop, ps, rm)
- **Limpieza:** [[Docker Prune]] (Eliminar imágenes y contenedores huerfanos)
- **Orquestación local:** [[Docker Compose]] (`docker-compose.yaml`)
- **Dockerfiles:** [[Crear un Dockerfile para .NET]]

---
## 🔌 Integraciones
*Cómo implementar Docker en mis desarrollos.*
- [[Dockerizar API .NET]]
- [[Dockerizar Frontend Angular]]