# 📑 Paginación

## 1. ¿Qué es y para qué sirve?

**¿Qué es?**
La paginación es el proceso de dividir un conjunto grande de datos en fragmentos más pequeños y manejables (páginas). En lugar de enviar toda la información de la base de datos al cliente, se envía solo lo requerido en ese momento (por ejemplo, 10 o 20 elementos).

**¿Para qué sirve?**

- **Rendimiento (Performance):** Reduce la carga en la memoria del servidor y el trabajo de la base de datos.
- **Ancho de Banda:** Envía respuestas [[JSON]] más ligeras, lo que es crucial para usuarios en redes móviles.
- **Experiencia de Usuario (UX):** La interfaz carga rápido y es más fácil de navegar.

## 🧮 2. La Lógica Matemática (Skip & Take)

En el entorno de LINQ y [[Entity Framework]] Core, la paginación se basa en dos métodos clave:

- `Skip(n)`: Omite los primeros *n* registros.
- `Take(n)`: Toma los siguientes *n* registros.

**La fórmula:**
Para obtener la página *X* con un tamaño de *Y* elementos:

> `Skip = (NumeroDePagina - 1) * TamañoDePagina`

**Ejemplo:**
Si se requiere la Página 3 y se muestran 10 ítems por página:
Se saltan los primeros 20 registros `((3-1) * 10)` y se toman los siguientes 10.

## 🛠️ 3. Implementación Paso a Paso

Para una implementación limpia y reutilizable, se evita escribir la lógica en cada controlador. Se utiliza una estructura genérica.

### Paso A: Definir el Modelo de Petición (Request)
Representa lo que el cliente envía para solicitar datos.

```csharp
public class PaginationParams
{
    private const int MaxPageSize = 50; // Protección contra abusos
    public int PageNumber { get; set; } = 1; // Valor por defecto

    private int _pageSize = 10; // Valor por defecto
    public int PageSize
    {
        get => _pageSize;
        set => _pageSize = (value > MaxPageSize) ? MaxPageSize : value;
    }
}


```
### Paso B: Definir el Modelo de Respuesta (Response)

Es el objeto que se devuelve al cliente. Se utiliza [[Programación Genérica]] (`<T>`) para que sea adaptable a diferentes entidades (Usuarios, Productos, Pedidos, etc.).



```csharp
public class PagedList<T> : List<T>
{
    public int CurrentPage { get; private set; }
    public int TotalPages { get; private set; }
    public int PageSize { get; private set; }
    public int TotalCount { get; private set; }

    public bool HasPrevious => CurrentPage > 1;
    public bool HasNext => CurrentPage < TotalPages;

    public PagedList(List<T> items, int count, int pageNumber, int pageSize)
    {
        TotalCount = count;
        PageSize = pageSize;
        CurrentPage = pageNumber;
        TotalPages = (int)Math.Ceiling(count / (double)pageSize);

        AddRange(items); // Agrega los elementos a la lista
    }

    // Método estático para crear la página desde la base de datos
    public static async Task<PagedList<T>> CreateAsync(IQueryable<T> source, int pageNumber, int pageSize)
    {
        // 1. Contar total de registros (antes de paginar)
        var count = await source.CountAsync(); 
        
        // 2. Aplicar Skip y Take para traer solo los datos necesarios
        var items = await source.Skip((pageNumber - 1) * pageSize)
                                .Take(pageSize)
                                .ToListAsync();

        return new PagedList<T>(items, count, pageNumber, pageSize);
    }
}
```

### Paso C: Usarlo en el Controlador (Controller)

Ejemplo de implementación en una [[API]] utilizando un controlador de productos.

```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly ApplicationDbContext _context;

    public ProductsController(ApplicationDbContext context)
    {
        _context = context;
    }

    [HttpGet]
    public async Task<ActionResult<IEnumerable<Product>>> GetProducts([FromQuery] PaginationParams paginationParams)
    {
        // Preparamos la query (aún no se ejecuta en BD)
        var query = _context.Products.AsQueryable();

        // Podrías agregar filtros aquí, ej:
        // query = query.Where(p => p.Price > 0);

        // Ejecutamos la paginación
        var pagedProducts = await PagedList<Product>.CreateAsync(
            query, 
            paginationParams.PageNumber, 
            paginationParams.PageSize
        );

        // Agregamos metadata al header (opcional, pero útil para el frontend)
        var metadata = new
        {
            pagedProducts.TotalCount,
            pagedProducts.PageSize,
            pagedProducts.CurrentPage,
            pagedProducts.TotalPages,
            pagedProducts.HasNext,
            pagedProducts.HasPrevious
        };

        Response.Headers.Add("X-Pagination", System.Text.Json.JsonSerializer.Serialize(metadata));

        return Ok(pagedProducts);
    }
}
```

## 🔄 4. Resumen Visual del Flujo

1. **Cliente:** Realiza petición `GET /api/products?pageNumber=2&pageSize=5`.
    
2. **[[API]]:** Recibe los parámetros.
    
3. **[[Entity Framework]] Core:**
    
    - Ejecuta `SELECT COUNT(*)` para obtener el total (ej: 100).
        
    - Calcula el salto: `(2-1) * 5 = 5`.
        
    - Ejecuta `SELECT * ... OFFSET 5 ROWS FETCH NEXT 5 ROWS ONLY` (sintaxis SQL Server).
        
4. **API:** Empaqueta los 5 productos + la metadata (TotalPages: 20).
    
5. **Cliente:** Recibe los datos y confirma que existen más páginas disponibles.
    

## 📌 5. Consideraciones Importantes

- **Ordenamiento (OrderBy):** Siempre se debe usar un `OrderBy` antes de hacer `Skip`. Sin esto, la base de datos no garantiza el orden y podrían aparecer datos repetidos o saltados entre páginas.
    
    - _Correcto:_ `query.OrderBy(p => p.Id).Skip(...).Take(...)`
        
- **Rendimiento en Tablas Gigantes:** Si existen millones de registros, `CountAsync()` puede ser lento. En escenarios de Big Data, ocasionalmente se utiliza "paginación por cursor" (basada en el ID del último elemento visto) en lugar de "paginación por offset", aunque la implementación mostrada cubre la mayoría de los casos de uso empresarial.
    
- **Metadata:** Es buena práctica devolver la metadata (número total de páginas) para que el Frontend determine si dibujar el botón de "Siguiente". Puede devolverse en los Headers (como en el ejemplo) o envolver la respuesta en un objeto JSON tipo `{ "data": [...], "meta": {...} }`.