---
status: borrador
tags:
  - java
  - lombok
  - jpa
  - spring-boot
  - buenas-practicas
  - errores
created: 2026-01-08
---

# 🚫 @ToString.Exclude y [[Lombok]] en [[JPA]]

El uso incorrecto de **[[Lombok]]** junto con **[[JPA]]** constituye una de las causas más frecuentes de errores "silenciosos" y caídas de rendimiento en aplicaciones **[[Spring Boot]]**.

La anotación `@ToString.Exclude` se utiliza para evitar que un campo específico aparezca en el método `toString()` que **[[Lombok]]** genera automáticamente.

---

## 1. ⚠️ El Problema: ¿Por qué es necesaria?

Si se utilizan anotaciones como `@Data` o `@ToString` en entidades **[[JPA]]** sin excluir ciertas relaciones, surgen dos problemas graves:

### A. Error de Recursión Infinita (`StackOverflowError`)
Es el escenario más común en relaciones bidireccionales.
1.  La Entidad A posee una lista de B.
2.  La Entidad B posee una referencia a A.
3.  Al llamar a `A.toString()`, intenta imprimir a B.
4.  Al imprimir a B, intenta imprimir a A.
5.  **Resultado:** Un bucle infinito que colapsa la aplicación.

### B. Problema de Carga Perezosa (`LazyInitializationException`)
Por defecto, las relaciones `@OneToMany` son *Lazy* (perezosas), lo que significa que los datos no se recuperan de la base de datos hasta que se solicitan.
* Si el método `toString()` intenta imprimir una lista de 1,000 registros asociados.
* **[[Hibernate]]** se ve forzado a realizar una consulta en ese momento para recuperar esos datos solo para imprimirlos en consola.
* **Resultado:**
    * Si la transacción se cerró: `LazyInitializationException` (fallo de la app).
    * Si la transacción sigue abierta: Degradación de rendimiento (problema N+1 queries).

---

## 2. 🛠️ La Solución: ¿Cuándo usarla?

Se debe aplicar `@ToString.Exclude` en los siguientes escenarios dentro de las entidades **[[JPA]]**:

### Escenario 1: En colecciones (`@OneToMany`, `@ManyToMany`)
Es imperativo excluir las listas o sets de las entidades padres.

```java
@Entity
@Data // Incluye @ToString implícitamente
public class Usuario {
    @Id
    private Long id;
    
    private String nombre;

    // ❌ PELIGRO: Su impresión provoca recursión o queries masivas
    @OneToMany(mappedBy = "usuario", fetch = FetchType.LAZY)
    @ToString.Exclude // ✅ SOLUCIÓN: Ignora este campo al imprimir
    private List<Pedido> pedidos; 
}

```
### Escenario 2: En la contraparte (`@ManyToOne`)

Para romper el ciclo bidireccional, se debe cortar la cadena en al menos uno de los lados (idealmente en ambos para mantener los logs limpios).


```Java

@Entity
@Data
public class Pedido {
    @Id
    private Long id;
    
    private String descripcion;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "usuario_id")
    @ToString.Exclude // ✅ SOLUCIÓN: Evita volver a imprimir al Usuario completo
    private Usuario usuario;
}
```

### Escenario 3: Campos sensibles o extensos

Si existe un campo `@Lob` (como una imagen en Base64 o un PDF binario) o una contraseña encriptada, se debe excluir para evitar saturar los logs.

---

## 📊 Estrategia de Decisión

|**Tipo de Relación**|**¿Usar @ToString.Exclude?**|**Razón Principal**|
|---|---|---|
|**@OneToMany (Listas)**|**SÍ** (Casi siempre)|Evitar cargar listas enormes (_Lazy_) y recursión.|
|**@ManyToOne (Padre)**|**SÍ** (Recomendado)|Romper el ciclo de recursión infinita.|
|**@OneToOne**|**DEPENDE**|Si es bidireccional, excluir en un lado.|
|**Campos Primitivos**|**NO**|Son seguros de imprimir (`String`, `Long`, `int`).|

---

## 🛡️ Alternativa: `@ToString(onlyExplicitlyIncluded = true)`

En lugar de excluir lo no deseado (lista negra), muchos arquitectos prefieren incluir solo lo necesario (lista blanca). Este enfoque es más seguro por defecto.

Java

```java
@Entity
@Getter @Setter
@ToString(onlyExplicitlyIncluded = true) // 1. Nada se imprime por defecto
public class Producto {
    
    @Id
    @ToString.Include // 2. Solo se incluye explícitamente el ID
    private Long id;
    
    @ToString.Include // 3. Y el nombre
    private String nombre;
    
    @ManyToOne
    // No tiene @ToString.Include, por lo que se ignora automáticamente.
    private Categoria categoria; 
}
```

> **Nota:** Este mismo conflicto de recursión y rendimiento ocurre con los métodos `equals()` y `hashCode()`, lo cual puede afectar el funcionamiento de `Set` o `HashMap` en **[[JPA]]**.