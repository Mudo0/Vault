Este script deployea una app de angular en cloudflare pages:

## 🔄 Flujo de Ejecución (Paso a Paso)

### 1. Selección Interactiva de Versión
- Lee la versión actual directamente desde el `package.json`.
- Calcula y te muestra dinámicamente cómo quedarían los tres tipos de salto semántico (_Semantic Versioning_):
    
    - **Patch** (ej. `1.0.0` → `1.0.1`) para correcciones.
    - **Minor** (ej. `1.0.0` → `1.1.0`) para nuevas funcionalidades.
    - **Major** (ej. `1.0.0` → `2.0.0`) para rediseños o cambios grandes.
- Te pide ingresar una breve descripción del cambio.
### 2. Ejecución de Pruebas (`ng test --no-watch`)
- Corre los tests unitarios una sola vez.
- **Filtro de seguridad:** Si un solo test falla, la ejecución se interrumpe de inmediato. No se modifica ningún archivo ni se sube nada.
### 3. Compilación de Angular (`ng build`)
- Genera los archivos de producción en la ruta `dist/bianca-tattoo/browser`.
- Si hay un error de TypeScript, sintaxis o HTML durante el build, el script se detiene aquí sin haber tocado el número de versión.
### 4. Incremento de Versión (`bumpVersion`)
- Una vez que el código pasó los tests y compiló con éxito, ejecuta `npm version <tipo> --no-git-tag-version`.
- Lee la nueva versión generada y arma el mensaje formal para Git (ejemplo: `v1.1.0: Agregada nueva galería`).
### 5. Confirmación en Git (`stageAndCommit`)
- Ejecuta `git add .` para preparar los archivos modificados.
- **Chequeo inteligente:** Usa `git diff --cached --quiet` para verificar si realmente hay cambios nuevos. Si no hay nada diferente por guardar, omite el commit limpiamente para no provocar un error de Git.
### 6. Despliegue a Cloudflare Pages (`deploy`)
- Sube los archivos compilaros (`dist/bianca-tattoo/browser`) al proyecto **`biantattoo`** en Cloudflare Pages mediante `wrangler`.
- **Si el despliegue en Cloudflare es exitoso:** Ejecuta automáticamente `git push` para enviar los commits a GitHub.
- **Si el despliegue falla:** No rompe todo. Te informa amablemente que tu código ya quedó guardado y versionado a salvo en Git local, y te entrega el comando exacto para reintentar la subida manualmente cuando quieras.
## 🛡️ Mecanismos de Seguridad Destacados

- **Rollback Automático de `package.json`:** Si por algún motivo el proceso falla justo después de haber cambiado la versión pero antes de hacer el commit, el script ejecuta `restorePackageJson()` para revertir tu `package.json` a la versión original.
- **Orden Lógico Perfecto:** **Test ➔ Build ➔ Version ➔ Commit ➔ Deploy ➔ Push**. Este orden evita que se creen "commits fantasma" de código que no llega a compilar.
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

  

function parseVersion(version) {

  const [major, minor, patch] = version.split('.').map(Number);

  return { major, minor, patch };

}

  

function formatVersion(v) {

  return `${v.major}.${v.minor}.${v.patch}`;

}

  

function bumpPatch(v) {

  return { major: v.major, minor: v.minor, patch: v.patch + 1 };

}

  

function bumpMinor(v) {

  return { major: v.major, minor: v.minor + 1, patch: 0 };

}

  

function bumpMajor(v) {

  return { major: v.major + 1, minor: 0, patch: 0 };

}

  

function exitError(msg) {

  console.error(`\n❌  ${msg}\n`);
  rl.close();
  process.exit(1);

}

  

// ── Input ───────────────────────────────────────────────────────────────────

  

async function askReleaseType(currentVersion) {

  const v = parseVersion(currentVersion);
  const patchV = formatVersion(bumpPatch(v));
  const minorV = formatVersion(bumpMinor(v));
  const majorV = formatVersion(bumpMajor(v));

  

  console.log('¿Qué tipo de cambio es?');

  console.log(`  1) Patch  (${currentVersion} → ${patchV})  — Corrección de errores`);

  console.log(`  2) Minor  (${currentVersion} → ${minorV})  — Nueva funcionalidad`);

  console.log(`  3) Major  (${currentVersion} → ${majorV})  — Cambio grande / rediseño\n`);

  

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

  

function generateVersionFile() {

  execSync('node scripts/generate-version.js', { stdio: 'pipe', cwd: ROOT });

}

  

function deploy(newVersion, commitMessage) {

  console.log(`\n☁️  Desplegando a Cloudflare Pages...\n`);

  

  const cmd = `npx wrangler pages deploy "${DIST_PATH}" --project-name="${PROJECT_NAME}" --commit-message="${commitMessage}"`;

  

  try {

    exec(cmd);
    console.log(`\n✅  ¡Despliegue exitoso v${newVersion}! 🎉`);

  

    console.log('\n📤  Subiendo cambios a Git remoto...');
    exec('git push');
    console.log('✅  Push exitoso.\n');

  

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

  

  const originalPkg = readPackageJson();

  const originalVersion = originalPkg.version;

  

  const releaseType = await askReleaseType(originalVersion);

  const userMessage = await askCommitMessage();

  

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