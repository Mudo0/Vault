---
status: borrador
tags:
  - docker
  - backend
  - software
created: 2025-12-23
---

# 🐳 Docker

**Docker** es una plataforma abierta que permite empaquetar aplicaciones en unidades estandarizadas llamadas **Contenedores**. Estos contenedores incluyen todo lo necesario para que el software se ejecute: código, herramientas del sistema, bibliotecas y configuraciones.

Su objetivo principal es separar la aplicación de la infraestructura, permitiendo entregar software rápidamente y asegurando que funcione igual en cualquier entorno.

---

## 🧠 Explicación simplificada

El concepto de contenedor se entiende mejor con la analogía del **Tupper (Recipiente de comida)**:

- **La Comida (Tu App):** Lo que quieres transportar (código, dependencias).
- **El Tupper (El Contenedor):** Es el envase estandarizado. Mantiene la comida aislada, evita que se mezcle con otras cosas y asegura que no se derrame.
- **La Mochila (El Servidor):** No importa qué mochila uses, si la comida está en el tupper, no se va a ensuciar ni a romper.

Sin Docker, es como llevar arroz suelto en el bolsillo: se mezcla con las llaves, mancha la tela y es un lío limpiarlo.

---

## 🏭 Ejemplos en la Industria

* **Microservicios:** Empresas como Netflix o Uber no usan un "servidor gigante", sino miles de pequeños contenedores que se crean y destruyen según la demanda.
* **CI/CD:** Las pruebas automáticas de GitHub corren en contenedores efímeros que garantizan un entorno limpio cada vez.

---

## 💻 Snippets de Configuración (Run Once)

Para desarrollo local, usamos Docker para levantar servicios de infraestructura sin instalar basura en Windows.

### 🐘 PostgreSQL
Base de datos relacional estándar. [[Postgres]]

```bash
docker run --name mi-postgres \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=miPassword \
  -v pg_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres