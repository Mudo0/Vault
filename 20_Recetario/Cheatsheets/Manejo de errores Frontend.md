![[Pasted image 20260316231028.png]]
# 🛡️ Arquitectura de Manejo de Errores por Capas (Frontend)

Esta estrategia representa un flujo estructurado en 5 capas, diseñado para capturar, procesar y mostrar errores de forma controlada en aplicaciones cliente (común en frameworks como **[[Angular]]**, **[[React]]** o **[[Vue]]**). 

Es una excelente referencia para entender cómo proteger una aplicación de fallos en diferentes niveles, evitando interrupciones abruptas en la experiencia del usuario.



---

## 🥞 Detalle de las Capas

### Capa 1 — GlobalErrorHandler
Actúa como la **red de seguridad final**. Su objetivo es capturar cualquier error que no haya sido manejado por la lógica específica de la aplicación, evitando cierres inesperados o que la consola colapse.

### Capa 2 — [[HTTP]] Interceptor
Funciona como un "peaje" centralizado para las peticiones al servidor. Captura errores de red o respuestas fallidas de la **[[API]]** (códigos 4xx y 5xx) antes de que la respuesta llegue a los servicios individuales de la app.

### Capa 3 — `catchError` en [[RxJS]] / [[WebSocket]]
Maneja la lógica específica de los flujos de datos reactivos y asíncronos. Permite gestionar errores en tiempo real, interceptar fallos en el *stream* de datos y configurar reconexiones automáticas si se pierde la señal.

### Capa 4 — NotificationService / Toast
Es la capa de comunicación directa con el usuario. Se encarga de traducir los errores técnicos en alertas visuales (*pop-ups*, *toasts*, *snackbars*) para informar qué salió mal de una manera amigable y no bloqueante.

### Capa 5 — Error Boundary Component
Define una "interfaz de respaldo" (*fallback*). Si una parte específica de la **[[UI]]** falla al intentar renderizarse, esta capa aísla el problema y muestra un mensaje de error localizado únicamente en esa sección, en lugar de corromper o dejar en blanco toda la pantalla de la aplicación.