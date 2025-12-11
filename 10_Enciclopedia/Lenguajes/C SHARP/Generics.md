Es una funcionalidad que nos da [[(.NET)]] la cual nos permite crear código reusable entre múltiples entidades. 

Cuando creamos código genérico lo hacemos para que sea compatible con cualquier tipo de dato y por ello, “seguro” ante diferentes tipos.

---

## Lista Genérica

```csharp
List<T> /// T de tipo
```

- T indica tipo y con esto se pueden declarar tanto listas que pueden contener cualquier tipo de objeto, como métodos que también devuelvan un tipo genérico.

```Csharp
public class Ejemplo
{ 
	public T GenericMethod<T>(T receivedGeneric) 
	{ 
		return receivedGeneric; 
	} 
}
```

- Al poner <**T**> delante del método le indicamos que espera recibir un tipo genérico sin declarar.