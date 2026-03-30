---
status: final
tags:
  - redes
  - protocolos
  - tcp-ip
  - capas
  - internet
created: 2026-03-30
---
# 🕸️ Modelo TCP/IP

Para entender qué es **TCP/IP**, imaginalo como el reglamento oficial y el sistema de logística que permite que internet funcione. No es un solo protocolo, sino un conjunto (*[[Suite]]*) de protocolos que trabajan en equipo para que un mensaje salga de tu computadora y llegue a otra sin romperse en el camino.

---
## ❓ ¿QUÉ es TCP/IP?

**TCP/IP** son las siglas de *Transmission Control Protocol/Internet Protocol*. Es el modelo estándar de comunicación en redes.

* **[[IP]] (Capa de Red):** Se encarga de la dirección y el enrutamiento. Sabe a dónde tiene que ir el paquete (como el sobre de una carta con la dirección).
* **[[TCP]] (Capa de Transporte):** Se encarga de la integridad. Corta la información en pedazos, los numera y se asegura de que lleguen todos bien y en orden (como el control de calidad).

---

## 🏗️ ¿CÓMO funciona? (El modelo de 4 capas)

A diferencia del modelo OSI de 7 capas, el modelo **[[TCP-IP|TCP/IP]]** es más práctico y se divide en 4 capas principales. La información baja por estas capas en el emisor y sube en el receptor:

### 1. Capa de Aplicación
Es donde interactúan los programas (tu navegador, el cliente de mail, un juego). Aquí se definen protocolos como **[[HTTP]]** (web), **[[FTP]]** (archivos) o **[[SMTP]]** (mail).
> **Dato:** Acá los datos están "en bruto", tal como los entiende la aplicación.

### 2. Capa de Transporte ([[TCP]] / [[UDP]])
Acá es donde el mensaje se divide en segmentos.
* **TCP** le pone un número de secuencia a cada pedazo para que, si llegan desordenados, la otra punta sepa cómo armarlos.
* Si un pedazo se pierde, **TCP** pide que se mande de nuevo.

### 3. Capa de Internet (IP)
Los segmentos se meten dentro de paquetes (datagramas). Se les pega la etiqueta de **[[IP]]** de origen e **[[IP]]** de destino. Es la capa que decide cuál es la ruta más rápida para llegar al destino a través de los **[[Router|routers]]**.

### 4. Capa de Acceso a la Red
Es la parte física. Convierte los paquetes en tramas de **[[Bits|bits]]** (ceros y unos) para que viajen por el cable de red, la fibra óptica o el **[[Wifi]]**.

---
## 📦 El proceso de "Encapsulamiento"

Para entender el funcionamiento real, pensalo como una mamushka (muñeca rusa):

* **Datos:** Tenés tu mensaje (ej: "Hola").
* **Segmento ([[TCP]]):** Metés el mensaje en una caja que dice "Este es el pedazo 1 de 10" y "Verificá que llegó bien".
* **Paquete ([[IP]]):** Metés esa caja en otra que dice "Viene de la IP 192... y va a la 200...".
* **Trama ([[Ethernet]]/[[Wifi]]):** Metés todo eso en un sobre final que tiene las direcciones físicas (**[[MAC]]**) de las placas de red.
Cuando llega a destino, el proceso se invierte (**desencapsulamiento**): se van sacando los "sobres" hasta que queda el mensaje original.

---
## ⚖️ ¿Por qué usamos los dos juntos?

Podrías usar **[[IP]]** solo (es lo que hace el protocolo **[[UDP]]**), pero los datos llegarían desordenados o incompletos. Usamos **[[TCP]]** sobre **[[IP]]** para que la comunicación sea confiable. Es el equilibrio perfecto entre "saber a dónde ir" (**[[IP]]**) y "asegurarse de llegar bien" (**[[TCP]]**).