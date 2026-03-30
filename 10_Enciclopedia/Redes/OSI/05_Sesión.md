# ⏳ Capa 5: Sesión ([[00_OSI|Modelo OSI]])

La **Capa de Sesión** es la encargada de actuar como el "director de orquesta" de la comunicación, gestionando la apertura, el mantenimiento y el cierre de las conexiones entre dos dispositivos.

Se define como **Sesión** al tiempo que transcurre desde que se abre la comunicación hasta que se da por finalizada.

---
![[session-layer.png]]
## ⚙️ Gestión de la Comunicación

Esta capa tiene dos responsabilidades críticas respecto al flujo de la conexión:

1.  **Persistencia:** Garantiza que la sesión permanezca abierta el tiempo suficiente para que todos los datos intercambiados se transfieran íntegramente.
2.  **Eficiencia de Recursos:** Una vez finalizada la transferencia, la capa de sesión cierra la conexión sin demora para evitar el desperdicio de recursos del sistema y de la red.
---
## 🏁 Sincronización y Puntos de Control

Una de las funciones más potentes de la Capa 5 es la capacidad de **sincronizar la transferencia** mediante el uso de puntos de control (*checkpoints*). 

### Mecanismo de Recuperación de Fallos
Si ocurre una desconexión o caída del sistema durante una transferencia extensa, los puntos de control permiten que la sesión se reanude desde el último estado guardado en lugar de reiniciar todo el proceso desde cero.

**Ejemplo Práctico:**
* Se transfiere un archivo de **100 MB**.
* La Capa de Sesión fija un punto de control cada **5 MB**.
* Si la conexión falla a los **52 MB**, el sistema detecta el último punto de control validado (50 MB).
* Al restablecerse, solo quedan pendientes de transmisión **50 MB**, ahorrando tiempo y ancho de banda.

---
## 🎯 Resumen de Funciones

* **Control de Diálogo:** Determina quién transmite, cuándo y por cuánto tiempo (mantenimiento de turnos).
* **Agrupamiento:** Marcación de grupos de datos para asegurar que se procesen como una unidad.
* **Recuperación:** Uso de puntos de control para reanudar diálogos tras interrupciones sin pérdida masiva de progreso.

> **Nota de Contexto:** En el desarrollo web moderno, conceptos como los **[[WebSocket]]** o las sesiones de usuario en **[[ASP.NET]]** heredan lógicamente estas responsabilidades, aunque su implementación técnica varíe respecto al modelo teórico original.