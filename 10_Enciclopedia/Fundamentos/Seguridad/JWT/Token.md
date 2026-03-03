## 1. El Token Codificado (Lo que viaja por la red)

Cuando el servidor te envía el token (o cuando tú se lo envías al servidor en una petición), se ve como una larga cadena de texto incomprensible a simple vista, separada por dos puntos (`.`):


<span style="color: red;">eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9</span>.<span style="color: violet;">eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Ikp1YW4gUGVyZXoiLCJyb2xlIjoiYWRtaW4iLCJpYXQiOjE1MTYyMzkwMjJ9</span>.<span style="color: cyan;">SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c</span>

---
## 2. El Token Decodificado (Lo que hay adentro)
Si tomamos esa larga cadena de texto y la separamos por sus puntos, obtenemos las tres partes que te mencioné antes (Header, Payload y Signature). Así es como se verían al decodificarlas:

#### Parte 1: El Header (Rojo)
La primera parte antes del primer punto (`eyJhbGci...`) nos dice cómo está construido el token:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

_Nos indica que es un JWT y que usa el algoritmo HMAC-SHA256 para la firma._

#### Parte 2: El Payload (Morado)
La segunda parte, entre los dos puntos (`eyJzdWIi...`), contiene la información del usuario (los _claims_):

```json
{
  "sub": "1234567890",
  "name": "Juan Perez",
  "role": "admin",
  "iat": 1516239022
}
```

- **`sub`** (Subject): El ID único del usuario en la base de datos.
- **`name`**: El nombre del usuario.
- **`role`**: Su nivel de acceso (esto es lo que permite la **autorización**).
- **`iat`** (Issued At): Un número que representa la fecha y hora exacta en la que se creó este token.

#### Parte 3: La Signature (Azul)

La última parte (`SflKxw...`) no es un JSON, es el resultado matemático que crea el servidor para asegurar que nadie alteró el token. Conceptualmente, el servidor hace esto:

```js
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  "mi_super_secreto_que_solo_conoce_el_servidor"
)
```

Si alguien intenta cambiar el `"role": "admin"` a `"role": "superadmin"` en el Payload, la firma matemática ya no coincidirá cuando el servidor la revise, y el token será rechazado automáticamente.

---


