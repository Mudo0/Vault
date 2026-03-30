# ⛓️ Capa 2: Enlace de Datos ([[00_OSI|Modelo OSI]])

La **Capa de Enlace de Datos** es la responsable de facilitar la transferencia de información entre dos dispositivos que se encuentran dentro de la **misma red** (**[[LAN]]**). Mientras que la Capa de Red gestiona la comunicación entre redes distintas, la Capa 2 se ocupa del movimiento de datos en el ámbito local.

---
![[data-link-layer.png]]

## 🛠️ Responsabilidades y Funciones

Esta capa actúa como el puente entre el hardware físico y la lógica de red, encargándose de las siguientes tareas:

### 1. Tramado (*Framing*)
La Capa de Enlace de Datos toma los paquetes provenientes de la Capa de Red (Capa 3) y los divide en partes más pequeñas denominadas **Tramas** (*Frames*). Estas tramas contienen la información necesaria para que el hardware de red local (como un *Switch*) sepa exactamente a qué puerto físico debe enviar los datos.

### 2. Control de Flujo Local
Al igual que en niveles superiores, esta capa gestiona la velocidad de transmisión para asegurar que un dispositivo emisor no sature a un receptor dentro de la misma red.

### 3. Control de Errores
Realiza la detección y, en algunos casos, la corrección de errores que puedan ocurrir durante la transmisión física de los bits. Es importante notar que, mientras la Capa de Transporte (Capa 4) realiza este control para la comunicación de extremo a extremo, la Capa 2 lo hace específicamente para el trayecto dentro de la red local.

---
## 🏗️ Subcapas de la Capa 2

Para organizar mejor sus funciones, esta capa suele dividirse en dos subcapas:

1.  **LLC (Logical Link Control):** Identifica los protocolos de la capa de red y encapsula los datos para ser transmitidos.
2.  **MAC (Media Access Control):** Se encarga del direccionamiento físico y del acceso al medio. Aquí es donde operan las **Direcciones [[MAC]]** grabadas en las tarjetas de red de cada dispositivo.

---

## 🆚 Comparativa de Responsabilidades

| Característica | Capa 2 (Enlace de Datos) | Capa 3 (Red) | Capa 4 (Transporte) |
| :--- | :--- | :--- | :--- |
| **Ámbito** | Misma red local. | Redes diferentes. | Extremo a extremo (*End-to-End*). |
| **Unidad de Datos** | Trama (*Frame*). | Paquete (*Packet*). | Segmento (*Segment*). |
| **Direccionamiento** | Físico (**[[MAC]]**). | Lógico (**[[IP]]**). | Puertos. |

> **Nota de Contexto:** En el desarrollo de aplicaciones web con **[[ASP.NET]]** o **[[(.NET)]]**, la interacción con la Capa 2 es casi invisible, ya que el sistema operativo y el hardware se encargan de ella. Sin embargo, su correcto funcionamiento es lo que permite que una base de datos local o un microservicio en el mismo clúster de **[[Docker]]** se comuniquen a máxima velocidad.