---
status: borrador
tags:
  - configuracion
  - git
  - ssh
  - wsl
created: 2025-12-10
---
# 🔐 Configuración [[SSH]] Multi-Cuenta ([[Linux]]/[[WSL]])

**Objetivo:** Utilizar dos cuentas de [[GitHub]] (Personal y Estudiante) en el mismo equipo sin conflictos de permisos.


## 1. 🔑 Generación de Llaves

Se generan dos llaves distintas: una por defecto y otra con un nombre específico para diferenciar la identidad.

```shell
# 1. Llave Personal (Por defecto: id_ed25519)
ssh-keygen -t ed25519 -C "personal@gmail.com"

# 2. Llave Estudiante (Nombre específico: id_student)
ssh-keygen -t ed25519 -C "estudiante@facultad.edu" -f ~/.ssh/id_student
```

---

## 2. ☁️ Carga en [[GitHub]]

Se debe copiar el contenido de la llave PÚBLICA (`.pub`) e ingresarlo en **[[GitHub]] -> Settings -> SSH Keys**.

Bash

```shell
# Copiar Llave Personal
cat ~/.ssh/id_ed25519.pub | clip.exe

# Copiar Llave Estudiante
cat ~/.ssh/id_student.pub | clip.exe
```

---

## 3. ⚙️ Creación del Archivo de Configuración

Este archivo indica al sistema [[Linux]] qué llave utilizar basándose en el "nombre" (host) al que se llama.

**Archivo:** `~/.ssh/config`

```plaintext
# Cuenta Personal (Default)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Cuenta Estudiante (Alias)
Host github-student
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_student
```

---

## 4. 📥 Uso (Clonado de Repositorios)

El método consiste en modificar el dominio al momento de clonar para activar el alias configurado en el paso anterior.

- **Personal:** `git clone git@github.com:usuario/repo.git`
- **Estudiante:** `git clone git@github-student:usuario/repo.git`

---

## 5. ✍️ Configuración de Firma (Email)

Configuración necesaria para asegurar la correcta atribución en el historial de cambios (commits).

- **Global (Personal):** Se establece como configuración predeterminada del sistema.
```shell
    git config --global user.email "personal@gmail.com"
    ```
    
- **Local (Proyectos de Facultad):** Se configura únicamente dentro de la carpeta del repositorio específico.
   ```shell
    git config user.email "estudiante@facultad.edu"
    ```
    