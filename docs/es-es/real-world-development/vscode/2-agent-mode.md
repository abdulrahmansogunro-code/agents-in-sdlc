---
title: "Ejercicio 2 - Añadir funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas de una aplicación suelen requerir cambios en varios archivos y tareas como ejecutar pruebas. El flujo habitual de desarrollo incluye localizar todos los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo falta y volver a modificarlo. Y así sucesivamente.

El modo de agente de Copilot ayuda con este proceso.

El modo de agente está diseñado para trabajar con más autonomía en el entorno de desarrollo integrado (IDE). Se comporta de forma parecida a un desarrollador: primero explora la estructura del proyecto, realiza las actualizaciones necesarias, ejecuta tareas como las pruebas y corrige automáticamente los errores que encuentra. Explora cómo usarlo para añadir funcionalidad al sitio.

> [!NOTE]
> Aunque los nombres se parecen, el modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el IDE y permite ciclos rápidos de comentarios e interacción. El agente en la nube trabaja de forma asíncrona como un miembro del equipo y se comunica contigo mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio aprenderás cómo:

- el modo de agente de Copilot puede explorar el proyecto, identificar los archivos pertinentes y coordinar cambios.
- el modo de agente de GitHub Copilot puede implementar funcionalidades en la interfaz y la capa de datos.
- revisar los cambios y las pruebas generados por el modo de agente antes de combinarlos en el código base.

## Escenario

A medida que crece la lista de juegos, quieres permitir que los usuarios filtren por categoría y editor. En el ejercicio anterior ya añadiste un helper de editores. Ahora completarás el trabajo restante en la capa de datos, la interfaz y las pruebas con el modo de agente de Copilot.

## Ejecuta el sitio web de Tailspin Toys

Antes de hacer cambios, explora el sitio web de Tailspin Toys para conocer su funcionalidad actual.

El sitio es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Permite mostrar juegos y sus detalles. Es una única aplicación Astro que genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local desde su frontmatter mediante Drizzle ORM. No hay una API de backend independiente ni un marco de trabajo de interfaz del lado cliente. Los helpers reutilizables de acceso a datos se encuentran en `src/lib/`, y la interactividad se implementa con un elemento `<script>` de Astro de alcance reducido que usa las API estándar del DOM.

### Inicia el sitio web

Se ha proporcionado la tarea `npm run dev` para iniciar el único servidor de desarrollo de Astro. Ejecútala en GitHub Codespaces con estos pasos:

1. Vuelve a tu codespace. Deberías estar en `main` después del ejercicio anterior.
2. Abre un terminal en el codespace con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea y selecciona una rama nueva para el trabajo de filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio web:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, aparecerá un mensaje con la URL, parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo para abrir un navegador con `http://localhost:4321`, ciérralo seleccionando **x**.

5. Abre el sitio manteniendo pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando en el terminal la dirección del servidor Astro `http://localhost:4321`.

> [!NOTE]
> En un codespace, al seleccionar el enlace localhost en el terminal, se te redirige automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Es un túnel privado al codespace, que ahora aloja el servidor web.

### Explora el sitio web

Con el sitio en ejecución, explora sus funciones principales:

- **Home Page**: muestra una lista de juegos de mesa con títulos, imágenes y descripciones.
- **Game Details Page**: al seleccionar un juego, se abre una página con más información, como el título, la descripción, el editor y la categoría.

## Explora el backlog con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso indica cuál debes usar.

La implementación inicial del sitio funciona, pero queremos añadir más funcionalidades. Empieza por revisar el backlog. Al crear el proyecto a partir de la plantilla, se generó automáticamente una lista de incidencias. Pide a GitHub Copilot que te las muestre.

1. En el selector de agentes de la vista Chat, selecciona **Agent**. El agente planifica e implementa cambios en varios archivos, ejecuta comandos de terminal y usa herramientas de forma autónoma.

   ![Captura de pantalla del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no recomiendan un modelo en particular. Se usó Claude Sonnet 4.5 para crear el taller, por lo que se incluye en estas instrucciones con la esperanza de que las sugerencias sean relativamente coherentes y ofrezcan una buena experiencia. Sin embargo, los modelos de lenguaje grandes (LLM, por sus siglas en inglés) son probabilísticos y las sugerencias pueden diferir de las descritas en el taller. Es normal y esperable.

> [!NOTE]
> Debido a la naturaleza probabilística de los modelos de lenguaje grandes (LLM, por sus siglas en inglés), Copilot puede usar un comando del Model Context Protocol (MCP) diferente, pero debería poder completar la tarea.

3. Pide a Copilot que muestre las incidencias del backlog con este prompt:

   ```plaintext
   Muéstrame el backlog de elementos del repositorio de GitHub. Ayúdame a priorizarlos según su utilidad para los usuarios.
   ```

4. Selecciona **Continue** para ejecutar el comando que enumera las incidencias.
5. Revisa la lista generada.

Copilot también habrá priorizado los elementos según lo que considera más útil para los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere código, revisa el archivo de instrucciones que dará contexto a Copilot. Usarás el archivo de [interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que explica cómo añadir funcionalidad al sitio.

1. En tu codespace, abre `.github/instructions/ui.instructions.md`.
2. Observa las directrices generales para añadir funcionalidad, entre ellas:
   - una descripción de la arquitectura.
   - principios de diseño de componentes, capacidad de prueba y accesibilidad.
   - enlaces a archivos de instrucciones específicos para Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones permiten hacer referencia a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas a la ubicación del archivo de instrucciones. Así se pueden reutilizar directrices, dividir conjuntos complejos en partes más pequeñas y proporcionar ejemplos y plantillas.

## Implementa el filtrado

Para completar el filtrado, la aplicación necesita al menos tres cambios:

- añadir o ajustar la lógica de filtrado restante en la capa de datos (`src/lib/`).
- añadir o actualizar las pruebas del comportamiento del filtrado.
- actualizar la página de listado de juegos para incluir la interfaz de filtrado.

También hay que ejecutar las pruebas y confirmar que se superan antes de combinar los cambios. El modo de agente de Copilot puede encargarse de estas tareas.

1. Continúa en la conversación actual de Copilot o selecciona **New Chat** para iniciar otra.
2. Selecciona **Add Context**, **Instructions** y **ui** como archivo de instrucciones.

   ![Captura de pantalla de la selección del archivo de instrucciones de interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Comprueba que **Agent** sigue seleccionado en el selector de agentes de la vista Chat.

   ![Captura de pantalla del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Comprueba que **Claude Sonnet 4.5** sigue seleccionado como modelo.
5. Pide a Copilot que implemente la funcionalidad basándose en la incidencia relacionada del backlog:

   ```plaintext
   Actualiza el sitio para incluir el filtrado por editor y categoría según los requisitos de la incidencia relacionada del backlog de GitHub. Ya existe un helper de editores del ejercicio anterior; consérvalo y mejóralo si es necesario mientras completas el trabajo restante de la capa de datos, la interfaz y las pruebas. Asegúrate de que todas las pruebas se superan antes de terminar. El servidor ya está en ejecución; no hace falta iniciarlo.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos relacionados con la funcionalidad. Debería encontrar los helpers de la capa de datos, la interfaz y las pruebas; después, modificará los archivos y ejecutará las pruebas.

   ![Captura de pantalla de Copilot explorando los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar varios minutos según la complejidad de la tarea y del código base. Durante el trabajo pueden aparecer los botones **Keep** y **Undo** en el editor. Cuando termine, tendrás una opción **Keep** o **Undo** para cada cambio; no hace falta seleccionarlos mientras el agente sigue trabajando.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Captura de pantalla de un cuadro de diálogo de Copilot Chat que pide permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede que se produzcan pausas o que fallen algunas pruebas durante el proceso. Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea y no detectar errores.

   ![Captura de pantalla de una sesión completada en el modo de agente de Copilot](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explora el código generado para detectar posibles problemas.

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador con el sitio en ejecución y explora la funcionalidad nueva.
11. Cuando hayas confirmado que todo funciona y revisado el código, selecciona **Keep** en la ventana Copilot Chat.

## Resumen y siguientes pasos

¡Enhorabuena! En este ejercicio has usado el modo de agente de GitHub Copilot para añadir funcionalidades al sitio web de Tailspin Toys. Has aprendido cómo:

- el modo de agente de GitHub Copilot puede implementar funcionalidades en la interfaz y la capa de datos.
- el modo de agente de Copilot puede explorar el proyecto, identificar los archivos pertinentes y coordinar cambios.
- revisar los cambios y las pruebas generados por el modo de agente antes de combinarlos en el código base.

A continuación, [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar paginación

A medida que crezca la lista de juegos, será necesario habilitar la paginación. Aplica lo aprendido para pedir a Copilot que añada paginación al sitio. Ten en cuenta lo siguiente:

- sigue las prácticas recomendadas existentes, incluidos los archivos de instrucciones.
- decide cómo quieres implementar la paginación: por ejemplo, si el usuario podrá elegir el tamaño de página o si será fijo.
- proporciona a Copilot las directrices necesarias en el prompt.
- puede que tengas que iterar con GitHub Copilot, solicitar cambios y proporcionar contexto. Ese es el flujo normal al trabajar con Copilot.

## Recursos

- [Copilot: modos ask, edit y agent; para qué sirven y cuándo usarlos][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
