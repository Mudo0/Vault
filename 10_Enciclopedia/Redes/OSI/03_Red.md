# 🌐 Capa 3: Red ([[00_OSI|Modelo OSI]])

La **Capa de Red** es la responsable de permitir y facilitar la transferencia de datos entre dos redes distintas. A diferencia de las capas inferiores que gestionan la comunicación local, la Capa 3 es el núcleo de la interconexión de redes (*Internetworking*).

> **Distinción Clave:** Si dos dispositivos que se comunican se encuentran dentro de la misma red local (**[[LAN]]**), la intervención de la Capa de Red no es estrictamente necesaria, ya que la Capa de Enlace de Datos puede resolver la entrega.

---

![[network-layer.png]]
## 🛠️ Responsabilidades Principales

Esta capa actúa como el sistema logístico inteligente de la red, encargándose de:

### 1. Fragmentación y Reensamblaje (Paquetes)
La Capa de Red toma los segmentos provenientes de la Capa de Transporte (Capa 4) y los divide en unidades más pequeñas llamadas **Paquetes** en el dispositivo emisor. En el extremo receptor, se encarga de volver a juntar estos paquetes para reconstruir el segmento original.

### 2. Enrutamiento (*Routing*)
Es la función más crítica de esta capa. Consiste en determinar y buscar la mejor ruta física posible para que los datos viajen desde su origen hasta su destino final a través de múltiples nodos y redes intermedias.

---
## 📑 Protocolos de la Capa de Red

En este nivel operan protocolos esenciales para la estructura de Internet y la gestión de diagnósticos de red:

| Protocolo | Función Principal |
| :--- | :--- |
| **[[IP]] (Internet Protocol)** | Gestiona el direccionamiento lógico para que los paquetes lleguen al host correcto (IPv4 / IPv6). |
| **[[ICMP]]** | Protocolo de mensajes de control, utilizado para enviar notificaciones de error y diagnósticos (ej. comando `ping`). |
| **[[IGMP]]** | Protocolo de gestión de grupos, utilizado para el intercambio de mensajes *multicast*. |
| **IPsec** | Conjunto de protocolos para asegurar las comunicaciones sobre el protocolo **[[IP]]** mediante cifrado. |

---
## 💻 Conexión con el Desarrollo Backend

En el desarrollo de aplicaciones con **[[(.NET)]]** o **[[Java]]**, la Capa de Red suele estar abstraída por el sistema operativo. Sin embargo, su comprensión es vital para:

* **Configuración de Infraestructura:** Gestión de **[[Docker]]** bridges, redes virtuales en la nube y reglas de firewall.
* **Depuración:** Identificar si un fallo de conexión entre un microservicio en **[[ASP.NET]]** y una base de datos externa se debe a un error de enrutamiento o a una dirección **[[IP]]** mal configurada.
