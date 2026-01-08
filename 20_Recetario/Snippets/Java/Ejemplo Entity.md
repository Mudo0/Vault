```java
import jakarta.persistence.*; // En Spring Boot 3 es Jakarta, no Javax
import lombok.Data;

@Data // Lombok genera getters/setters
@Entity // Indica que esto es una tabla
@Table(name = "usuarios") // Opcional: si quieres que la tabla se llame diferente a la clase
public class Usuario {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // IMPORTANTE para SQL Server
    private Long id;

    @Column(nullable = false, length = 100)
    private String nombre;

    @Column(unique = true)
    private String email;
    
    // Spring convertirá camelCase a snake_case automáticamente en la DB
    // private String fechaNacimiento  --> columna: fecha_nacimiento
}

```