---
status: borrador
tags:
  - java
  - testing
  - qa
  - devops
  - maven
  - gradle
created: 2026-05-12
---
# 📊 [[Jacoco]] (Java Code Coverage)

**[[Jacoco]]** es una biblioteca de código abierto que mide qué porcentaje de tu código **[[Java]]** es ejecutado por tus pruebas (unitarias, de integración, etc.). Proporciona métricas visuales para evaluar la calidad de tu suite de tests.

---

## 🎯 ¿Para qué sirve?

- **Identificar áreas sin testear:** Localiza visualmente qué líneas de código, métodos o ramas lógicas (`if/else`, `switch`) no fueron tocadas por los tests.
- **Métricas de complejidad:** Calcula la complejidad ciclomática para ayudarte a entender qué tan difícil es probar ciertas partes del sistema.
- **Control de calidad en CI/CD:** Permite definir umbrales mínimos de cobertura (ej: 80%); si el código nuevo no alcanza ese nivel, el despliegue falla automáticamente.
- **Generación de reportes:** Crea informes detallados en formatos HTML, XML y CSV.

---

## 🛠️ Cómo se usa

Se integra directamente en el ciclo de vida del proyecto mediante herramientas de construcción como **[[Maven]]** o **[[Gradle]]**.

### 1. Uso con [[Maven]]

Agregá el plugin en tu archivo `pom.xml` dentro de la etiqueta `<build>`:

```xml
<plugin>
    <groupId>org.groupId.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.12</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

- **Terminal:** `mvn test`
- **Reporte:** `target/site/jacoco/index.html`

### 2. Uso con [[Gradle]]

En tu `build.gradle`, añadís el plugin:

```gradle
plugins {
    id 'java'
    id 'jacoco'
}

test {
    finalizedBy jacocoTestReport // Genera el reporte después de correr los tests
}

jacocoTestReport {
    dependsOn test // Asegura que los tests corran antes de generar el reporte
}
```

- **Terminal:** `./gradlew test jacocoTestReport`
- **Reporte:** `build/reports/jacoco/test/html/index.html`

---

## 🚦 Interpretación de los reportes

Al abrir el archivo HTML generado, verás el código resaltado con el siguiente código de colores:

- 🟢 **Verde:** El código se ejecutó completamente.
- 🟡 **Amarillo:** Cobertura parcial (se ejecutó una rama de una decisión lógica pero no la otra).
- 🔴 **Rojo:** El código no se ejecutó en absoluto durante las pruebas.

> [!NOTE]
> 
> Una cobertura del 100% no garantiza que el código no tenga bugs, solo indica que todas las líneas fueron ejecutadas. La calidad de los _assertions_ sigue siendo responsabilidad del desarrollador.