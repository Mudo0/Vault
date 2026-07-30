Este script deployea una app de angular en cloudflare pages:
### 1. Configuración inicial y lectura de rutas

- Define la raíz del proyecto (`ROOT`), la ruta del `package.json`, el directorio de salida compilado (`dist/bianca-tattoo/browser`) y el nombre del proyecto en Cloudflare (`biantattoo`).
- Prepara una interfaz interactiva de lectura por consola (`readline`) para hacerte preguntas.
### 2. Recolección de datos (Interacción)

- **Pregunta el tipo de cambio:** Te pide seleccionar entre `1) Patch`, `2) Minor` o `3) Major` (si no respondes nada, asume `1 / patch`).
- **Pregunta el mensaje:** Te pide un texto descriptivo de los cambios realizados.
- **Guarda un respaldo en memoria:** Lee la versión original del `package.json` para poder restaurarla si algo falla más adelante.
### 3. Ejecución de pruebas (`runTests`)

- Ejecuta `ng test --no-watch`.
- Corre los tests unitarios una sola vez. **Si un test falla, el script se detiene de inmediato** y no avanza al siguiente paso.
### 4. Compilación de Angular (`runBuild`)

- Ejecuta `ng build`.
- Genera los archivos optimizados para producción dentro de `dist/bianca-tattoo/browser`. Si la compilación falla (por un error de TypeScript, HTML o SCSS), el script se aborta.
### 5. Actualización de versión (`bumpVersion`)

- Ejecuta `npm version [patch|minor|major] --no-git-tag-version`.
- Aumenta el número de versión en `package.json` sin crear etiquetas de Git automáticas aún.
- Construye la cadena del mensaje del commit (ej: `v1.1.0: Se agregó formulario de contacto`).
- Activa la bandera de control `versionBumped = true`.
### 6. Guardado en Git (`stageAndCommit`)

- Ejecuta `git add .` para preparar todos los archivos modificados.
- Verifica mediante `git diff --cached --quiet` si realmente hay cambios preparados:
    - Si **hay cambios**, ejecuta `git commit -m "vX.Y.Z: mensaje"`.
    - Si **no hay cambios nuevos**, omite el commit para evitar que Git lance un error.
- Activa la bandera de control `commitDone = true`.
### 7. Despliegue a Cloudflare Pages (`deploy`)

- Ejecuta el comando de Wrangler:
    `npx wrangler pages deploy "dist/bianca-tattoo/browser" --project-name="biantattoo" --commit-message="..."`
    
- **Si el despliegue es exitoso:** Muestra el mensaje de felicitaciones y finaliza.
- **Si el despliegue falla:** Informa que el commit en Git quedó a salvo, muestra el comando exacto de Wrangler para reintentarlo manualmente y sale con código de error.
### 8. Sistema de Seguridad y Rollback (`catch`)

Si ocurre un error imprevisto durante el proceso:

- **Si la versión se modificó pero AÚN NO se hizo el commit** (`versionBumped && !commitDone`): Restaura automáticamente el `package.json` original con la versión anterior para no dejar tu repositorio en un estado inconsistente.
- Imprime el mensaje de error y cierra la ejecución de forma limpia.


```js


const { execSync } = require('child_process');

const readline = require('readline');

const fs = require('fs');

const path = require('path');

  

// ── Constantes ──────────────────────────────────────────────────────────────

  

const ROOT = path.join(__dirname, '..');

const PKG_PATH = path.join(ROOT, 'package.json');

const DIST_PATH = 'dist/bianca-tattoo/browser';

const PROJECT_NAME = 'biantattoo';

  

// ── Readline ────────────────────────────────────────────────────────────────

  

const rl = readline.createInterface({ input: process.stdin, output: process.stdout });

const ask = (question) => new Promise((resolve) => rl.question(question, resolve));

  

// ── Helpers ─────────────────────────────────────────────────────────────────

  

function exec(command, options = {}) {

  return execSync(command, { stdio: 'inherit', cwd: ROOT, ...options });

}

  

function readPackageJson() {

  return JSON.parse(fs.readFileSync(PKG_PATH, 'utf8'));

}

  

function restorePackageJson(original) {

  fs.writeFileSync(PKG_PATH, JSON.stringify(original, null, 2) + '\n');

}

  

function exitError(msg) {

  console.error(`\n❌  ${msg}\n`);

  rl.close();

  process.exit(1);

}

  

// ── Input ───────────────────────────────────────────────────────────────────

  

async function askReleaseType() {

  console.log('¿Qué tipo de cambio es?');

  console.log('  1) Patch  (1.0.0 → 1.0.1)  — Corrección de errores');

  console.log('  2) Minor  (1.0.0 → 1.1.0)  — Nueva funcionalidad');

  console.log('  3) Major  (1.0.0 → 2.0.0)  — Cambio grande / rediseño\n');

  

  const answer = (await ask('Opción [1]: ')).trim() || '1';

  const types = { 1: 'patch', 2: 'minor', 3: 'major' };

  return types[answer] ?? 'patch';

}

  

async function askCommitMessage() {

  return (await ask('\nMensaje descriptivo del cambio: ')).trim();

}

  

// ── Pipeline ────────────────────────────────────────────────────────────────

  

function runTests() {

  console.log('\n🧪  Ejecutando tests...');

  exec('ng test --no-watch');

}

  

function runBuild() {

  console.log('\n🔨  Compilando Angular...');

  exec('ng build');

}

  

function bumpVersion(releaseType, userMessage) {

  console.log('\n📦  Actualizando versión...');

  exec(`npm version ${releaseType} --no-git-tag-version`);

  

  const pkg = readPackageJson();

  const newVersion = pkg.version;

  const commitMessage = `v${newVersion}${userMessage ? `: ${userMessage}` : ''}`;

  

  return { newVersion, commitMessage };

}

  

function stageAndCommit(commitMessage) {

  console.log('\n📝  Guardando cambios en Git...');

  exec('git add .');

  

  // git diff --cached --quiet → 0 si NO hay cambios, ≠0 si hay

  try {

    execSync('git diff --cached --quiet', { stdio: 'pipe', cwd: ROOT });

    console.log('   No hay cambios nuevos que commitear, se omite el commit.');

  } catch {

    exec(`git commit -m "${commitMessage}"`);

  }

}

  

function deploy(newVersion, commitMessage) {

  console.log(`\n☁️  Desplegando a Cloudflare Pages...\n`);

  

  const cmd = `npx wrangler pages deploy "${DIST_PATH}" --project-name="${PROJECT_NAME}" --commit-message="${commitMessage}"`;

  

  try {

    exec(cmd);

    console.log(`\n✅  ¡Despliegue exitoso v${newVersion}! 🎉\n`);

    rl.close();

  } catch {

    console.error(

      `\n⚠️  El commit v${newVersion} se guardó con éxito en Git, pero falló la subida a Cloudflare.`,

    );

    console.error('   Tu código está a salvo y versionado.');

    console.error('   Para reintentar el deploy manualmente:');

    console.error(`   ${cmd}\n`);

    rl.close();

    process.exit(1);

  }

}

  

// ── Main ────────────────────────────────────────────────────────────────────

  

async function main() {

  console.log('\n🚀  ---  DESPLIEGUE A CLOUDFLARE PAGES  ---\n');

  

  const releaseType = await askReleaseType();

  const userMessage = await askCommitMessage();

  

  const originalPkg = readPackageJson();

  const originalVersion = originalPkg.version;

  

  let versionBumped = false;

  let commitDone = false;

  

  try {

    runTests();

    runBuild();

  

    const { newVersion, commitMessage } = bumpVersion(releaseType, userMessage);

    versionBumped = true;

  

    stageAndCommit(commitMessage);

    commitDone = true;

  

    deploy(newVersion, commitMessage);

    // deploy maneja su propio éxito/error con mensajes específicos

  } catch (err) {

    if (versionBumped && !commitDone) {

      restorePackageJson(originalPkg);

      console.log(`\n↩️  Versión restaurada a ${originalVersion} (package.json)`);

    }

  

    exitError(err.message);

  }

}

  

main();

```