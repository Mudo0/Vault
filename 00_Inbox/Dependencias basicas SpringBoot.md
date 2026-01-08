Para armar un stack sólido con Spring Boot y SQL Server, estas son las dependencias que deberías seleccionar en el asistente de IntelliJ (Initializr).

Las he dividido en **Esenciales** (sin esto no arranca) y **Productividad** (muy recomendadas para no sufrir escribiendo código repetitivo).

### 1. Las Esenciales (El "Core")

Busca y marca estas opciones en el wizard:

- **Spring Web** (`spring-boot-starter-web`)
    
    - **¿Qué hace?**: Incluye Tomcat (servidor) y el modelo MVC.1 Es lo que te permite crear los Controllers y exponer endpoints REST.
        
- **Spring Data JPA** (`spring-boot-starter-data-jpa`)
    
    - **¿Qué hace?**: Es la capa de acceso a datos.2 Usa **Hibernate** por debajo para mapear tus clases Java a tablas de SQL Server automáticamente.3 Te ahorrará escribir queries SQL manuales para operaciones básicas (CRUD).
        
- **MS SQL Server Driver** (`mssql-jdbc`)
    
    - **¿Qué hace?**: Es el conector oficial de Microsoft. Sin esto, la aplicación no sabrá cómo "hablar" el idioma de tu base de datos SQL Server.
        

### 2. Las de Productividad (Altamente Recomendadas)

- **Lombok** (`lombok`)
    
    - **¿Por qué?**: En Java, las clases de modelo suelen llenarse de código "basura" (Getters, Setters, Constructores, `toString`). Con Lombok, pones una anotación (`@Data`) y él genera todo eso automáticamente al compilar. Mantiene tu código limpio.
        
- **Spring Boot DevTools** (`spring-boot-devtools`)
    
    - **¿Por qué?**: "Hot Reload". Si haces un cambio en el código y guardas, reinicia el servidor automáticamente y muy rápido. Sin esto, tendrás que detener y volver a ejecutar la app manualmente por cada cambio pequeño (un dolor de cabeza).
        

---

### Configuración Necesaria (El "Connection String")

Una vez creado el proyecto, Spring Boot intentará conectarse a la base de datos al arrancar y fallará porque no sabe **dónde** está tu SQL Server.

Tienes que ir al archivo `src/main/resources/application.properties` y agregar esto:

Properties

```java
# Conexión a SQL Server (ajusta tu base de datos, usuario y password)
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=NombreDeTuBaseDeDatos;encrypt=true;trustServerCertificate=true;
spring.datasource.username=sa
spring.datasource.password=TuPasswordFuerte123

# Para que Hibernate actualice la estructura de tablas automáticamente
spring.jpa.hibernate.ddl-auto=update

# Opcional: Para ver las queries SQL en la consola (útil para depurar)
spring.jpa.show-sql=true
```

**Nota sobre `encrypt` y `trustServerCertificate`:** En las versiones nuevas del driver de SQL Server, la encriptación viene activada por defecto. Si estás en un entorno local de desarrollo (localhost), suele dar error de certificados SSL, por eso ponemos `trustServerCertificate=true` en la URL.
