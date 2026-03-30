---
status: final
tags:
  - redes
  - protocolos
  - websocket
  - mensajeria
  - backend
created: 2026-03-16
---
# 📩 Protocolo STOMP

**STOMP** (Simple Text Oriented Messaging Protocol) es un protocolo de mensajería muy ligero diseñado para que aplicaciones escritas en diferentes lenguajes (como **[[Java]]**, **[[Python]]**, **[[JavaScript]]** o Ruby) puedan comunicarse entre sí a través de un **[[Message Broker]]** (un intermediario de mensajes).

Se puede conceptualizar como el "**[[HTTP]]** de la mensajería": es fácil de leer para los humanos, está basado en texto y resulta muy sencillo de implementar.

---

## 🛠️ ¿Para qué se utiliza?

Su uso principal es servir como capa de comunicación en sistemas donde se requiere el envío asíncrono de mensajes. Sus aplicaciones más comunes incluyen:

* **[[WebSocket|WebSockets]] en Aplicaciones Web:** Es el estándar *de facto* al utilizar **[[WebSocket]]**. Dado que estos solo proporcionan un "tubo" de datos crudos, STOMP añade la estructura (comandos, destinos, cabeceras) para que el navegador y el servidor sepan cómo interpretar la información.
* **Sistemas de Chat y Notificaciones:** Ideal para enviar mensajes en tiempo real (ej. "usuario-1 se ha conectado", "tienes un nuevo mensaje").
* **Interoperabilidad:** Permite que un backend en **[[Java]]** se comunique con un frontend en **[[React]]** o un script en **[[Python]]** sin conocer los detalles internos del otro; solo necesitan comunicarse en STOMP.
* **Integración con Message Brokers:** Se utiliza para interactuar con servidores de mensajería populares como **[[RabbitMQ]]**, Apache ActiveMQ o **[[Spring Boot]]**.

---

## 🏗️ ¿Cómo funciona?

STOMP opera mediante *frames* (marcos) de texto. Cada *frame* consta de un comando, una serie de cabeceras (opcionales) y un cuerpo de datos.

### Ejemplo de un mensaje STOMP:
```text
SEND
destination:/queue/pedidos
content-type:text/plain

Hola, este es un nuevo pedido.
^@
```

> _(El símbolo `^@` al final representa un carácter nulo que indica el fin del mensaje)._

## Conceptos clave:

- **Destinos (_Destinations_):** Son cadenas de texto que indican la ruta a la que se dirige el mensaje (por ejemplo, `/topic/novedades` o `/queue/pagos`).
- **Productores:** Quienes envían mensajes mediante el comando `SEND`.
- **Consumidores:** Quienes se registran para recibir mensajes mediante el comando `SUBSCRIBE`.

---

## 📋 Comandos principales

|**Comando**|**Acción**|
|---|---|
|`CONNECT`|El cliente inicia la sesión con el servidor/broker.|
|`SEND`|Envía un mensaje a un destino específico.|
|`SUBSCRIBE`|Indica que el cliente desea escuchar mensajes de un destino.|
|`UNSUBSCRIBE`|Deja de escuchar un destino.|
|`ACK` / `NACK`|Confirma (o rechaza) que un mensaje ha sido procesado correctamente.|
|`DISCONNECT`|Cierra la conexión de forma limpia.|

---

## ⚖️ Ventajas y Desventajas

| **Ventajas**                                                                                              | **Desventajas**                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sencillez:** Es extremadamente simple. Se puede desarrollar un cliente STOMP básico en un par de horas. | **Eficiencia:** Al estar basado en texto, no es tan eficiente como los protocolos binarios (ej. **[[MQTT]]** o Protobuf) si se requiere transmitir volúmenes gigantescos de datos a alta velocidad. |
| **Ligereza:** Muy ligero en comparación con protocolos más complejos como **[[AMQP]]**.                   |                                                                                                                                                                                                     |

