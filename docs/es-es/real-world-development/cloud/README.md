---
slug: es-es/real-world-development/cloud
title: "Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El **[agente de GitHub Copilot en la nube](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** permite que GitHub Copilot trabaje de forma asíncrona en la nube. Le asignas trabajo en GitHub y el agente en la nube lo realiza en segundo plano: explora el repositorio, hace cambios y abre una solicitud de incorporación de cambios mientras tú te ocupas de otras tareas.

En estos ejercicios añadirás instrucciones personalizadas que seguirá el agente y, después, le asignarás una incidencia de GitHub para que la implemente. Revisarás y usarás agentes personalizados para orientar su enfoque, supervisarás y dirigirás las sesiones desde el panel de agentes y, por último, revisarás sus solicitudes de incorporación de cambios y repetirás el proceso sobre los resultados.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea el repositorio y el codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade instrucciones personalizadas para el agente en la nube |
| [2. Agente en la nube][ex2] | Agente asíncrono | Asigna incidencias al agente de GitHub Copilot en la nube |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revisa y usa agentes personalizados |
| [4. Gestión de agentes][ex4] | Supervisión | Supervisa y dirige sesiones de agente |
| [5. Iteración][ex5] | Revisión | Revisa las solicitudes, itera sobre el trabajo de Copilot y elige los siguientes pasos |

## Requisitos previos

Antes de empezar este taller, asegúrate de disponer de:

- [ ] Una cuenta de GitHub con un plan **Copilot Student, Pro, Pro+, Business o Enterprise** activo
- [ ] El agente de GitHub Copilot en la nube habilitado para tu cuenta u organización

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye el agente, el Model Context Protocol (MCP), la revisión de código y las funciones de Copilot CLI que se usan en este taller, por lo que permite completar todos los entornos.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> El agente en la nube está disponible en los planes **Copilot Student, Pro, Pro+, Business y Enterprise**; solo queda excluido Copilot Free. En Copilot Business o Enterprise, un administrador debe habilitarlo para la organización.

> [!NOTE]
> Este entorno no incluye MCP. Para aprender a usar servidores MCP con Copilot, consulta el [entorno de CLI](../cli/) o el [entorno de VS Code](../vscode/).

## Comenzar

**[Empieza por el Ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
