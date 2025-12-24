---
status: borrador
tags:
  - conceptos
  - docker
  - virtualizacion
  - arquitectura
created: 2025-12-23
---
# 🆚 Virtualización vs. Containerización ([[Docker]])

La diferencia fundamental radica en el nivel en el que ocurre la abstracción: la virtualización (máquinas virtuales) abstrae el hardware físico, mientras que la containerización (**[[Docker]]**) abstrae el sistema operativo.

A continuación, se detallan las diferencias clave desglosadas por categorías:

---

## 1. 🏗️ Arquitectura y Núcleo (Kernel)

### Virtualización (Máquinas Virtuales - VM)
* Utiliza una capa de software llamada **Hypervisor** (como VirtualBox o VMWare) que se instala sobre el sistema anfitrión.
* Cada VM emula un sistema informático completo, lo que implica que incluye su propio Sistema Operativo "invitado" completo (*Guest OS*) con su propio kernel, binarios y librerías.

### Containerización ([[Docker]])
* Utiliza un **Container Engine** (Motor de contenedores).
* No posee un sistema operativo propio; en su lugar, comparte el kernel del sistema operativo del anfitrión (*Host OS*).
* Solo empaqueta la aplicación y sus dependencias (librerías, binarios, configuración), aislándolas a nivel de proceso.

---

## 2. ⚖️ Peso y Consumo de Recursos

* **VM:** Son pesadas. Dado que cada una posee un SO completo, una imagen de VM suele pesar varios Gigabytes (GBs). Además, requieren la asignación de recursos fijos (CPU, RAM) por adelantado, los cuales quedan bloqueados aunque la aplicación no los utilice.
* **Contenedores:** Son ligeros. Al no duplicar el SO, las imágenes suelen pesar solo cientos de Megabytes (MBs). Comparten los recursos del host dinámicamente, resultando mucho más eficientes.

---

## 3. ⚡ Rendimiento y Velocidad

* **VM:** El arranque es lento (minutos), ya que debe iniciar un sistema operativo completo desde cero en cada ocasión.
* **Contenedores:** El arranque es casi instantáneo (segundos). Al utilizar el kernel que ya se encuentra en ejecución en el anfitrión, solo necesitan iniciar el proceso de la aplicación.

---

## 4. 📦 Portabilidad y Aislamiento

* **VM:** Ofrece un aislamiento completo (incluso del SO), lo cual aporta seguridad pero reduce la portabilidad entre diferentes infraestructuras debido al peso y la dependencia del Hypervisor.
* **Contenedores:** Garantizan que la aplicación funcione idénticamente en cualquier entorno (desarrollo, testing, producción) debido a que empaquetan todas las dependencias necesarias. Son altamente portables y fáciles de compartir.

---

## 🏙️ Analogía Conceptual

Para visualizar la diferencia, se suele utilizar la comparación entre un Departamento y un Food Truck:

* **Máquina Virtual (Departamento):** Comparable a alquilar un departamento entero. Se dispone de cocina, baño y sala propios (infraestructura completa). Es cómodo y aislado, pero costoso de mantener, requiere más tiempo de construcción y no se puede trasladar fácilmente.
* **Contenedor (Food Truck):** Comparable a un puesto de comida móvil. Es liviano, transporta solo lo necesario para operar (la cocina y los ingredientes), es rápido de mover a cualquier ubicación y utiliza los recursos de la ciudad (calles/kernel) en lugar de construir infraestructura propia.