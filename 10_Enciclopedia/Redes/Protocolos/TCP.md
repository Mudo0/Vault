---
status: final
tags:
  - redes
  - protocolos
  - tcp
  - capa-4
created: 2026-03-29
---
# 📦 [[TCP]] (Transmission Control Protocol)

**[[TCP]]** (Transmission Control Protocol) es un protocolo específico que vive en la **[[04_Transporte|Capa de Transporte]]**. Su única misión es asegurar que los datos lleguen completos, en orden y sin errores desde el punto A al punto B.

* **Es orientado a la conexión:** Antes de mandar un solo **[[Bits|bit]]**, hace un "**Handshake**" (el famoso *Three-way handshake*) para confirmar que el otro lado está escuchando.
* **Garantiza la entrega:** Si un paquete se pierde en el camino, **[[TCP]]** se da cuenta y pide que lo reenvíen.
* **Mantiene el orden:** Si los paquetes llegan mezclados, **[[TCP]]** los reordena antes de pasárselos a tu aplicación.

**En resumen:** **[[TCP]]** es el "mensajero obsesivo-compulsivo" que no se queda tranquilo hasta que confirmás que recibiste cada palabra del mensaje en el orden correcto.