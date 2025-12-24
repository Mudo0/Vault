---
status: borrador
tags:
  - docker
  - conceptos
  - arquitectura
created: 2025-12-24
---
# 🖼️ Imágenes vs. Contenedores ([[Docker]])

Para comprender **[[Docker]]**, resulta esencial distinguir entre dos conceptos fundamentales que funcionan de manera análoga a una receta y un plato elaborado.

---

## 1. 📜 ¿Qué es una Imagen? (El Plano)

Una imagen es un paquete ejecutable inmutable (de solo lectura) que contiene todo lo necesario para ejecutar una aplicación: el código, el entorno de ejecución (*runtime*), las librerías, las variables de entorno y los archivos de configuración.

* **Es una plantilla:** Se considera a la imagen como un plano arquitectónico. Define las características del edificio, los materiales y el diseño, pero no es habitable por sí misma.
* **Arquitectura de Capas:** Las imágenes se construyen mediante capas apiladas (*Union File System*). Cada instrucción en su construcción (como instalar una librería o copiar un archivo) genera una nueva capa, permitiendo la reutilización entre distintas imágenes para optimizar espacio.
* **Almacenamiento:** Las imágenes se almacenan en un registro (como Docker Hub) o en la caché local hasta su uso.

---

## 2. 🏗️ ¿Qué es un Contenedor? (El Edificio)

Un contenedor es la instancia en ejecución de una imagen. Representa el momento en que la imagen "cobra vida" y se convierte en un proceso aislado dentro del sistema operativo.

* **Es la materialización:** Siguiendo la analogía, si la imagen es el plano, el contenedor es el edificio construido. Constituye un entorno real y activo donde ocurren procesos.
* **Aislamiento y Eficiencia:** Aunque el contenedor comparte el kernel del sistema operativo anfitrión con otros contenedores, opera en su propio espacio aislado (posee su propia red, sistema de archivos y procesos).
* **Efímero:** Por defecto, los contenedores son volátiles. Si se elimina el contenedor, cualquier dato generado dentro de él se pierde (salvo que se utilicen volúmenes para persistir la información).

---

## 🆚 Resumen de la Relación

| Característica | Imagen (Image) | Contenedor (Container) |
| :--- | :--- | :--- |
| **Estado** | Estática (Solo lectura) | Dinámico (Ejecución) |
| **Analogía** | Plano / Receta / Clase | Edificio / Plato / Objeto |
| **Origen** | Se construye (`docker build`) o descarga (`docker pull`) | Se crea e inicia (`docker run`) desde una imagen |
| **Cantidad** | Una imagen única... | ...puede crear múltiples contenedores idénticos. |

---

## 🏙️ Analogía Conceptual

Para visualizar estos conceptos, se utiliza la comparación entre **Planos y Edificios**:

> "Una imagen [[Docker]] es como el plano de un edificio: define los materiales, el diseño y los pasos para construir. Un contenedor [[Docker]] es un edificio construido a partir de ese plano: es una instancia ejecutable, real y viva."

Es posible utilizar el mismo plano (imagen) para construir tantos edificios (contenedores) idénticos como se desee. Si se requiere modificar el diseño, no se altera el edificio ya construido, sino que se modifica el plano (se crea una nueva imagen) y se construyen nuevos edificios.