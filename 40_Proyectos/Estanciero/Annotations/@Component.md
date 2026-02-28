---
status: borrador
tags:
  - java
  - spring-boot
  - spring-framework
  - inyeccion-dependencias
  - componentes
created: 2026-01-24
---
# 🧩 Anotación @Component ([[Spring Boot]])

Para comprender el funcionamiento de esta anotación, se puede concebir a **[[Spring Boot]]** como una gran oficina y al Contenedor de Spring (*ApplicationContext*) como el Jefe. El Jefe necesita saber a quién contratar (qué clases instanciar) y tenerlos disponibles para cuando sean requeridos.

* **Sin la anotación:** Una clase (ej. `GameFactory`) es simplemente código inerte. Spring ignora su existencia y no puede utilizarla.
* **Con `@Component`:** La anotación funciona como una etiqueta que comunica al framework: *"Esta es una pieza útil. Se solicita crear una instancia (ejecutar `new GameFactory()`) al iniciar la aplicación y almacenarla en memoria"*.

---

## 🆚 @Component vs. Estereotipos Específicos

Técnicamente, las anotaciones de especialización son funcionalmente casi idénticas a `@Component`, pero aportan semántica al código. Spring organiza sus etiquetas de la siguiente manera:

* **`@Component`:** La etiqueta genérica ("Soy una pieza gestionada por Spring").
* **`@Service`:** Es un `@Component`, pero semánticamente indica "Aquí reside lógica de negocio".
* **`@Repository`:** Es un `@Component`, pero indica "Aquí se interactúa con la base de datos" (y habilita traducción de excepciones de persistencia).
* **`@Controller`:** Es un `@Component`, pero indica "Aquí se reciben peticiones Web".



---

## 🛠️ Guía de Uso: ¿Cuándo usar cuál?

La elección depende de la responsabilidad de la clase:

1.  **Usa `@Service`:** Para clases que contienen la lógica de negocio principal (ej. `LobbyService`).
2.  **Usa `@Component`:** Para herramientas útiles, clases de utilería o *Factories* (como el ejemplo `GameFactory`), que no constituyen exactamente "lógica de negocio" ni "acceso a datos", sino componentes auxiliares o ayudantes.