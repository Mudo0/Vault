---
status: final
tags:
  - java
  - utn
  - backend
  - introduccion
  - programacion
created: 2026-04-07
---
# ☕ Introducción al Lenguaje [[Java]]

## 1. Características del Lenguaje

**[[Java]]** es un lenguaje de programación de alto nivel, orientado a objetos, portable y seguro. Fue lanzado en 1995 por Sun Microsystems.

- **Lenguaje de Alto Nivel**: Utiliza una sintaxis cercana al lenguaje humano, abstrayendo los detalles del hardware. Se enfoca en resolver problemas mediante estructuras y abstracciones sin gestionar directamente la memoria o instrucciones de CPU.
    
- **Portabilidad y [[JVM]]**: Los programas pueden ejecutarse en distintos sistemas operativos sin ser recompilados. Esto es posible gracias a la **Máquina Virtual de [[Java]] ([[JVM]])**, que actúa como intermediario.
    
- **Flujo de Ejecución**:
    
    1. El código fuente se escribe en archivos `.java`.
    2. El compilador (`javac`) lo convierte en **Bytecode**.
    3. La **[[JVM]]** interpreta y traduce el bytecode a instrucciones del hardware específico.

---

2. Programación Orientada a Objetos ([[P.O.O]])

Organiza el código en unidades llamadas objetos que representan entidades del mundo real.

- **Clase**: Molde o plantilla que define características y comportamientos.
- **Objeto**: Instancia concreta de una clase.
- **Encapsulamiento**: Oculta detalles internos exponiendo solo lo necesario mediante modificadores de acceso (`private`, `protected`, `public`).
- **Herencia**: Permite que una clase adquiera atributos y métodos de otra.
- **Polimorfismo**: Un mismo método puede tener diferentes comportamientos según el contexto.

---
3. [[Java]] Development Kit ([[JDK]])

Proporciona las herramientas esenciales para el desarrollo.

- **Compilador (`javac`)**: Transforma el fuente en bytecode y detecta errores de sintaxis .
- **[[JVM]]**: Interpreta el bytecode y aplica técnicas como la compilación _Just-In-Time_ (JIT) para mejorar el rendimiento.
- **Bibliotecas de Clases**: Funciones predefinidas para archivos (`java.io`), bases de datos (`java.sql`), red (`java.net`) e interfaces gráficas (`javax.swing`).
- **Herramientas**: Incluye el depurador (**JDB**), **JConsole** para monitoreo y **Javadoc** para generar documentación.
- **Empaquetamiento**: Los archivos **JAR** (_[[Java]] Archive_) agrupan clases y recursos para facilitar su distribución.
---

4. Sintaxis y Programa Mínimo

Todo programa debe estar dentro de una clase cuyo nombre coincida exactamente con el archivo (`NombreClase.java`). El punto de inicio es el método `main`.

### Reglas y Convenciones

- **Instrucciones**: Deben finalizar con punto y coma (`;`).
- **Case-sensitive**: Distingue entre mayúsculas y minúsculas.
- **Nombres**: Clases usan `CamelCase` con mayúscula inicial. Variables y métodos comienzan con minúscula. Constantes van en mayúsculas con guiones bajos.
- **Comentarios**: `//` para una línea y `/* */` para bloques.

---

5. Tipos de Datos

Existen dos categorías principales:

Tipos Primitivos

Son tipos básicos que no son objetos y almacenan directamente el valor en memoria.

- **Enteros**: `byte` (8 [[Bits|bits]]), `short` (16), `int` (32), `long` (64).
- **Flotantes**: `float` (32 [[Bits|bits]]), `double` (64).
- **Otros**: `char` (carácter Unicode 16 [[Bits|bits]]) y `boolean` (`true`/`false`).

Tipos de Referencia

Refieren a objetos creados a partir de clases y se almacenan en el **Heap**. La variable guarda la dirección de memoria.

- **[[String]]**: Es un tipo de referencia que representa una secuencia de caracteres inmutable.
- **[[String Pool]]**: Área de memoria que optimiza el uso de recursos reutilizando cadenas idénticas.
- **Fechas**: Se recomienda el uso de `LocalDate`, `LocalDateTime` y `ZonedDateTime` del paquete `java.time` .

---

6. Variables y Ámbitos

**[[Java]]** es un lenguaje tipado, requiriendo especificar el tipo de dato de cada variable.

- **Ámbitos (Scope)**:
    
    - **De Clase**: Variables de instancia únicas para cada objeto.
    - **De Método**: Variables locales accesibles solo dentro del método.
    - **De Parámetro**: Variables pasadas al llamar al método.
    - **De Bloque**: Definidas dentro de estructuras de control como `for` o `if`.
    - **Estáticas**: Asociadas a la clase (`static`), compartidas por todas las instancias.
---

7. Estructuras de Control y Operadores

- **Operadores**: Aritméticos (`+`, `-`, `*`, `/`, `%`), asignación (`=`, `+=`, etc.), comparación (`==`, `!=`, `>`, etc.) y lógicos (`&&`, `||`, `!`) .
- **Operador Ternario**: `expresion_booleana ? si_verdadero : si_falso`.
- **Selección**: `if`, `if-else` y `switch` .
- **Repetición**:
    
    - `while`: Repite mientras se cumpla la condición (0 a n veces).
    - `do-while`: Garantiza al menos una ejecución (1 a n veces).
    - `for`: Utilizado cuando la cantidad de vueltas es conocida con exactitud.
---

8. Entrada y Salida Estándar

- **Salida**: Se utiliza el objeto `System.out` con los métodos `print()` y `println()`. `println` agrega un salto de línea (`\n`) al final.
- **Entrada**: Se utiliza la clase **`Scanner`** (`java.util`).
    
    - Requiere un `import` previo a la clase.
    - Métodos comunes: `nextInt()`, `nextFloat()`, `nextLine()`, etc.