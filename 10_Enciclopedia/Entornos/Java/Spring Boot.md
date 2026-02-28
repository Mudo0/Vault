---
status: final
tags:
  - java
  - spring-boot
  - backend
  - framework
  - web
created: 2026-01-06
---

# 🍃 ¿Qué es [[Spring Boot]]?

Spring Boot es un framework de [[Código Abierto]] para Java que simplifica enormemente la creación de aplicaciones basadas en el framework Spring, permitiendo desarrollar microservicios y aplicaciones web listas para producción rápidamente, sin configuraciones complejas, gracias a características como la autoconfiguración, los "Starters" (dependencias preconfiguradas) y servidores web integrados, enfocándose en la productividad del desarrollador

Para comprender su función, se puede concebir al **Spring Framework** tradicional como un motor potente pero desensamblado: requiere conectar cables, configurar combustible y ajustar componentes manualmente (archivos **[[XML]]**, configuración de *beans*, servidores de aplicaciones externos, etc.).

**[[Spring Boot]]**, por el contrario, es ese mismo motor ya montado en un vehículo listo para conducir. Es una extensión de Spring que favorece la "convención sobre configuración". Su objetivo principal es permitir la ejecución de una aplicación con la mayor rapidez posible y la mínima configuración necesaria.

---

## 🏛️ Los 3 Pilares Fundamentales

Para un proyecto nuevo, estos son los aspectos críticos:

### 1. Auto-configuración
[[Spring Boot]] escanea las librerías presentes en el proyecto (el *classpath*) y configura los "Beans" automáticamente.
* *Ejemplo:* Si se detecta una base de datos H2 en las dependencias, se configurará automáticamente la conexión a la base de datos en memoria sin necesidad de escribir código de configuración.

### 2. Starters (Dependencias Inteligentes)
En lugar de buscar múltiples librerías compatibles entre sí para crear una **[[API]]** **[[REST]]**, basta con agregar una única dependencia.
* *Ejemplo:* `spring-boot-starter-web` incluye automáticamente Tomcat (servidor), Spring MVC (framework web), Jackson (para **[[JSON]]**) y Logback (logging), asegurando la compatibilidad de versiones.

### 3. Standalone (Autónomo)
No requiere la instalación de un servidor Tomcat o JBoss por separado. La aplicación genera un archivo `.jar` que lleva el servidor embebido en su interior. Se ejecuta como cualquier programa **[[Java]]** (`java -jar mi-app.jar`).

---

## 👨‍💻 Ejemplo Práctico: "Hola Mundo" Web

A continuación, se compara el código necesario.

### 1. El punto de entrada (Main)
Todo proyecto cuenta con una clase principal anotada con `@SpringBootApplication`. Esta única línea activa el escaneo de componentes y la auto-configuración.

```Java
package com.miempresa.proyecto;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MiAplicacion {

    public static void main(String[] args) {
        // Esta línea arranca el servidor Tomcat embebido y toda la app
        SpringApplication.run(MiAplicacion.class, args);
    }
}

```
### 2. Creando un Endpoint (Controller)

Sin archivos **[[XML]]**, utilizando únicamente clases y anotaciones.


```Java
package com.miempresa.proyecto.controladores;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController // Indica que esta clase maneja peticiones HTTP y responde JSON/Texto
public class SaludoController {

    @GetMapping("/hola") // Mapea la URL http://localhost:8080/hola
    public String saludar() {
        return "¡Hola! Tu proyecto Spring Boot está funcionando.";
    }
}
```

---

## 🚀 Usos Principales

En la actualidad, su uso predomina en:

- **Microservicios:** Debido a su ligereza y autonomía.
- **[[API|APIs]] [[REST]]ful:** Como backend para aplicaciones de React, Angular, Vue o móviles.
- **Aplicaciones Cloud-Native:** Preparadas para desplegarse en **[[Docker]]** y **[[Kubernetes]]** con facilidad.

---

## 💡 Consejo para el Inicio

Para comenzar un proyecto, se recomienda utilizar **Spring Initializr** (`start.spring.io`) en lugar de crear la estructura manualmente. Es la herramienta oficial para generar la base del proyecto, permitiendo seleccionar:

- **Build tool:** **[[Maven]]** o **[[Gradle]]**.
- **Lenguaje:** **[[Java]]**, Kotlin o Groovy.
- **Dependencias:** Spring Web, Spring Data JPA, Lombok, etc.