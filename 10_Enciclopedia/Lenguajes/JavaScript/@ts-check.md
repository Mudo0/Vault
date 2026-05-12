---
status: final
tags:
  - javascript
  - typescript
  - tooling
  - calidad-codigo
  - vscode
created: 2026-04-21
---
# 🛡️ Directiva `// @ts-check`

La directiva **`// @ts-check`** es una herramienta increíblemente útil si trabajas con **[[JavaScript]]** pero quieres la seguridad y las ayudas que ofrece **[[TypeScript]]** sin necesidad de cambiar la extensión de tus archivos a `.ts`.

---

## 🔍 1. ¿Qué es exactamente?

**`// @ts-check`** es un comentario especial que se coloca en la primera línea de un archivo **[[JavaScript]]**. Su función es indicarle al editor (especialmente a **Visual Studio Code**) que debe activar el motor de análisis de **[[TypeScript]]** para ese archivo específico.

Normalmente, **[[JavaScript]]** es muy permisivo y no te avisa si intentas acceder a una propiedad que no existe o si pasas un número donde se esperaba un texto. Al añadir esta línea, el editor empezará a marcar errores con el famoso "subrayado rojo".



---

## 🛠️ 2. ¿Para qué sirve?

* **Detección de errores en tiempo real:** Te avisa si escribiste mal el nombre de una variable o si estás llamando a una función con argumentos incorrectos.
* **Mejorar el Autocompletado (IntelliSense):** Al entender los tipos de datos, el editor te sugerirá métodos y propiedades con mucha más precisión.
* **Documentación con [[JSDoc]]:** Se integra perfectamente con los comentarios **[[JSDoc]]** para definir tipos complejos.

### Ejemplo práctico

**Sin `@ts-check` (JavaScript normal):**
```javascript
function saludar(nombre) {
    console.log("Hola " + nombre.toUpperCase());
}

saludar(42); // El código falla en ejecución: "nombre.toUpperCase is not a function"
```

**Con `@ts-check`:**



```js
// @ts-check
/** @param {string} nombre */
function saludar(nombre) {
    console.log("Hola " + nombre.toUpperCase());
}

saludar(42); // ¡ERROR! El editor avisa: "Argument of type 'number' is not assignable to parameter of type 'string'."
```

---

## 🚀 3. ¿Cuándo deberías utilizarlo?

No siempre es necesario migrar todo un proyecto a **[[TypeScript]]**. Aquí es donde brilla esta directiva:

- **Proyectos Legados:** Si tienes un proyecto JS antiguo y grande, puedes ir añadiendo `@ts-check` archivo por archivo para limpiarlo de errores.
- **Scripts Rápidos o Prototipos:** Cuando creas un archivo `.js` pequeño para automatizar algo y no quieres configurar un compilador de **[[TypeScript]]** (`tsconfig.json`, build steps, etc.).
- **Librerías en Vanilla JS:** Si estás desarrollando una biblioteca que debe ser distribuida en JS puro, pero quieres mantener la calidad del código.
- **Aprendizaje Gradual:** Una forma excelente de empezar a usar conceptos de tipado sin abandonar la comodidad de **[[JavaScript]]**.

---

## 📊 4. Comparativa rápida

|**Característica**|**JavaScript puro**|**JS con @ts-check**|**TypeScript (.ts)**|
|---|---|---|---|
|**Detección de errores**|Muy básica|Alta (vía **[[JSDoc]]**)|Máxima|
|**Configuración**|Ninguna|Solo una línea|Requiere `tsconfig.json`|
|**Compilación**|No requiere|No requiere|Necesita transpilación|
|**Sintaxis de tipos**|No existe|Comentarios **[[JSDoc]]**|Nativa de TS|

> [!TIP]
> 
> Si quieres activar el chequeo de tipos en todos tus archivos **[[JavaScript]]** sin escribir la línea en cada uno, activa en la configuración de **VS Code** la opción: `JS/TS › Implicit Project Config: Check JS`.


