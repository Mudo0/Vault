---
status: final
tags:
  - redes
  - protocolos
  - ipv6
  - internet
  - iot
created: 2026-03-30
---
# 🌐 [[IPv6]] (Internet Protocol version 6)

## 1. 🚀 ¿Por qué nació IPv6? (El problema del espacio)

Antes usábamos (y seguimos usando mucho) el **[[IPv4]]**. El problema es que **[[IPv4]]** solo permite unos 4.300 millones de direcciones. Con el auge de los smartphones, tablets, relojes inteligentes y hasta heladeras conectadas, ¡se agotaron las direcciones!

**[[IPv6]]** llegó para rescatarnos con un espacio casi infinito. Mientras que **[[IPv4]]** usa 32 **[[Bits|bits]]**, **[[IPv6]]** usa 128 **[[Bits|bits]]**.

> **Dato curioso:** **[[IPv6]]** permite $2^{128}$ direcciones. Eso es un 34 seguido de 37 ceros. Hay suficientes direcciones para asignarle miles de millones a cada grano de arena en la Tierra.

---
## ⚖️ 2. Diferencias clave: IPv4 vs. IPv6

| Característica | [[IPv4]] | [[IPv6]] |
| :--- | :--- | :--- |
| **Formato** | Numérico (Ej: `192.168.1.1`) | Alfanumérico/Hexadecimal (Ej: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`) |
| **Longitud** | 32 **[[Bits|bits]]** | 128 **[[Bits|bits]]** |
| **Seguridad** | Opcional (añadida después) | Diseñado con seguridad (**[[IPsec]]**) integrada |
| **Configuración** | Manual o por **[[DHCP]]** | Autoconfiguración automática (*Plug & Play*) |

---
## ✨ 3. Ventajas de usar IPv6

El protocolo es más inteligente y ofrece beneficios directos:

* **Adiós al [[NAT]]:** Como hay tantas direcciones, ya no necesitamos que muchos dispositivos "se escondan" detrás de una sola **[[IP]]** pública. Cada dispositivo puede tener su **[[IP]]** global real.
* **Mayor eficiencia:** Los **[[Router|routers]]** procesan los paquetes de datos más rápido porque el "encabezado" de la información es más simple y organizado.
* **Mejor para el [[IoT]]:** Es fundamental para el "**Internet de las Cosas**". Desde sensores en campos de cultivo hasta ciudades inteligentes, todo necesita una **[[IP]]** propia para funcionar bien.
* **Seguridad nativa:** **[[IPv6]]** fue creado pensando en el cifrado y la autenticación, lo que hace que las comunicaciones sean más seguras desde la base.

---
## ⏳ 4. ¿Por qué no lo usamos para todo todavía?

Cambiar el internet entero es como intentar cambiar las ruedas de un auto mientras vas a 120 km/h por la autopista. Muchos equipos viejos no lo entienden, por lo que hoy en día coexistimos con ambos sistemas (esto se llama **[[Dual Stack]]**).