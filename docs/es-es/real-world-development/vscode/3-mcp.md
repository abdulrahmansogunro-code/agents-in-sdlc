---
title: "Ejercicio 3 - Probar la funcionalidad con el servidor Model Context Protocol (MCP) de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Modo de agente][previous-lesson] · [Siguiente ejercicio: Agentes personalizados →][next-lesson]

Acabas de crear una funcionalidad de filtrado con el modo de agente. Antes de abrir una solicitud de incorporación de cambios, confirma que funciona en el navegador. En lugar de probar la aplicación manualmente, conectarás el **servidor MCP de Playwright** y pedirás a Copilot que controle un navegador real. Después publicarás la rama y abrirás la solicitud.

En este ejercicio:

- aprenderás qué es el Model Context Protocol (MCP) y cómo los servidores MCP amplían las herramientas de Copilot.
- añadirás el servidor MCP de Playwright al espacio de trabajo.
- pedirás a Copilot que lo use para probar manualmente la funcionalidad de filtrado en un navegador.
- publicarás la rama y abrirás una solicitud de incorporación de cambios para el trabajo de filtrado.

## ¿Qué es el Model Context Protocol (MCP)?

El modo de agente es mucho más potente cuando puede acceder a recursos externos al editor. Copilot lo consigue mediante el Model Context Protocol (MCP), un estándar que permite al agente comunicarse con herramientas y servicios externos.

![Diagrama del funcionamiento interno del modo de agente y su interacción con el contexto, el modelo de lenguaje grande (LLM) y las herramientas, incluidas las que proporcionan los servidores MCP y las extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

El [Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada mediante recursos y realizar acciones en tu nombre mediante herramientas.

Se accede a estas herramientas y recursos a través de un servidor MCP, que actúa como puente entre el agente de inteligencia artificial (IA) y los servicios y herramientas externos. El servidor MCP gestiona la comunicación entre el agente y las herramientas externas, como las interfaces de programación de aplicaciones (API) existentes o las herramientas locales, por ejemplo, paquetes del gestor npm. Cada servidor MCP representa un conjunto distinto de herramientas y recursos a los que el agente puede acceder.

Algunos servidores MCP populares son:

- **[Servidor MCP de GitHub][github-mcp-server]**: proporciona acceso a varias API para gestionar repositorios de GitHub, crear repositorios, actualizar los existentes y gestionar incidencias y solicitudes de incorporación de cambios.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: proporciona funciones de automatización del navegador mediante Playwright. Permite al agente navegar por páginas web, rellenar formularios y seleccionar botones.

Hay muchos otros servidores MCP disponibles que proporcionan acceso a distintas herramientas y recursos. GitHub aloja un [registro de MCP][mcp-registry] para facilitar la búsqueda y las contribuciones al ecosistema.

> [!CAUTION]
> Por motivos de seguridad, trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de usar uno, revisa detenidamente su código fuente, verifica quién lo publica y considera las implicaciones de seguridad. Usa únicamente servidores MCP de confianza y ten cuidado al conceder acceso a recursos u operaciones sensibles.

## Revisa la configuración de MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en este espacio de trabajo de VS Code.

1. Abre `.vscode/mcp.json` en tu codespace.
2. Deberías ver que ya está configurado un servidor `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

La entrada `github` se incluye en la plantilla del proyecto, por eso Copilot pudo leer el backlog de incidencias en el ejercicio anterior. Usa el [servidor MCP remoto de GitHub][remote-github-mcp-server], así que no hay que instalar nada localmente: VS Code se conecta mediante HTTP y te autenticas en GitHub la primera vez que Copilot usa una de sus herramientas.

## Añade el servidor MCP de Playwright

Añade un segundo servidor. El [servidor MCP de Playwright][playwright-mcp-server] proporciona a Copilot un navegador que puede controlar para probar la funcionalidad.

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github` para que el archivo quede así:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

A diferencia del servidor remoto `github`, `playwright` es un servidor **local**: VS Code lo inicia en tu equipo mediante `npx @playwright/mcp@latest`. La opción `--headless` indica a Playwright que ejecute el navegador sin una ventana visible, algo necesario en un codespace, que no tiene escritorio para mostrarla.

> [!NOTE]
> Tailspin Toys ya usa Playwright para sus pruebas de extremo a extremo, así que normalmente el navegador necesario ya está instalado. Si Copilot informa de que falta un navegador, pídele que ejecute `npx playwright install chromium` y vuelve a intentarlo.

## Inicia y autoriza el servidor

VS Code inicia los servidores MCP **cuando se necesitan**: la primera vez que Copilot requiere las herramientas de un servidor, VS Code lo inicia y te pide confirmar que confías en él.

1. En `.vscode/mcp.json`, aparecerá una acción **Start** encima de la entrada `playwright`. Selecciónala para iniciar el servidor y confirmar que la configuración es correcta.
2. Si VS Code te pregunta si confías en el servidor, revisa la configuración y confirma que confías en él para poder iniciarlo.

Iniciarlo manualmente es opcional. Si omites este paso, VS Code lo iniciará y te pedirá que confirmes si confías en él la primera vez que Copilot necesite sus herramientas.

## Prueba la funcionalidad de filtrado

El [servidor MCP de Playwright][playwright-mcp-server] proporciona a Copilot un navegador real que puede controlar. En lugar de probar la aplicación manualmente, el agente puede abrir una página, navegar por ella, aplicar filtros y leer los resultados; después, resumirá lo que ha observado. Así puedes confirmar rápidamente que una funcionalidad se comporta como esperas sin salir de la conversación.

Internamente, el servidor MCP de Playwright usa el [árbol de accesibilidad de la página][playwright-mcp-server], no capturas de pantalla. El agente analiza elementos estructurados y etiquetados (botones, enlaces y elementos de lista), como hacen las tecnologías de asistencia. Por eso, una comprobación funcional rápida también ofrece una comprobación básica de accesibilidad.

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe la funcionalidad de filtrado:

```text
Usa el servidor MCP de Playwright para abrir un navegador con la aplicación en ejecución en http://localhost:4321 y comprobar la nueva funcionalidad de filtrado de juegos:

1. Ve a la página de juegos e indica cuántos aparecen.
2. Aplica un filtro de categoría y confirma que la lista solo muestra los juegos de esa categoría.
3. Borra el filtro, aplica uno de editor y confirma que la lista se actualiza para mostrar los juegos de ese editor.
4. Combina un filtro de categoría y otro de editor y confirma que los resultados respetan ambos.

Describe lo que observas en cada paso e indica cualquier comportamiento inesperado.
```

Copilot abrirá un navegador mediante el servidor MCP de Playwright, seguirá los pasos y comunicará el resultado. Compara el resumen con los criterios de aceptación de la incidencia. Si algo no funciona, pide más información o solicita que corrija el código antes de abrir una solicitud de incorporación de cambios.

> [!NOTE]
> Para esta prueba, la aplicación debe estar en ejecución en `http://localhost:4321`. Si detuviste el servidor de desarrollo, vuelve a iniciarlo antes de enviar el prompt. La primera vez que Copilot use el servidor MCP de Playwright puede ser necesario descargar un navegador. Si informa de que falta, pídele que ejecute `npx playwright install chromium` y vuelve a intentarlo.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publica la rama y crea una solicitud de incorporación de cambios

Ahora que has confirmado que la funcionalidad funciona, abre una solicitud de incorporación de cambios (PR) para que el equipo pueda revisarla. Primero publicarás la rama `filtering-vscode`.

1. Abre el panel **Source Control** del codespace y revisa los cambios de Copilot.
2. Prepara los cambios seleccionando el icono **+**.
3. Genera un mensaje de confirmación con el botón **Sparkle**.

   ![Captura de pantalla del panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

4. Selecciona **Publish** para enviar la rama al repositorio.

## Crea la solicitud de incorporación de cambios

Hay varias formas de crear una solicitud, como github.com o la interfaz de línea de comandos (CLI) de GitHub. Como ya estás trabajando con GitHub Copilot, pídele que la cree. Puede localizar la incidencia pertinente y asociarla a la solicitud.

1. Abre el panel Copilot Chat y selecciona **New Chat** para iniciar una sesión nueva.
2. Confirma que **Agent** está seleccionado en el selector de agentes para que Copilot pueda usar las herramientas de GitHub.
3. Pide a Copilot que cree una solicitud:

   ```plaintext
   Busca en el repositorio la incidencia relacionada con el filtrado por categoría y editor. Crea una solicitud de incorporación de cambios para la rama actual y vincúlala a la incidencia correspondiente.
   ```

4. Cuando sea necesario, selecciona **Continue** para permitir que Copilot recopile información y realice las operaciones. La primera vez que use una herramienta de GitHub, puede pedirte que te autentiques; sigue las instrucciones para permitirlo.
5. Observa cómo Copilot busca entre las incidencias, encuentra la correcta y crea la solicitud.
6. Selecciona el enlace de Copilot para revisar la solicitud, pero **no la combines todavía**.

## Resumen y siguientes pasos

En este ejercicio:

- has aprendido qué es el Model Context Protocol (MCP) y cómo los servidores MCP amplían las herramientas de Copilot.
- has añadido el servidor MCP de Playwright al espacio de trabajo.
- lo has usado para probar manualmente la funcionalidad de filtrado en un navegador antes de publicarla.
- has publicado la rama y abierto una solicitud de incorporación de cambios para el trabajo de filtrado.

Has usado un servidor MCP para *probar* una funcionalidad, pero MCP es solo una forma de ampliar Copilot. A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas concretas, como las revisiones de accesibilidad.

## Recursos

- [Qué es MCP y por qué todo el mundo habla de ello][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro MCP de GitHub][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
