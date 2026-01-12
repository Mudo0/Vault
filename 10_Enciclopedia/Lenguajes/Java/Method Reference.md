---
status: final
tags:
  - java
  - sintaxis
  - funcional
  - clean-code
  - lambda
created: 2026-01-11
---
# 🔗 Referencias de Método ([[Java]])

Introducidas en **[[Java]]** 8, las referencias de método funcionan como "azúcar sintáctico" para una **[[Lambda Expression]]**. Su propósito es simplificar el código, haciéndolo más limpio y legible.

Se utilizan cuando una **[[Lambda Expression]]** no realiza otra acción más que invocar a un método existente. En lugar de escribir el cuerpo completo de la invocación, se hace referencia al método por su nombre.

* **Sintaxis:** Se emplea el operador de doble dos puntos `::`.
    > `NombreClase::nombreMetodo`
* **Regla de oro:** Su uso es válido únicamente cuando los argumentos recibidos por la **[[Lambda Expression]]** son pasados exactamente en el mismo orden al método invocado.

---

## 4️⃣ Tipos de Referencias

Para comprender su aplicación, es útil visualizar su traducción desde una **[[Lambda Expression]]** estándar:

| Tipo de Referencia | Sintaxis | Expresión [[Lambda Expression]] equivalente |
| :--- | :--- | :--- |
| **1. Método Estático** | `Clase::metodoStatic` | `(args) -> Clase.metodoStatic(args)` |
| **2. Instancia (Objeto específico)** | `instancia::metodo` | `(args) -> instancia.metodo(args)` |
| **3. Instancia (Tipo arbitrario)** | `Clase::metodo` | `(arg0, rest) -> arg0.metodo(rest)` |
| **4. Constructor** | `Clase::new` | `(args) -> new Clase(args)` |

---

## 👨‍💻 Ejemplos Prácticos

A continuación se presentan casos reales utilizando una lista de nombres:
`List<String> nombres = Arrays.asList("Carlos", "Ana", "Beatriz", "David");`

### 1. Referencia a un Método Estático
Objetivo: Convertir números a String.
* **Lambda:** `(x) -> String.valueOf(x)`
* **Referencia:** `String::valueOf`

```java
List<Integer> numeros = Arrays.asList(1, 2, 3);

// Lambda clásica
numeros.stream().map(n -> String.valueOf(n)); 

// Referencia de Método
numeros.stream().map(String::valueOf); 
```

### 2. Referencia a un Método de Instancia (Objeto Específico)

Se invoca un método de un objeto existente fuera de la Lambda (ej. `System.out`).

- **Lambda:** `nombres.forEach(n -> System.out.println(n))`
- **Referencia:** `System.out::println`

```java
// El objeto "out" existe dentro de la clase System
nombres.forEach(System.out::println);
```
### 3. Referencia a un Método de Instancia (Tipo Arbitrario)

El método se invoca sobre el _primer parámetro_ de la Lambda.

- **Lambda:** `(a, b) -> a.compareToIgnoreCase(b)`
- **Referencia:** `String::compareToIgnoreCase`

```java
// Java infiere que "compareToIgnoreCase" debe ejecutarse sobre el 
// primer elemento (a) pasando el segundo (b) como argumento.
nombres.sort(String::compareToIgnoreCase);
```

### 4. Referencia a un Constructor

Utilizado frecuentemente para crear nuevos objetos o colecciones al finalizar un **[[Stream]]**.

- **Lambda:** `() -> new ArrayList<>()`
- **Referencia:** `ArrayList::new`

```java
// Crear una nueva lista a partir de un Stream
List<String> copia = nombres.stream()
                            .collect(Collectors.toCollection(ArrayList::new));
```

---

## 🆚 Comparativa Visual

Supongamos la conversión de una lista de nombres a mayúsculas.

**Opción A (Lambda clásica):**

```java
nombres.stream()
       .map(s -> s.toUpperCase()) // "s" es el parámetro, se llama al método sobre "s"
       .collect(Collectors.toList());
```

**Opción B (Referencia de Método):**

```java
nombres.stream()
       .map(String::toUpperCase)  // Más conciso, aplica a cada elemento
       .collect(Collectors.toList());
```

---

## ⚠️ ¿Cuándo NO usarla?

Aunque aportan limpieza al código, no deben forzarse si comprometen la claridad o la funcionalidad. No se pueden utilizar si:

1. **Manipulación de argumentos:** Se requiere modificar los datos antes de pasarlos.
    
    - _Ejemplo:_ `x -> metodo(x + 1)` (No tiene traducción directa).
        
2. **Ambigüedad:** El nombre del método es poco descriptivo sin visualizar los parámetros explícitos.