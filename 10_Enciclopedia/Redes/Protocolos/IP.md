---
status: final
tags:
  - redes
  - protocolos
  - ip
  - capa-3
created: 2026-03-30
---
# 🌐 IP (Internet Protocol)

## 🛠️ ¿Qué es y para qué sirve?

**[[IP]]** es el protocolo principal de la **[[03_Red|Capa de Red]]**. Su función básica es permitir la comunicación bidireccional entre dispositivos en una red (o entre redes distintas, como Internet).

* **Identificación:** Le asigna una etiqueta numérica única (dirección **[[IP]]**) a cada dispositivo.
* **Encaminamiento (Routing):** Decide qué camino deben tomar los paquetes de datos para llegar de la red A a la red B.
* **Entrega "Best Effort":** A diferencia de **[[TCP]]**, a **[[IP]]** no le importa si el paquete llega roto o si no llega; su único laburo es intentar mandarlo a la dirección correcta.

---
## 🏗️ ¿Cómo está compuesto?

Un paquete de **[[IP]]** (técnicamente llamado [[datagrama]]) tiene dos partes principales:

### 1. El Header (Encabezado)
Es donde está la "metadata" necesaria para que los **[[Router|routers]]** sepan qué hacer con el paquete. Contiene:
* **Versión:** Si es **[[IPv4]]** o **[[IPv6]]**.
* **Dirección de Origen y Destino:** Fundamental para saber de dónde viene y a dónde va.
* **TTL (Time to Live):** Un contador que evita que un paquete dé vueltas infinitas en internet. Cada vez que pasa por un router, el **TTL** baja 1. Si llega a 0, el paquete se descarta.
* **Protocolo:** Indica si lo que viene adentro es **[[TCP]]**, **[[UDP]]**, **[[ICMP]]**, etc.

### 2. El Payload (Carga útil)
Es el contenido real, es decir, los datos que vienen de las capas superiores (como el segmento de **[[TCP]]** ya anotado).

---
## 🔄 ¿Cómo funciona? (El proceso)

El funcionamiento de **[[IP]]** es "*connectionless*" (no orientado a la conexión). No saluda antes de mandar, simplemente dispara el paquete. 

1.  **Fragmentación:** Si el mensaje es muy grande para la red, **[[IP]]** lo divide en pedazos más chicos.
2.  **Direccionamiento:** Se le pega la etiqueta de **[[IP]]** de destino al paquete.
3.  **Salto de Router en Router:** El paquete sale de la computadora al router local. El router mira la **[[IP]]** de destino y, si no es el destinatario, lo pasa al siguiente nodo más cercano.
4.  **Llegada:** El dispositivo de destino recibe los paquetes. Como **[[IP]]** no garantiza el orden, aquí es donde entra **[[TCP]]** (en la capa superior) para acomodarlos y verificar que no falte ninguno.

---
## 🌍 IPv4 vs IPv6
* **[[IPv4]]**: 32 bits (ej: `192.168.1.1`). Hay unos 4.300 millones de combinaciones y ya se han agotado.
* **[[IPv6]]**: 128 bits (ej: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`). Son básicamente infinitas y es el estándar que está reemplazando al viejo **[[IPv4]]**.