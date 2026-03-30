---
status: final
tags:
  - redes
  - protocolos
  - ipv4
  - internet
created: 2026-03-30
---
# 🌐 [[IPv4]] (Internet Protocol version 4)
## 1. 🔍 ¿Qué es exactamente una dirección IPv4?

Una dirección **[[IPv4]]** es un número de **32 [[Bits|bits]]** que identifica de forma única a un dispositivo (PC, smartphone, servidor, cafetera inteligente) en una **[[Red]]**.

Para que sea fácil de leer para nosotros los humanos, se escribe en **notación decimal con puntos**. Se divide en cuatro grupos de números (llamados octetos) que van del 0 al 255.

* **Ejemplo:** `192.168.1.15` o `8.8.8.8` (el famoso **[[DNS]]** de Google).

### Características clave:
* **Capacidad:** Permite un total de aproximadamente 4,300 millones de direcciones únicas ($2^{32}$).
* **Agotamiento:** Aunque suene a mucho, ¡ya se acabaron! Por eso ahora usamos tecnologías como **[[NAT]]** o el nuevo protocolo **[[IPv6]]** (que tiene muchísimas más direcciones).

---
## 2. ⚙️ ¿Cómo se utiliza?
El **[[IPv4]]** cumple dos funciones principales en el mundo digital: **Identificación** y **Localización**.
### A. Identificación de dispositivos
Sin una **[[IP]]**, el **[[Router]]** no sabría a quién enviarle los datos. Si tú y tu hermano están viendo videos diferentes en la misma red **[[Wifi]]**, el router usa las **[[IP|IPs]]** internas para que el video de gatitos no termine en la pantalla de quien está estudiando álgebra.

### B. Enrutamiento de paquetes
Cuando envías un mensaje, este se divide en "paquetes". Cada paquete lleva una etiqueta con la **[[IP]]** de origen (la tuya) y la **[[IP]]** de destino. Los **[[Router|routers]]** en el camino leen esa etiqueta y deciden cuál es la ruta más rápida para que llegue a su destino.

---
## 🏢 3. Direcciones Públicas vs. Privadas

Para estirar la vida del **[[IPv4]]**, se crearon dos tipos de direcciones:

| Tipo           | ¿Para qué sirve?                                                                                                                                          | Ejemplo                                    |               |
| :------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------- | ------------- |
| **IP Privada** | Se usa dentro de tu casa u oficina. Tu celular y tu laptop tienen **[[IP                                                                                  | IPs]]** diferentes dentro de tu red local. | `192.168.x.x` |
| **IP Pública** | Es la dirección que el mundo ve. Tu **[[Router]]** tiene una sola **[[IP]]** pública que representa a todos los dispositivos de tu casa ante el internet. | `201.185.x.x`                              |               |

---
## 💡 Un detalle curioso...

Como las direcciones **[[IPv4]]** se agotaron oficialmente hace años, hoy vivimos en una era de transición. Si entras a la configuración de tu **[[Router]]**, probablemente verás una dirección **[[IPv4]]** (corta y numérica) y una **[[IPv6]]** (larga, con letras y números como `2001:0db8:85a3...`). Ambas conviven para que el internet no colapse.