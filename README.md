# Prácticas de automatización de pruebas UI

Repositorio de ejercicios de automatización de pruebas web con Selenium y Cucumber. Los escenarios están escritos en Gherkin y sus pasos se implementan en Java.

## Stack y tecnologías

- **Java 15** como lenguaje.
- **Gradle** para la compilación y gestión de dependencias.
- **Selenium WebDriver 3.141.59** para automatizar el navegador Chrome.
- **Cucumber 4.2.0** para describir y ejecutar escenarios BDD.
- **JUnit 4.12** como integración de pruebas de Cucumber.
- **ExtentReports** (`extentreports-cucumber4-adapter`) para generar reportes.
- **SLF4J Simple** para logging.

## Organización

- `src/test/resources/features/`: escenarios Gherkin.
- `src/test/java/steps/`: definiciones de pasos y hooks de Cucumber.
- `src/test/java/pages/`: Page Objects y operaciones reutilizables de Selenium.
- `src/test/java/runner/runner.java`: runner de Cucumber y configuración de reportes.
- `src/test/resources/extent.properties`: configuración de los reportes Extent.

## Funcionalidades cubiertas

- **Búsqueda en Google**: abre Google, ingresa el texto `Google` y pulsa el botón de búsqueda.
- **Búsqueda en una lista dinámica**: filtra por estado y comprueba ciudades para los ejemplos de Washington/Seattle y Chicago/Chicago, Illinois.
- **Tabla estática**: navega a una tabla, lee una celda específica y contiene un escenario para comprobar su visualización.
- **Dropdown del sandbox**: selecciona la opción `Manual`.
- **Captura ante fallos**: el hook posterior a cada escenario adjunta una captura de pantalla cuando el escenario falla.

## Requisitos

- JDK 15.
- Gradle instalado (el repositorio no incluye Gradle Wrapper).
- Google Chrome y una versión compatible de ChromeDriver.

La ruta del ejecutable de ChromeDriver está configurada actualmente de forma fija en `src/test/java/pages/BasePage.java` como `C:\Program Files\ChromeDriver\chromedriver.exe`. Ajustala para tu entorno antes de ejecutar las pruebas si la ruta local es distinta.

## Ejecución

Desde la raíz del repositorio:

```bash
gradle test
```

El runner está configurado para ejecutar por defecto los escenarios con la etiqueta `@List`. Para ejecutar otros escenarios, ajustá las etiquetas en `@CucumberOptions` de `src/test/java/runner/runner.java` o pasá las opciones de Cucumber mediante `cucumber.options`. Por ejemplo, el runner incluye una configuración de ejemplo para seleccionar escenarios etiquetados `@Grid` y `@Smoke`:

```bash
gradle test -Dcucumber.options="--tags @Grid --tags @Smoke"
```

## Reportes

El runner genera un reporte JSON en `target/cucumber-reports.json`. El adaptador de ExtentReports también está configurado para generar el reporte HTML en `test-output/HtmlReport/ExtentHtml.html`.

## Pendientes conocidos

- El paso final del escenario de Google todavía no valida los resultados.
- La comprobación de visibilidad de la tabla usa actualmente `assertFalse`; revisar esa aserción si el objetivo es confirmar que la tabla se muestra.
