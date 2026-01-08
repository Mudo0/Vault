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
# 🔌 @JoinColumn vs mappedBy ([[JPA]])

En el manejo de relaciones bidireccionales con **[[JPA]]**, la configuración de `@JoinColumn` resulta necesaria (o altamente recomendable), ya que el atributo `mappedBy` del lado inverso depende de que esta definición exista.

A continuación se detalla el funcionamiento y la interacción entre ambos elementos.

---

## 1. 🔑 ¿Qué hace @JoinColumn?

Esta anotación es la responsable de crear la columna física en la base de datos.

Instruye a **[[Hibernate]]**: "En la tabla de esta entidad (ej. `Box`), crear una columna llamada `board_id` que actuará como Llave Foránea (*Foreign Key*)". Dicha columna contendrá el ID de la entidad padre (`Board`) a la que pertenece el registro.

---

## 2. 🔗 Relación con mappedBy

Aunque exista un `mappedBy` en la entidad padre, se requiere `@JoinColumn` porque `mappedBy` no genera columnas, sino que proporciona instrucciones lógicas.

En una relación Uno a Muchos (Un tablero, muchas casillas):

* **Lado Dueño (*Owning Side*):** Es la clase hija (`Box`) donde se coloca el `@ManyToOne`. Es el lado que posee la llave foránea en la base de datos.
* **Lado Inverso (*Inverse Side*):** Es la clase padre (`Board`) donde se coloca el `@OneToMany`.

Al definir `mappedBy = "board"` en la clase `Board`, se indica a **[[JPA]]**:
> "Esta entidad (`Board`) no gestiona la llave foránea de la relación. Para conocer la unión, se debe consultar la clase `Box` y revisar el atributo llamado `board`."

En consecuencia, **[[JPA]]** se dirige a la clase `Box`, localiza el atributo `board` y busca la anotación `@JoinColumn` para determinar qué columna de la base de datos utilizar para unir las tablas.

---

## 3. ⚠️ ¿Qué sucede si se omite @JoinColumn?

Si se elimina la anotación, el código seguirá funcionando, pero se perderá control sobre el nombre de la columna física.

**[[JPA]]** aplicará su estrategia de nomenclatura por defecto, que usualmente sigue el patrón: `nombreDelAtributo_id`.
* *Caso con default:* Si el atributo se llama `board`, se creará `board_id`.
* *Caso con otro nombre:* Si el atributo fuese `tableroJuego`, se crearía `tableroJuego_id`.

> **Recomendación:** Se sugiere utilizar siempre `@JoinColumn`. Es preferible ser explícito y definir el nombre exacto de la columna en la base de datos (ej. `board_id`), en lugar de depender de las deducciones automáticas de **[[Hibernate]]**.

---

## 📝 Resumen de Implementación

* **En Padre (`Board`):** `mappedBy` es obligatorio para evitar la creación de tablas intermedias innecesarias. Indica que la otra clase gestiona la relación.
* **En Hija (`Box`):** `@JoinColumn` define el nombre real de la columna en la tabla SQL donde se almacenará la referencia (ID).