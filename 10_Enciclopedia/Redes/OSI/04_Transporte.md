# 🚛 Capa 4: Transporte ([[00_OSI|Modelo OSI]])

La **Capa de Transporte** es la responsable de las comunicaciones de extremo a extremo (*end-to-end*) entre dos dispositivos. Su función principal es garantizar que los datos se entreguen de manera confiable y eficiente desde el origen hasta el destino final.

---
![[transport-layer.png]]

## 🧩 Segmentación y Reensamblaje

Antes de transferir la información a la Capa de Red (Capa 3), la Capa de Transporte realiza un proceso de fragmentación:

1.  **En el Emisor:** Toma los datos provenientes de la Capa de Sesión y los divide en unidades más pequeñas llamadas **Segmentos**.
2.  **En el Receptor:** Se encarga de recibir estos segmentos, ordenarlos y reensamblarlos para reconstruir los datos originales que la Capa de Sesión puede consumir.
---
## 🚦 Control de Flujo y de Errores

La Capa 4 no solo transporta datos, sino que gestiona la calidad y la integridad de la conexión mediante dos mecanismos críticos:

### 1. Control de Flujo
Determina la velocidad óptima de transmisión. Su objetivo es evitar que un emisor con una conexión de alta velocidad sature o "abrumen" a un receptor que posee una conexión más lenta o menor capacidad de procesamiento.

### 2. Control de Errores
Realiza una verificación en el extremo receptor para asegurar que los datos recibidos estén completos y sin corrupciones. Si se detecta que faltan segmentos o hay errores, la capa de transporte solicita automáticamente una retransmisión al emisor.

---

## 📑 Protocolos Principales

Existen dos protocolos fundamentales que operan en esta capa, cada uno con propósitos distintos según las necesidades de la aplicación:

| Protocolo | Nombre Completo | Características | Uso Común |
| :--- | :--- | :--- | :--- |
| **[[TCP]]** | Transmission Control Protocol | Orientado a conexión, garantiza la entrega y el orden de los datos. | Navegación web, **[[API|APIs]]**, transferencia de archivos. |
| **[[UDP]]** | User Datagram Protocol | No orientado a conexión, prioriza la velocidad sobre la fiabilidad. | Streaming de video, juegos online, llamadas VoIP. |

> **Conexión con el Desarrollo:** En entornos como **[[(.NET)]]** y **[[ASP.NET]]**, el manejo de estos protocolos se abstrae mediante clases como `TcpClient` o a través de servidores Kestrel que gestionan las conexiones **[[TCP]]** subyacentes de forma automática para tus aplicaciones web.