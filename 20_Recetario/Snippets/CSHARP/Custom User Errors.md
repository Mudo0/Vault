```csharp
using ErrorOr;

namespace Domain.Errors
{
    public static partial class DomainErrors
    {
        /// <summary>
        /// Clase estática para definir y acceder a los errores relacionados con la entidad User.
        /// </summary>
        public static class User
        {
            public static Error UserNotFound => Error.NotFound(
                    code: "User.NotFound",
                    description: "The user was not found.");

            public static Error SaveFailure => Error.Failure(
                    code: "User.SaveFailure",
                    description: "An error occurred while saving the user.");
        }
        
		    public static Error InvalidUsername => Error.Validation(
				    code: "User.InvalidUsername",
				    description: "The provided username is invalid.");
    }
}

```

