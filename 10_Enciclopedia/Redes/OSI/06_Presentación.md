# 🎭 Capa 6: Presentación ([[00_OSI|Modelo OSI]])

La **Capa de Presentación** es la responsable principal de preparar y formatear los datos para que puedan ser utilizados por la Capa de Aplicación. Su función es garantizar que la información sea "legible" y consumible para los sistemas de software.

---
![[presentation-layer.png]]
## 🛠️ Responsabilidades Principales

Esta capa actúa como un traductor y optimizador de datos, centrando su actividad en tres pilares:

### 1. Traducción (Sintaxis y Codificación)
Dos dispositivos que se comunican podrían utilizar distintos métodos de codificación de caracteres o formatos de datos. La Capa 6 traduce los datos entrantes a una sintaxis que la Capa de Aplicación receptora comprenda.
* *Ejemplo:* Manejo de formatos de serialización como **[[JSON]]**, **[[XML]]** o conversiones entre diferentes conjuntos de caracteres (como ASCII o Unicode).

### 2. Cifrado (Seguridad)
Si los dispositivos interactúan a través de una conexión cifrada, esta capa gestiona la seguridad del dato en sí mismo:
* **En el emisor:** Añade el cifrado a los datos provenientes de la aplicación.
* **En el receptor:** Decodifica el cifrado para entregar datos descifrados y legibles a la capa superior.

### 3. Compresión (Eficiencia)
La capa de presentación es la encargada de comprimir la información recibida de la aplicación antes de enviarla a la Capa 5 (Sesión).
* **Objetivo:** Minimizar la cantidad de datos transferidos para mejorar la velocidad y la eficiencia de la comunicación en la red.
---
## 🎯 Resumen de Flujo

En esencia, la Capa 6 se asegura de que el mensaje tenga el formato correcto:
1.  **Hacia abajo (Emisor):** Recibe datos de la aplicación -> Los traduce -> Los cifra -> Los comprime -> Los envía a la Capa de Sesión.
2.  **Hacia arriba (Receptor):** Recibe datos de la red -> Los descomprime -> Los descifra -> Los traduce -> Los entrega a la **[[API]]** o software cliente.