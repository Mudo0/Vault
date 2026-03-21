---
status: borrador
tags:
  - android
  - mobile
  - kotlin
  - moc
  - indice
created: 2026-03-21
---
# 📱 Hub Android
> Centro de comando para desarrollo de aplicaciones móviles nativas.

## 🧠 Teoría y Fundamentos
*Conceptos clave y arquitectura.*

### Core del Sistema Operativo
- [[10_Enciclopedia/Entornos/Android/01_Definición|Definición y Máquina Virtual (ART)]]
- [[Activity Lifecycle]] (El ciclo de vida de las pantallas)
- [[Context]] (Qué es y cuándo usar Application vs Activity context)
- [[Intents y Navigation]]

### Arquitectura (App Architecture)
- [[MVVM en Android]] (Model-View-ViewModel)
- UI Moderna: [[Jetpack Compose]]
- UI Clásica: [[Views y XML Layouts]]

### Componentes en Background
- [[Services y WorkManager]]
- [[Broadcast Receivers]]

---

## 🛠️ Recetario (Cómo se hace...)
*Soluciones prácticas, configuraciones y código reutilizable.*

### ⚙️ Configuración de Proyecto
- Manifiesto: [[AndroidManifest.xml]] (Permisos y declaración de componentes)
- Build System: [[build.gradle.kts]] (Gestión de dependencias y versiones)

### 🧱 Implementaciones Comunes
- **Red y API:** [[Retrofit + OkHttp]] (Llamadas HTTP)
- **Base de Datos Local:** [[Room Database]] (Abstracción de SQLite)
- **UI Patterns:** Snippets de [[LazyColumn (Compose)]] o [[RecyclerView Adapter (XML)]]
- **Seguridad:** [[Petición de Permisos en Runtime]]

---
