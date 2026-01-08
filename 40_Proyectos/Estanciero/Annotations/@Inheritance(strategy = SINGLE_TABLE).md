---
status: borrador
tags:
  - java
  - jpa
  - hibernate
  - backend
  - bases-de-datos
created: 2026-01-08
---

# 🧬 Estrategia de Herencia: SINGLE_TABLE ([[JPA]])

La anotación `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)` es fundamental al trabajar con **[[JPA]]** (Java Persistence API) e **[[Hibernate]]** en **[[Spring Boot]]** para manejar la herencia de clases.

---

## ⚙️ ¿Qué hace esta anotación?

En la **[[P.O.O]]**, es común tener una clase padre y varias clases hijas (herencia). Sin embargo, las bases de datos relacionales no comprenden la herencia de forma nativa; operan mediante tablas.

Esta anotación instruye a **[[JPA]]**: "Tomar toda la jerarquía de clases (padre e hijas) y almacenarla en una sola tabla en la base de datos".

### Funcionamiento de la estrategia

1.  **Una sola tabla unificada:** Se crea una única tabla que contiene las columnas de la clase padre más todas las columnas de todas las clases hijas.
2.  **Columnas nulas:** Si una clase hija posee una propiedad que otra hija no tiene, dicha columna permanecerá como `NULL` para las filas que no correspondan.
3.  **Columna Discriminadora:** **[[JPA]]** agrega automáticamente una columna extra (usualmente llamada `DTYPE`) para identificar a qué clase pertenece cada fila (por ejemplo, si es un `Coche` o una `Moto`).

---

## 👨‍💻 Ejemplo Visual

Se plantea la siguiente jerarquía en **[[Java]]**:
* `Vehiculo` (Padre)
* `Auto` (Hija: tiene `cantidadPuertas`)
* `Moto` (Hija: tiene `tieneSidecar`)

### 1. El código [[Java]]

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE) // <--- Estrategia de tabla única
@DiscriminatorColumn(name = "tipo_vehiculo") // Opcional: personaliza el nombre del discriminador
public class Vehiculo {
    @Id
    private Long id;
    private String marca;
}

@Entity
@DiscriminatorValue("AUTO") // Valor para la columna discriminadora
public class Auto extends Vehiculo {
    private int cantidadPuertas;
}

@Entity
@DiscriminatorValue("MOTO")
public class Moto extends Vehiculo {
    private boolean tieneSidecar;
}
```

### 2. La tabla resultante en Base de Datos

**[[JPA]]** generará una sola tabla llamada `Vehiculo` con la siguiente estructura:

|**ID**|**TIPO_VEHICULO**|**MARCA**|**CANTIDAD_PUERTAS**|**TIENE_SIDECAR**|
|---|---|---|---|---|
|1|AUTO|Toyota|4|NULL|
|2|MOTO|Yamaha|NULL|false|
|3|AUTO|Ford|2|NULL|

> **Nota:** Las propiedades exclusivas de una clase (`cantidadPuertas` o `tieneSidecar`) quedan como `NULL` cuando no aplican al tipo de registro.

---

## ⚖️ Ventajas y Desventajas

Esta es la estrategia por defecto de **[[JPA]]** si no se especifica otra.

|**Ventajas**|**Desventajas**|
|---|---|
|**Rendimiento Alto:** Es la más rápida porque no requiere realizar `JOINs` entre tablas para recuperar datos. Todo reside en un mismo lugar.|**Integridad de Datos:** No es posible establecer restricciones `NOT NULL` en las columnas de las clases hijas, ya que deben permitir nulos para las otras clases hermanas.|
|**Simplicidad:** La consulta e inserción de datos es directa (una sola tabla).|**Tamaño de Tabla:** Si existen muchas subclases con campos distintos, la tabla crece en anchura y contiene múltiples espacios vacíos (_sparse table_).|

---

## ✅ ¿Cuándo utilizarla?

- Cuando la jerarquía de clases es simple.
- Cuando el rendimiento es un factor crítico y se desea evitar `JOINs`.
- Cuando las subclases comparten la mayoría de los atributos y poseen pocos atributos propios distintos.