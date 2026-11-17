---
title: "Lección 6 - Validar la funcionalidad con Playwright y el Model Context Protocol (MCP)"
description: "Inspecciona o configura Playwright MCP en Copilot CLI y úsalo para explorar en el navegador la funcionalidad de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos señalado, programar no consiste únicamente en escribir código. También hay que trabajar con datos y servicios externos, y permitir que Copilot acceda a automatizaciones adicionales. Para ello se usan los servidores del Model Context Protocol (MCP), que amplían Copilot CLI con herramientas y servicios.

En esta lección:

- aprenderás qué es el Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- añadirás el servidor MCP de Playwright si aún no está disponible.
- pedirás al agente que controle un navegador y explore la funcionalidad de filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero validar cambios en la interfaz de usuario requiere interactuar con ella. Quieres que Copilot pueda usar el sitio web como lo haría un usuario para automatizar mejor la validación y tener más confianza en que los cambios funcionan como se espera.

## ¿Qué es el Model Context Protocol (MCP)?

El [Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de inteligencia artificial (IA) se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada y realizar acciones en tu nombre.

Se accede a estas herramientas y recursos a través de un servidor MCP, que actúa como puente entre el agente de IA y los servicios y herramientas externos. Cada servidor MCP representa un conjunto distinto de herramientas y recursos a los que el agente puede acceder.

Algunos servidores MCP populares son:

- **[Servidor MCP de GitHub][github-mcp]**: proporciona acceso a las interfaces de programación de aplicaciones (API) para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: proporciona funciones de automatización del navegador mediante Playwright.

Hay muchos otros servidores MCP disponibles. GitHub aloja un [registro de MCP][mcp-registry] para facilitar la búsqueda y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de usar uno, revisa su código fuente, verifica quién lo publica y considera las implicaciones de seguridad.

## Añade el servidor MCP de Playwright

Si el servidor MCP de Playwright aún no está disponible, añádelo para que Copilot pueda interactuar con el sitio web como lo haría un usuario.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos de configuración y continúa con la sección siguiente.

1. Vuelve a tu codespace.
2. En Copilot CLI, abre el cuadro de diálogo para añadir un servidor MCP con este comando:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** pulsando <kbd>Enter</kbd> y, a continuación, pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el cuadro de diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor MCP.
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de diálogo MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Antes confirmaste manualmente que la funcionalidad se comporta como esperabas. Ahora usarás el servidor MCP de Playwright disponible en Copilot para hacer lo mismo.

1. Usa el siguiente prompt para pedir a Copilot que valide la funcionalidad con el servidor MCP de Playwright:

   ```plaintext
   Inicia la aplicación y usa Playwright MCP para comprobar el filtrado de acuerdo con la incidencia y el plan. Dime qué funciona y qué no, sin hacer cambios. Detén el servidor que hayas iniciado cuando termines.
   ```

> [!NOTE]
> No es necesario pedir explícitamente a Copilot que use el servidor MCP; normalmente lo deduce por su cuenta. Aun así, indicar la herramienta puede orientar el trabajo, mejorar la coherencia y ahorrar tokens.

2. Observa cómo Copilot enumera los pasos que realiza en el navegador para comprobar que la funcionalidad funciona.
3. Lee el informe y confirma que todo se comporta como se espera.

Copilot iniciará el servidor, usará Playwright para interactuar con el sitio web, detendrá el servidor y te dará un informe.

## Resumen y siguientes pasos

Has usado el servidor MCP de Playwright para explorar tu funcionalidad con un navegador real desde Copilot CLI. En esta lección:

- has aprendido qué es el Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- has añadido el servidor MCP de Playwright, si aún no estaba disponible.
- has pedido al agente que controlara un navegador y explorara la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de QA][next-lesson] que combinará la habilidad y las herramientas del navegador en un rol especializado.

## Recursos

- [Qué es MCP y por qué todo el mundo habla de ello][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
