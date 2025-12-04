# ¿Qué es una API?

**API** (Interfaz de Programación de Aplicaciones) es un conjunto de definiciones y protocolos que se utiliza para desarrollar e integrar el software de las aplicaciones. Permite que dos sistemas de software dispares se comuniquen entre sí, estableciendo las reglas de cómo una aplicación puede solicitar servicios o datos a otra.

Actúan como intermediarios, abstrayendo la complejidad del sistema subyacente y exponiendo solo los puntos de acceso necesarios para el usuario o desarrollador externo.

---

## Explicación simplificada

Para entender una API, es útil usar la analogía de un **Restaurante**:

- **El Cliente (Tú/Tu App):** Quieres comida, pero no puedes ir a la cocina a prepararla tú mismo ni sabes cómo está organizada la despensa.
- **La Cocina (El Servidor/Base de Datos):** Es donde se preparan los datos y ocurre la lógica compleja.
- **El Camarero (La API):** Es el intermediario crítico. Tú le das tu pedido al camarero (haces una "petición"), él lleva ese pedido a la cocina, espera la respuesta y te trae la comida (los datos) a la mesa.

Tú no necesitas saber cómo cocina el chef, solo necesitas saber qué pedirle al camarero. Del mismo modo, una app no necesita saber cómo funciona el servidor del banco, solo necesita usar la API para consultar el saldo.

---

## Tipos comunes de Web APIs

Aunque existen muchas arquitecturas, en el desarrollo web moderno predominan:

- **[[REST]] (Representational State Transfer):** La más popular actualmente. Utiliza el protocolo [[HTTP]] estándar y suele intercambiar datos en formato [[JSON]].
- **SOAP (Simple Object Access Protocol):** Un protocolo más antiguo y estricto, basado en XML, común en sistemas empresariales financieros o legacy.