
Proyecto Aplicación web To Do List.

## Backend


-diagrama de la estructura-

### Base Classes

#### User
-----

```c#
 public class User
 {
     public int Id { get; set; }

     public string Username { get; set; }

     public string Email { get; set; }

     public string PasswordHash { get; set; }
	
	//navigation key for the DbContext
     public ICollection<ToDo> ToDos { get; set; }
 }
```
-----

#### TodoItem
----
```c#
public class ToDo
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }
    public bool IsCompleted { get; set; }
    public DateTime CreatedAt { get; set; }
    
    ///////Properties for Entity framework
    
    //foreign key for the progress table
	    public int ProgressId { get; set; }
    //navigation key for the DbContext
    public ToDoProgress Progress { get; set; }

    //foreign key for the user table
    public int UserId { get; set; }

    //navigation key for the DbContext
    public User User { get; set; }
}
```

- Progress tracking class
```c#
	public class ToDoProgress
{
    public int Id { get; set; }
    public string Progress { get; set; }
	
	//navigation key for the DbContext
    public ICollection<ToDo> ToDos { get; set; }
}
```

----

### Entity Framework DbContext

```C#
public class ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
    : DbContext(options)
{
	////entities
    public DbSet<ToDo> ToDos { get; set; }
    public DbSet<ToDoProgress> ToDoProgresses { get; set; }
    public DbSet<User> Users { get; set; }
	////
	
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
    ////
        base.OnModelCreating(modelBuilder);
Assembly assemblyWithConfiguration = GetType().Assembly;
modelBuilder.ApplyConfigurationsFromAssembly(assemblyWithConfiguration);
    }
}

```


---
- The configuration of each model is extracted on a separated class



