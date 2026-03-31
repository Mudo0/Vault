---
status: final
tags:
  - java
  - maven
  - herramientas
  - devops
  - dependencias
created: 2026-01-19
---
# 🪶 ¿Qué es Apache Maven?

Maven es una herramienta fundamental en el desarrollo de software, especialmente en el entorno **[[Java]]**. En términos simples, se define como una herramienta de automatización de construcción (*build automation*) y gestión de dependencias.

Se puede conceptualizar como un "Jefe de Obra" inteligente: se le suministran los planos (el archivo de configuración) y este se encarga de conseguir los materiales (librerías externas) y organizar la construcción (compilar, probar y empaquetar).

---

## 🎯 ¿Para qué sirve?

Maven resuelve tres problemas principales en la programación:

1.  **El infierno de las dependencias:** Elimina la necesidad de descargar manualmente archivos `.jar` y verificar su compatibilidad. Basta con escribir el nombre y la versión requerida para que se descarguen automáticamente.
2.  **Estandarización:** Obliga al uso de una estructura de carpetas estándar. Esto permite ubicar rápidamente el código fuente y las pruebas en cualquier proyecto Maven.
3.  **Ciclo de vida:** Automatiza tareas repetitivas como la compilación, ejecución de pruebas unitarias, generación de reportes y creación del ejecutable final (JAR o WAR).

---

## ❤️ El Corazón: `pom.xml`

Todo proyecto Maven posee un archivo en la raíz llamado `pom.xml` (*Project Object Model*). Funciona como la "receta" del proyecto, definiendo:

* **Identidad:** El nombre y versión del proyecto.
* **Necesidades:** Las librerías externas (dependencias).
* **Construcción:** Plugins y configuraciones especiales.

### Conceptos Clave (Coordenadas GAV)
Para identificar cualquier librería se utilizan tres datos:
* **GroupId:** El identificador de la organización (ej. `com.google.code.gson`).
* **ArtifactId:** El nombre del proyecto o librería (ej. `gson`).
* **Version:** La versión específica (ej. `2.8.9`).

---

## 🛠️ Implementación Paso a Paso

### 1. Estructura de Carpetas
Maven espera la siguiente organización predeterminada:

```text
mi-proyecto/
 ├── pom.xml              <-- Archivo de configuración
 └── src/
     ├── main/
     │   ├── java/        <-- Código fuente
     │   └── resources/   <-- Configuraciones, imágenes, etc.
     └── test/
         └── java/        <-- Pruebas unitarias
```

### 2. Ejemplo de un `pom.xml` básico

Configuración de ejemplo utilizando la librería Gson para manejar **[[JSON]]**:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.miempresa</groupId>
    <artifactId>mi-aplicacion</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.8.9</version>
        </dependency>
    </dependencies>
</project>
```

### 3. Los Comandos (El ciclo de vida)

Maven funciona mediante "fases".

|**Comando**|**Acción**|
|---|---|
|`mvn clean`|**Limpia**. Borra la carpeta `target` (compilados previos) para iniciar desde cero.|
|`mvn compile`|**Compila**. Transforma el código `.java` en `.class`.|
|`mvn test`|**Prueba**. Ejecuta las pruebas unitarias (carpeta `src/test`).|
|`mvn package`|**Empaqueta**. Genera el archivo distribuible (como un `.jar`).|
|`mvn install`|**Instala**. Copia el `.jar` al repositorio local para uso de otros proyectos en el equipo.|

> **Nota:** Los comandos son acumulativos. Al ejecutar `mvn package`, Maven realiza automáticamente `compile` y `test` antes de empaquetar.

---

## 🔄 Resumen del Flujo de Trabajo

1. Se crea el proyecto y el archivo `pom.xml`.
2. Se añade una dependencia en el archivo (ej. conector de base de datos).
3. Se ejecuta `mvn install`.
4. Maven lee el archivo, consulta el **Repositorio Central** (nube), descarga la librería y la almacena en el **Repositorio Local** (carpeta oculta `.m2`).