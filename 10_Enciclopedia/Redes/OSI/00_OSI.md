---
status: final
tags:
  - redes
  - protocolos
  - infraestructura
  - estandares
created: 2026-03-29
---
# 🌐 Modelo OSI (Open Systems Interconnection)

El **Modelo OSI** es un marco conceptual creado por la Organización Internacional para la Estandarización (**[[ISO]]**), diseñado para permitir que diversos sistemas de comunicación se conecten utilizando **[[Protocolos]]** estándar. 

En esencia, el modelo OSI proporciona un lenguaje universal y un estándar técnico para que distintos sistemas y equipos de hardware puedan interoperar entre sí, independientemente de su fabricante o arquitectura interna.

---

## 🏗️ Estructura: Las 7 Capas Abstractas

El modelo se basa en el concepto de dividir un sistema de comunicación en siete capas abstractas, organizadas de forma vertical (pila). Cada capa se apoya en la anterior y ofrece servicios a la superior.

![[osi-layers.png]]

### Clasificación de las Capas:


1.  **Capas de Host (End-to-End):** Se enfocan en la entrega de datos y la interacción con el software.
    * **[[07_Aplicación|Capa 7 - Aplicación]]:** Interfaz directa con los servicios de red (ej. **[[HTTP]]**, **[[SMTP]]**, **[[FTP]]**).
    * **[[06_Presentación|Capa 6 - Presentación]]:** Traducción, cifrado y compresión de datos.
    * **[[05_Sesión|Capa 5 - Sesión]]:** Gestión de diálogos y mantenimiento de conexiones.
    * **[[04_Transporte|Capa 4 - Transporte]]:** Conexiones extremo a extremo y control de flujo (**[[TCP]]**/**[[UDP]]**).
2.  **Capas de Medios (Host-to-Network):** Se encargan de la transmisión física y el direccionamiento de los datos.
    * **[[03_Red|Capa 3 - Red]]:** Determinación de ruta e **[[IP]]** (direccionamiento lógico).
    * **[[02_Enlace de Datos|Capa 2 - Enlace de Datos]]:** Direccionamiento físico (**MAC**) y detección de errores.
    * **[[01_Física|Capa 1 - Física]]:** Transmisión de bits crudos sobre el medio físico (cables, ondas).
---

## 🔄 El Proceso de Encapsulamiento

Para que la comunicación ocurra, los datos deben viajar desde la Capa 7 del emisor hasta la Capa 1, transmitirse por el medio físico, y luego subir desde la Capa 1 hasta la Capa 7 del receptor.


* **Encapsulamiento:** A medida que los datos bajan por la pila en el emisor, cada capa añade su propia información de control (cabeceras o *headers*).
* **Desencapsulamiento:** En el receptor, cada capa remueve su cabecera correspondiente y entrega los datos limpios a la capa superior.

> **💡 Nota comparativa:** Aunque el modelo OSI es el estándar teórico por excelencia, el modelo que realmente utiliza internet hoy en día es el modelo **[[TCP-IP|TCP/IP]]**, que es una versión más simplificada y práctica de estas capas.

