## 1. Desencadenantes (_Triggers_)


```yml
name: Compilar APK Android

on:
  push:
    branches: [ main, master ]
  workflow_dispatch:
```

- **`name`**: Es el título que vas a ver en la pestaña _Actions_ de GitHub para identificar este proceso.
- **`on:`**: Define **cuándo** se ejecuta.
    - **`push: branches: [ main, master ]`**: Cada vez que subas código o hagas un _merge_ a la rama principal, el proceso arranca solo.
    - **`workflow_dispatch:`**: Te agrega un botón de "Run workflow" en la web de GitHub para que puedas lanzar la compilación a mano cuando quieras, sin tener que hacer un commit.
## 2. Definición del Entorno (_Runner_)

```yml
jobs:
  build:
    runs-on: ubuntu-latest
```

- **`jobs:`**: Contiene la lista de tareas a realizar.
- **`runs-on: ubuntu-latest`**: Le dice a GitHub qué tipo de máquina virtual (servidor en la nube) usar.
    - **Por qué Ubuntu:** Es la opción más rápida, consume menos minutos gratuitos de GitHub Actions y tiene preinstaladas casi todas las herramientas base necesarias para Android y Node.
## 3. La Secuencia de Pasos (_Steps_)

Cada paso es una acción individual que se ejecuta en orden secuencial dentro de esa máquina virtual de Ubuntu.
### Paso 1: Clonar tu código
```yml
- name: Checkout del código
  uses: actions/checkout@v4
```

- **Qué hace:** Clona el repositorio de tu proyecto dentro de la máquina virtual de GitHub.
- **Por qué:** Por defecto, el servidor arranca totalmente vacío. Sin esto, no hay archivos para compilar.
### Paso 2: Preparar Node.js
```yml
- name: Configurar Node.js
  uses: actions/setup-node@v4
  with:
    node-version: 20
    cache: 'npm'
```

- **Qué hace:** Instala Node.js versión 20 en el servidor y activa la caché de paquetes de NPM.
- **Por qué:** Tu app usa Angular y Capacitor, los cuales corren sobre el ecosistema de Node. Usar `cache: 'npm'` hace que las siguientes ejecuciones sean mucho más rápidas porque no descarga todas las librerías desde cero cada vez.
### Paso 3: Preparar Java (SDK de Android)
```yml
- name: Configurar Java JDK 17
  uses: actions/setup-java@v4
  with:
    distribution: 'zulu'
    java-version: '17'
```

- **Qué hace:** Instala el Kit de Desarrollo de Java (JDK 17).
- **Por qué:** Aunque escribas la app en TypeScript/Angular, el proyecto nativo de Android se compila con **Gradle** (que funciona sobre la Máquina Virtual de Java). Sin Java, es imposible generar un `.apk`.
### Paso 4: Instalar las dependencias de la app
```yml
- name: Instalar dependencias
  run: npm ci
```
- **Qué hace:** Instala las librerías de tu `package.json`.
- **Por qué `npm ci` en vez de `npm install`:** `npm ci` está pensado específicamente para entornos de integración continua (CI). Es más rápido, más estricto y garantiza instalarlas **exactamente** como están en tu `package-lock.json`, evitando errores por diferencias de versiones.
### Paso 5: Compilar Angular y sincronizar Capacitor
```yml
- name: Build de Angular y Capacitor Sync
  run: |
    npm run build
    npx cap sync android
```

- **Qué hace:**
    1. Ejecuta el `build` de Angular para generar los archivos HTML, JS y CSS optimizados (normalmente en la carpeta `dist/` o `www/`).
    2. Ejecuta `npx cap sync android`, que toma esa carpeta compilada web y la copia dentro de la estructura del proyecto nativo de Android (`android/app/src/main/assets/public`).
- **Por qué:** Si no haces el `cap sync`, Android terminaría compilando la app con una versión vieja del código web (o sin código web).
### Paso 6: Permisos para el compilador de Android
```yml
- name: Dar permisos a Gradle
  run: chmod +x android/gradlew
```

- **Qué hace:** Le otorga permisos de ejecución al ejecutable de Gradle (`gradlew`).
- **Por qué:** A veces, al subir proyectos desde Windows a Git, los archivos pierden sus permisos de ejecución en sistemas Linux (Ubuntu). Este comando previene el típico error de `Permission denied`.
### Paso 7: Generar el archivo `.apk`
```yml
- name: Compilar APK (Debug)
  run: |
    cd android
    ./gradlew assembleDebug
```

- **Qué hace:** Entra a la carpeta de Android y llama al compilador nativo para generar la versión `Debug` de la app.
- **Por qué `assembleDebug`:** Genera un APK sin necesidad de configurar claves de firma complejas (_Keystore_). Es ideal para probar rápido en teléfonos físicos.
### Paso 8: Guardar y exponer el resultado
```yml
- name: Guardar APK como Artefacto
  uses: actions/upload-artifact@v4
  with:
    name: app-debug
    path: android/app/build/outputs/apk/debug/app-debug.apk
```

- **Qué hace:** Busca el archivo `.apk` recién creado dentro de la máquina virtual y lo sube al panel de GitHub.
- **Por qué:** Al terminar el proceso, la máquina virtual de Ubuntu se destruye por completo. Si no usas esta acción para rescatar el `.apk`, se borraría junto con todo el servidor.

---

```yml

name: Compilar APK Android

on:
  push:
    branches: [ main, master ]
  workflow_dispatch: # Permite ejecutar el workflow manualmente desde la interfaz de GitHub

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # 1. Descargar el código del repositorio
      - name: Checkout del código
        uses: actions/checkout@v4

      # 2. Configurar el entorno de Node.js
      - name: Configurar Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      # 3. Configurar Java (requerido para compilar Android)
      - name: Configurar Java JDK 17
        uses: actions/setup-java@v4
        with:
          distribution: 'zulu'
          java-version: '17'

      # 4. Instalar dependencias de Node
      - name: Instalar dependencias
        run: npm ci

      # 5. Compilar la app Web en Angular y sincronizar con Capacitor
      - name: Build de Angular y Capacitor Sync
        run: |
          npm run build
          npx cap sync android

      # 6. Dar permisos de ejecución a Gradle
      - name: Dar permisos a Gradle
        run: chmod +x android/gradlew

      # 7. Compilar el APK de Android
      - name: Compilar APK (Debug)
        run: |
          cd android
          ./gradlew assembleDebug

      # 8. Subir el APK como artefacto descargable en GitHub
      - name: Guardar APK como Artefacto
        uses: actions/upload-artifact@v4
        with:
          name: app-debug
          path: android/app/build/outputs/apk/debug/app-debug.apk

```