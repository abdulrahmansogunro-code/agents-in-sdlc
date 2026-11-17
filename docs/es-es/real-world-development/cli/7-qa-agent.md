---
title: "Lección 7 - Crear y usar un agente de QA"
description: "Crea un agente personalizado de QA que combine los requisitos de la incidencia, la habilidad quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has usado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y el servidor del Model Context Protocol (MCP) de Playwright para observar la experiencia de filtrado en un navegador. Ahora reunirás estas capacidades en un agente personalizado con un proceso de QA bien definido.

En esta lección:

- explorarás cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP.
- crearás e inspeccionarás un perfil reutilizable de control de calidad.
- seleccionarás el agente de QA y revisarás sus conclusiones respecto a la incidencia de filtrado.

## Escenario

Antes de abrir una solicitud de incorporación de cambios (PR), Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador. Un agente personalizado puede coordinar el proceso de QA y generar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot definida en un perfil de Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles para el agente. En este taller definirás el rol de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Las personalizaciones que has usado tienen funciones distintas. Las instrucciones del repositorio describen los estándares del equipo. La habilidad `quality-checks` reúne comprobaciones repetibles. Playwright MCP proporciona herramientas para el navegador. El perfil de QA indica a Copilot cómo utilizar esas capacidades para evaluar los requisitos y comunicar sus conclusiones. No sustituye a las demás personalizaciones ni requiere otra conversación.

## Crea el perfil de QA

Antes de abrir la solicitud de incorporación de cambios de la funcionalidad, pide a Copilot que cree un perfil de QA reutilizable. El perfil definirá las comprobaciones de QA y los límites que debe respetar.

1. Vuelve a tu codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Crea un agente personalizado llamado QA en .github/agents/qa.agent.md. Debe comprobar las funcionalidades respecto a sus incidencias y los requisitos acordados, seguir las instrucciones del repositorio, ejecutar la habilidad quality-checks, usar Playwright MCP para verificar el comportamiento y añadir pruebas si falta cobertura.

   Debe comunicar cada requisito como superado, no superado o bloqueado, con pruebas que respalden el resultado. Debe pedir permiso antes de cambiar código de implementación y no debe confirmar cambios ni abrir solicitudes de incorporación de cambios.

   Por ahora, crea únicamente el perfil para que pueda revisarlo.
   ```

## Inspecciona el perfil

Antes de usar el agente nuevo, revisa su perfil para confirmar que Copilot ha capturado el flujo de QA y sus límites previstos. Así evitarás que el perfil esté incompleto o permita cambios demasiado amplios cuando solo quieres verificar la funcionalidad.

1. Escribe `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. Se requiere `description`; `name` es opcional, pero incluirlo da al agente un nombre claro en la interfaz.
3. Lee las instrucciones del perfil y confirma que QA parte de los requisitos, sigue las instrucciones del repositorio, ejecuta la habilidad `quality-checks` y usa Playwright MCP.
4. Confirma que QA presenta pruebas de respaldo, pide permiso antes de cambiar código de implementación y no confirma cambios ni abre solicitudes de incorporación de cambios.
5. Si el perfil generado omite alguna de estas responsabilidades o límites, pide al agente predeterminado que lo revise antes de continuar.

## Ejecuta QA respecto a la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Reanuda la misma conversación de filtrado después de crear el perfil y, después, selecciona QA para que pueda usar la incidencia y las decisiones de planificación que ya tiene en contexto.

1. Activa el agente con este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, es posible que no aparezca en la lista de agentes disponibles. Aun así, puedes activarlo con el comando anterior.

2. Usa este prompt para pedir al agente de QA que revise la funcionalidad:

   ```plaintext
   Revisa la funcionalidad de filtrado respecto a la incidencia y las decisiones del plan. ¿Está lista para una solicitud de incorporación de cambios?
   ```

3. Deja que el agente de QA trabaje.
4. Cuando termine, lee el informe.

## Resumen y siguientes pasos

Has añadido un rol especializado reutilizable y has revisado su trabajo. En esta lección:

- has explorado cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP.
- has creado e inspeccionado un perfil reutilizable de control de calidad.
- has seleccionado el agente de QA y revisado sus conclusiones respecto a la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y el informe de verificación listos para revisión. A continuación, [los reunirás en una solicitud de incorporación de cambios de la funcionalidad y usarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
