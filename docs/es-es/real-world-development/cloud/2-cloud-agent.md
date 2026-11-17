---
title: "Ejercicio 2 - Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Es probable que casi todas las organizaciones tengan problemas de deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que hay que actualizar o solicitudes de funcionalidad que llevan tiempo en el backlog porque no ha habido tiempo para implementarlas. El agente de GitHub Copilot en la nube está diseñado para realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, genera un borrador de solicitud de incorporación de cambios para que lo revise un desarrollador. Así puedes delegar tareas tediosas, acelerar el desarrollo y centrarte en cuestiones de mayor alcance.

Con el agente de Copilot en la nube explorarás:

- cómo personalizar el entorno de generación de código.
- cómo garantizar que las operaciones se realicen de forma segura.
- la importancia de delimitar claramente las incidencias.
- cómo asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica que quiere resolver. Los contratistas que crearon la primera versión del sitio dejaron la documentación en mal estado: comprobarás que no hay ninguna. Como primer paso, se quieren añadir comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere mejorar la búsqueda de juegos. Quiere mostrar juegos relacionados —otros títulos de la misma categoría— en la página de detalles de cada juego para que la gente pueda seguir explorando. No necesita una implementación refinada; solo algo que permita hacer pruebas de aceptación de la experiencia. Es un impedimento para el equipo, aunque ahora hay otras incidencias con mayor prioridad.

Estas son tareas que suelen posponerse y que conviene asignar al agente de Copilot en la nube. El agente puede trabajar en ellas de forma asíncrona mientras tú te ocupas de otras tareas, y después puedes volver para revisar su trabajo y comprobar que el resultado es correcto.

## Presentación del agente de GitHub Copilot en la nube

El [agente de GitHub Copilot en la nube](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma parecida a un desarrollador. Igual que con un desarrollador, puedes trabajar con él de varias formas, por ejemplo, [asignándole una incidencia de GitHub](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Cuando se le asigna una incidencia, Copilot crea un borrador de solicitud de incorporación de cambios para registrar el progreso, configura un entorno y empieza a trabajar. Puedes consultar la sesión mientras sigue en curso o una vez completada. Cuando la solución propuesta esté lista para revisión, te mencionará en la solicitud.

## La importancia de delimitar bien las instrucciones

GitHub Copilot no hace magia: no puedes saltarte el análisis. Incluso las tareas que parecen sencillas pueden ser complejas, así que [delimita con cuidado las tareas que asignas al agente de Copilot en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir IA generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has visto cómo las instrucciones personalizadas orientan a Copilot. Si ya completaste el ejercicio práctico sobre instrucciones personalizadas, has visto `.github/copilot-instructions.md` en acción; si no, este es un buen momento para echarle un vistazo. Antes de asignar trabajo al agente de Copilot en la nube, revisa los archivos de instrucciones del repositorio sin modificarlos para poder observar su efecto más adelante.

Abre los siguientes archivos en la interfaz web de GitHub o en un codespace que ya tengas en ejecución:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observa el frontmatter `applyTo`, que limita estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes al agente en la nube la incidencia `Code lacks documentation` en la sección siguiente, busca en la solicitud de incorporación de cambios comentarios TSDoc, convenciones de TypeScript y encabezados de comentarios. Estas indicaciones proceden de los archivos de instrucciones, y volveremos a mencionarlas al revisar las solicitudes en un ejercicio posterior.

## Configura el entorno de desarrollo del agente de Copilot en la nube

La creación de código suele requerir un entorno concreto y la ejecución de scripts de configuración, independientemente de quién realice el trabajo. Lo mismo ocurre con las tareas que se asignan a Copilot, que trabaja de forma parecida a un ingeniero de software (SWE).

El agente en la nube usa [GitHub Actions][github-actions] como entorno de trabajo. Puedes personalizarlo mediante un [flujo de trabajo de configuración especial][setup-workflow] en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece a trabajar. Así puede acceder a las herramientas y dependencias de desarrollo necesarias. Este flujo se ha configurado por adelantado para facilitar el taller. Proporciona Node.js, las dependencias del proyecto, los binarios del navegador para las pruebas de extremo a extremo y la base de datos SQLite migrada y precargada de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Limita los permisos a los mínimos necesarios para *tus pasos*. Copilot tendrá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de los pasos de configuración, por ejemplo, para instalar dependencias, necesitarás el permiso `contents: read`. Si no lo clonas en esos pasos, Copilot lo hará automáticamente cuando terminen.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de frontend y aplicación: Node.js (ahora toda la aplicación usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y precarga la base de datos SQLite local para que las compilaciones y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier otro flujo de trabajo de GitHub, pero tiene algunos aspectos importantes:

- Contiene un único trabajo llamado `copilot-setup-steps`. Se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la solicitud.
- El desencadenador `workflow_dispatch` permite ejecutar manualmente el flujo desde la pestaña **Actions** del repositorio. Esto sirve para probarlo sin esperar a que Copilot lo ejecute.

## Añade documentación

Todos reconocen la importancia de la documentación, pero muchos proyectos tienen información obsoleta o carecen de ella. Esta deuda técnica suele quedar desatendida, reduce la productividad y dificulta el mantenimiento del código o la incorporación de nuevos desarrolladores al equipo. Copilot puede ayudar a crear documentación, así que esta es una buena incidencia para asignarle al agente en la nube. El agente trabajará en segundo plano para generarla y revisarás el resultado en un ejercicio posterior.

1. Abre tu repositorio en una pestaña nueva del navegador en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de una incidencia nueva.
4. Selecciona **Blank issue** para crear la incidencia.
5. Escribe `Code lacks documentation` en **Title**.
6. Escribe lo siguiente en **Description**:

   ```plaintext
   Nuestra organización exige que las funciones y los métodos incluyan comentarios TSDoc de documentación cuando sean útiles. Sin embargo, las actualizaciones recientes no han seguido este estándar. Hay que actualizar el código existente para incluir comentarios de documentación cuando ayuden a aclarar el comportamiento.
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

   ![Asignar una incidencia a Copilot](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la solicitud de incorporación de cambios (PR) nueva, que tendrá un título parecido a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la ventana del navegador.
12. Al cabo de unos minutos, Copilot debería haber creado una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer en la solicitud. Copilot está preparando su entorno —ejecuta el flujo de trabajo descrito antes—, analizando el proyecto y determinando cómo abordar la tarea.

13. Revisa la lista y las tareas que va a completar.
14. Desplázate por la cronología de la solicitud y busca una actualización que indique que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona el botón **View session**.

   ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la ventana para ver el indicador actualizado.

16. Observa que puedes desplazarte por la sesión en directo y ver cómo Copilot resuelve el problema: explora el código y su estado, se detiene a analizar y elegir un plan y, después, crea el código.

El proceso puede tardar varios minutos. Una de las principales ventajas del agente de Copilot en la nube es que puede trabajar de forma asíncrona y dejarte tiempo para otras tareas. Aprovecharemos esa característica asignándole otra tarea y, después, nos centraremos en añadir funcionalidades a la aplicación.

## Añade una sección de juegos relacionados a la página de detalles

Una gran ventaja del agente de Copilot en la nube es que permite dividir el trabajo: tú puedes centrarte en unas tareas mientras el agente se ocupa de otras. Aunque añadir una sección de juegos relacionados quizá no lleve mucho tiempo, puedes aprovechar ese tiempo para otras tareas. Asigna el trabajo al agente en la nube.

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de una incidencia nueva.
4. Selecciona **Blank issue** para usar la plantilla en blanco.
5. Escribe `Show related games on the game details page` en **Title**.
6. Escribe lo siguiente en **Description**:

   ```markdown
   Queremos ayudar a descubrir más juegos mostrando juegos relacionados en la página de detalles de cada juego. El equipo de diseño quiere explorar la experiencia y realizar pruebas de aceptación. Estos son los requisitos:

   - Añadir un helper de acceso a datos en `src/lib/` que devuelva otros juegos de la misma categoría que un juego, excluyendo ese juego
   - Mostrar en la página de detalles una sección "Related games" que utilice el helper
   - Gestionar el caso en que un juego no tenga juegos relacionados
   - Crear pruebas unitarias para el nuevo helper
   - Antes de crear la solicitud de incorporación de cambios, asegurarse de que se superan todas las pruebas
   ```

7. Selecciona **Create** para crear la incidencia.
8. A la derecha, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

   ![Asignar una incidencia a Copilot](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Poco después, deberías ver el emoji 👀 en el primer comentario de la incidencia, que indica que Copilot está trabajando en ella.

![Copilot usa el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot ya está trabajando en la segunda solicitud. El agente en la nube funciona de manera parecida a un ingeniero de software, así que no hace falta supervisarlo continuamente; puedes revisar el resultado cuando termine. Ahora crearás y usarás agentes personalizados.

## Resumen y siguientes pasos

En este ejercicio has explorado el [agente de GitHub Copilot en la nube][copilot-agents]. Puedes asignarle incidencias para que trabaje de forma asíncrona. Copilot puede resolver deuda técnica, crear funcionalidades o ayudar a migrar código de un marco de trabajo a otro.

Has explorado estos conceptos:

- cómo personalizar el entorno de generación de código.
- cómo garantizar que las operaciones se realicen de forma segura.
- la importancia de delimitar claramente las incidencias.
- cómo asignar incidencias a Copilot.

Mientras el agente en la nube trabaja, puedes centrarte en crear y usar agentes personalizados. [El agente de Copilot en la nube también puede usar servidores del Model Context Protocol (MCP)][cloud-agent-mcp] y acceder a las instrucciones personalizadas que exploraste en ejercicios anteriores.

## Recursos

- [Acerca del agente de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de trabajo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente ejercicio: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
