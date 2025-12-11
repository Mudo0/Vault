---
status: final
tags:
  - conceptos
  - arquitectura
  - web
created: 2025-12-10
---
# 🔗 ¿Qué es una API?

**API** (Interfaz de Programación de Aplicaciones) es un conjunto de definiciones y protocolos utilizados para desarrollar e integrar software de aplicaciones. Permite que dos sistemas dispares se comuniquen entre sí, estableciendo las reglas sobre cómo una aplicación puede solicitar servicios o datos a otra.

Actúan como intermediarios, abstrayendo la complejidad del sistema subyacente y exponiendo solo los puntos de acceso necesarios para el usuario o desarrollador externo.

---

## 💡 Explicación simplificada

Para comprender el funcionamiento de una [[API]], resulta útil la analogía de un **Restaurante**:

- **El Cliente (Usuario/Aplicación):** Requiere un servicio o dato, pero no tiene acceso directo a la lógica interna ni a la estructura de almacenamiento.
    
- **La Cocina (Servidor/Base de Datos):** Lugar donde se procesan los datos y se ejecuta la lógica compleja.
    
- **El Camarero (La API):** Es el intermediario crítico. El cliente entrega el pedido al camarero (realiza una "petición"), este traslada la orden a la cocina, aguarda la respuesta y entrega el resultado (los datos) al cliente.
    

No es necesario conocer el proceso de preparación del chef; basta con saber qué solicitar al camarero. Del mismo modo, una aplicación no requiere conocer el funcionamiento interno de un servidor, solo necesita utilizar la interfaz para realizar la consulta.

---

## 🌐 Tipos comunes de Web APIs

Aunque existen diversas arquitecturas, en el desarrollo web moderno predominan:

- **[[REST]] (Representational State Transfer):** La más popular actualmente. Utiliza el protocolo [[HTTP]] estándar y suele intercambiar datos en formato [[JSON]].
    
- **[[SOAP]] (Simple Object Access Protocol):** Un protocolo más antiguo y estricto, basado en XML, común en sistemas empresariales financieros o legacy.