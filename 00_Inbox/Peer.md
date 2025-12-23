---
status: borrador
tags:
  - conceptos
  - redes
  - arquitectura
created: 2025-12-23
---
# 👥 ¿Qué es un Peer?

Un **Peer** (término en inglés para "par", "colega" o "igual") se define como una computadora o dispositivo dentro de una red que posee la misma autoridad y capacidad operativa que el resto de los integrantes de dicha red.

---

## 🆚 Diferencia de Modelos

Para comprender el concepto, es útil contrastarlo con el modelo tradicional:

### 1. Modelo [[Cliente-Servidor]] (Tradicional)
* **Analogía:** Una clase con un profesor (Servidor) y alumnos (Clientes).
* **Funcionamiento:** Si un alumno requiere información, debe solicitársela al profesor. Los alumnos no se enseñan entre sí; dependen de la autoridad central (el servidor) para obtener los recursos.

### 2. Modelo [[P2P]] (Peer-to-Peer)
* **Analogía:** Un grupo de estudio sin profesor.
* **Funcionamiento:** Todos los integrantes son estudiantes (**Peers**). La información fluye horizontalmente (ej. Juan comparte apuntes con María). Todos son iguales; aportan y reciben conocimientos sin jerarquías.

---

## ⚙️ Funcionamiento Técnico

En una red de "pares" (conocida como [[P2P]]), un nodo o Peer actúa simultáneamente con dos roles:

* **Como Cliente:** Solicita y descarga archivos o datos de otros dispositivos.
* **Como Servidor:** Ofrece y comparte sus propios archivos, espacio en disco o potencia de procesamiento con los demás miembros de la red.

---

## 🌍 Ejemplos Cotidianos

### A. Descarga de Torrents (BitTorrent)
Al descargar contenido mediante torrents, no se obtiene el archivo de un servidor central. El dispositivo (el Peer) recolecta fragmentos del archivo desde las computadoras de miles de usuarios alrededor del mundo. Simultáneamente, el dispositivo envía los fragmentos que ya posee a otros usuarios que los necesitan.

### B. Criptomonedas ([[Bitcoin]])
La red de [[Bitcoin]] no depende de una entidad bancaria centralizada. Se sostiene mediante miles de "peers" (nodos). Cada computadora mantiene una copia del libro contable (blockchain). Si un nodo se desconecta, la red continúa operativa gracias a la redundancia de información en los demás pares.

### C. Juegos Online (Hosting local)
En ciertos videojuegos o redes LAN, un jugador actúa como anfitrión ("host") de la partida y los demás se conectan a su equipo. En este escenario, actúan como pares conectados directamente entre sí para la transmisión de datos, sin intermediación de un servidor dedicado externo.

---

## 📝 Resumen

Un **Peer** constituye un nodo colaborativo en la red. No ejerce un rol exclusivo de jefe (servidor) ni de subordinado (cliente), sino que opera como un igual que colabora para mantener la funcionalidad y disponibilidad de la red.