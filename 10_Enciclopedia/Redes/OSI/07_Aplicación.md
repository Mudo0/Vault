# 🖥️ Capa 7: Aplicación ([[00_OSI|Modelo OSI]])

La **Capa de Aplicación** es el nivel superior del **[[00_OSI|Modelo OSI]]** y es la única que interactúa de manera directa con los datos del usuario final. Actúa como la ventana para los servicios de red.

---
![[application-layer.png]]
## ⚙️ Funcionamiento e Interacción

Las aplicaciones de software, como los navegadores web y los clientes de correo electrónico, dependen de esta capa para iniciar y gestionar las comunicaciones a través de la red. 

### ⚠️ Distinción Crítica: Software vs. Capa
Es fundamental aclarar que las aplicaciones de software cliente (como Chrome, Outlook o una **[[API]]**) **no forman parte** de la capa de aplicación. 

En cambio, la capa de aplicación es la responsable de los **[[Protocolos]]** y la manipulación de datos de los que depende dicho software para presentar información con significado al usuario. En términos de desarrollo, esta capa proporciona la interfaz entre el código de la aplicación y el stack de red subyacente.

---

## 📑 Protocolos de la Capa de Aplicación

Esta capa define los protocolos que las aplicaciones utilizan para intercambiar datos. Algunos de los más relevantes incluyen:

* **[[HTTP]] (HyperText Transfer Protocol):** El protocolo base para la navegación web y la comunicación con servicios **[[ASP.NET]]** o **[[Spring Boot]]**.
* **[[SMTP]] (Simple Mail Transfer Protocol):** Uno de los estándares que permite las comunicaciones y transferencias por correo electrónico.
* **[[FTP]] (File Transfer Protocol):** Utilizado para la transferencia de archivos entre sistemas.
* **[[DNS]] (Domain Name System):** Encargado de la resolución de nombres de dominio en direcciones **[[IP]]**.
---
## 🎯 Responsabilidades Principales

1.  **Identificación de socios de comunicación:** Asegura que los destinos previstos sean localizables y estén disponibles.
2.  **Determinación de disponibilidad de recursos:** Verifica si existen los medios necesarios para establecer la conexión solicitada.
3.  **Sincronización de la comunicación:** Coordina el flujo de datos entre las aplicaciones emisor/receptor.
