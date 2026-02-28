---
status: borrador
tags:
  - web
  - websocket
  - redes
  - javascript
  - tiempo-real
created: 2026-02-24
---
# 🔌 ¿Qué es un [[WebSocket]]?

Un **[[WebSocket]]** es un protocolo de comunicación que proporciona canales bidireccionales y de dúplex completo (*full-duplex*) a través de una única conexión **[[TCP]]** de larga duración. Es una tecnología fundamental para las aplicaciones web modernas que requieren flujo de información en tiempo real.

Para comprender su utilidad, resulta útil compararlo con el protocolo **[[HTTP]]** tradicional:

* **[[HTTP]] Tradicional:** Es unidireccional y se basa en el modelo de "petición-respuesta". El cliente (navegador) solicita información y el servidor responde. El servidor no puede enviar datos si el cliente no los ha solicitado previamente, y la conexión se cierra tras cada respuesta.
* **[[WebSocket]]:** Funciona como una llamada telefónica. Una vez establecida la conexión entre cliente y servidor, la línea permanece abierta. Cualquiera de las partes puede enviar datos en cualquier momento sin esperar una petición previa.



---

## 🔄 Ciclo de Vida de la Conexión

El funcionamiento de una conexión **[[WebSocket]]** consta de tres fases principales:

### 1. El Handshake (Apretón de manos)
El proceso inicia como una petición **[[HTTP]]** normal. El cliente envía una solicitud al servidor incluyendo cabeceras especiales (ej. `Upgrade: websocket`). Esto le indica al servidor la intención de cambiar el canal **[[HTTP]]** a un canal **[[WebSocket]]**.

### 2. Conexión Persistente
Si el servidor soporta WebSockets y acepta la petición, responde afirmativamente. A partir de este momento, el protocolo cambia y la conexión inicial no se cierra, manteniéndose activa de forma constante.

### 3. Transmisión de Datos
Tanto el cliente como el servidor pueden enviarse "mensajes" (texto o datos binarios) en cualquier dirección y momento. Esto elimina la latencia generada por la apertura de nuevas conexiones para cada envío de datos.



---

## 🎯 Usos y Aplicaciones

Los WebSockets se emplean siempre que se requiera **baja latencia** y **actualizaciones en tiempo real**.

**Casos de uso comunes:**
* **Aplicaciones de chat:** (ej. WhatsApp Web, Slack) donde los mensajes deben aparecer instantáneamente.
* **Juegos multijugador online:** Sincronización de movimientos en milisegundos.
* **Plataformas financieras:** Visualización de fluctuaciones en precios de acciones o criptomonedas en tiempo real.
* **Edición colaborativa:** (ej. Google Docs) visualización instantánea de las modificaciones de otros usuarios.
* **Notificaciones en vivo:** Alertas del sistema o actualizaciones de redes sociales.

---

## 👨‍💻 Ejemplo Básico: Cliente [[JavaScript]]

La implementación desde el navegador es directa gracias a la **[[API]]** nativa de **[[JavaScript]]**.

```javascript

// 1. Crear la conexión (apuntar al servidor WebSocket)
// Nota: Se usa 'ws://' en lugar de 'http://' (o 'wss://' para conexiones seguras)
const miSocket = new WebSocket('ws://[ejemplo.com/servidor-socket](https://ejemplo.com/servidor-socket)');

// 2. Escuchar cuando la conexión se abra correctamente
miSocket.onopen = function(evento) {
    console.log("¡Conexión establecida!");
    
    // Enviar un mensaje al servidor
    miSocket.send("Hola servidor, acabo de conectarme.");
};

// 3. Escuchar los mensajes que envía el servidor
miSocket.onmessage = function(evento) {
    console.log("El servidor dice: " + evento.data);
};

// 4. Manejar posibles errores
miSocket.onerror = function(error) {
    console.error("Hubo un error en el WebSocket:", error);
};

// 5. Detectar cuándo se cierra la conexión
miSocket.onclose = function() {
    console.log("Conexión cerrada.");
};