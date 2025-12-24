---
status: borrador
tags:
  - docker
  - arquitectura
  - componentes
  - devops
created: 2025-12-23
---
# 🏗️ Arquitectura de [[Docker]]

La arquitectura de **[[Docker]]** funciona bajo un modelo [[Cliente-Servidor]] e introduce un enfoque revolucionario al separar la construcción, el envío y la ejecución de aplicaciones.

A continuación se detalla su composición y lo que sucede internamente al ejecutar un comando.

---

## 1. 🧩 Componentes Principales de la Arquitectura

Para comprender el funcionamiento, se deben identificar las piezas clave:

### Docker Client (Cliente)
Es la herramienta con la cual se interactúa (generalmente la **[[CLI]]** o línea de comandos). Su función es convertir los comandos (como `docker run` o `docker build`) en peticiones a la **[[API]]** y enviarlas al Docker Daemon.

### Docker Host (El servidor)
Es la máquina donde se ejecuta el motor de [[Docker]]. Dentro de este host operan componentes vitales:
* **[[Docker Daemon]] (`dockerd`):** Es el proceso en segundo plano que escucha las peticiones del cliente y gestiona los objetos de Docker (imágenes, contenedores, redes).
* **containerd:** Es un gestor de ejecución (*runtime*) de alto nivel. Se encarga del ciclo de vida del contenedor: buscar la imagen, descomprimirla y solicitar a `runc` que ejecute el contenedor.
* **runc:** Es el ejecutor de bajo nivel. Se comunica directamente con el kernel del sistema operativo para crear el espacio aislado donde residirá el contenedor. Una característica particular es que `runc` finaliza apenas el contenedor inicia.

### Docker Registry
Es el almacén donde se guardan las imágenes. El más conocido es Docker Hub (público), aunque pueden configurarse registros privados.

### Objetos
* **[[Imágenes]]:** Son plantillas de solo lectura (los "planos") construidas por capas.
* **[[Image & Container|Contenedores]]:** Son las instancias ejecutables y vivas de dichas imágenes.

---

## 2. 🔄 El Flujo de Ejecución

Tomando como ejemplo el comando más común: `docker run hello-world`. Aunque la ejecución parece instantánea, desencadena una secuencia de pasos orquestada entre los componentes mencionados:

1.  **El Cliente envía la orden:**
    El Docker Client convierte el comando en una llamada a la **[[API]]** (una petición **[[HTTP]]** POST) y la envía al Docker Daemon.
2.  **El Daemon recibe y delega:**
    El `dockerd` recibe la solicitud. No ejecuta el contenedor directamente, sino que contacta a `containerd` para que gestione la tarea.
3.  **Búsqueda de la Imagen (Pull):**
    `containerd` verifica si la imagen existe localmente. De no encontrarla, se conecta al Registry (como Docker Hub), descarga las capas necesarias y las prepara.
4.  **Creación del Contenedor:**
    Una vez lista la imagen, `containerd` ordena a `runc` que cree el contenedor. `runc` interactúa con el kernel del sistema operativo para aislar los recursos (CPU, memoria, red).
5.  **Ejecución y Salida:**
    `runc` inicia el proceso de la aplicación dentro del contenedor y luego se cierra (sale) automáticamente, dejando al contenedor ejecutándose de forma ligera y aislada.

---

## 🏙️ Analogía Conceptual

Es posible visualizar esta arquitectura utilizando la analogía de la **Construcción de Edificios**:

* **La Imagen es el Plano Arquitectónico:** Define los materiales, el diseño y la estructura, pero no es habitable. Es inmutable (de solo lectura).
* **El Contenedor es el Edificio Construido:** Es la materialización del plano en el mundo real. Es una instancia viva donde ocurren actividades.
* **Docker Client:** Representa al **Arquitecto** que emite la orden de construir.
* **Docker Daemon/Engine:** Representa a la **Constructora** que recibe la orden y coordina a los trabajadores (`containerd` y `runc`) para levantar el edificio según el plano.

De esta forma, se puede utilizar el mismo "plano" (imagen) para construir tantos "edificios" (contenedores) idénticos como se necesiten, de manera rápida y eficiente.