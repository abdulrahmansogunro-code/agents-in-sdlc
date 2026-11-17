---
title: "Lección 10 - Repaso y siguientes pasos"
description: "Repasa el flujo de trabajo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has usado GitHub Copilot CLI en un flujo continuo de Tailspin Toys. Has:

- preparado un codespace, instalado Copilot CLI, explorado el proyecto y localizado la incidencia de filtrado del backlog.
- añadido valoraciones por estrellas, revisado el resultado en un navegador reenviado y combinado manualmente tu primera solicitud de incorporación de cambios (PR).
- partido de la incidencia de filtrado, definido el enfoque en el modo Plan, desarrollado la funcionalidad en Autopilot y revisado el resultado en Interactive.
- guiado al agente con instrucciones personalizadas, personalizado la habilidad `quality-checks` existente y usado la habilidad para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- añadido el servidor Model Context Protocol (MCP) de Playwright y usado el servidor para explorar el filtrado en un navegador real.
- creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas en el navegador.
- revisado todo el cambio de filtrado y autorizado Agent Merge para esa solicitud.
- explorado comandos de barra para gestionar el contexto y los modelos, compartir sesiones y delegar trabajo opcionalmente en la nube.

## Qué has entregado

El taller incluye dos hitos de solicitudes de incorporación de cambios, cada uno en su propia rama creada a partir de `main` actualizado:

1. **Valoraciones por estrellas:** mostrar el valor existente de `starRating` y un estado explícito cuando no hay valoración en las tarjetas de juegos.
2. **Filtrado y flujo de calidad:** implementar el filtrado, actualizar las instrucciones y aplicarlas a la funcionalidad, personalizar el informe de `quality-checks`, crear un perfil de QA e incluir las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su solicitud de incorporación de cambios, has usado la misma conversación y rama. Hemos reunido el trabajo en una solicitud para simplificar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias formas: con pruebas automatizadas, examinando el sitio en el navegador y usando Copilot para explorar el navegador mediante MCP. La habilidad `quality-checks` ejecutó las pruebas unitarias, el lint y las comprobaciones de tipos, y generó el nuevo formato de informe. QA reunió esos resultados con la revisión de los requisitos y la cobertura de pruebas antes de abrir la solicitud.

Las pruebas nuevas deben cubrir carencias reales; una ejecución de QA que no necesite añadir pruebas también puede ser correcta. Revisa el código y las pruebas antes de autorizar la combinación, y actualiza las pruebas afectadas después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas a Copilot condicionan su trabajo. En este taller has actualizado las instrucciones, personalizado una habilidad, creado un perfil de QA y configurado un servidor MCP. Reutiliza estas personalizaciones en otras conversaciones y adáptalas a las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados reales de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Usa **Plan** para pensar en un enfoque antes de empezar a desarrollar, **Interactive** para mantenerte al tanto de los cambios acotados y **Autopilot** para las tareas bien delimitadas. Elige un modelo más rápido para los cambios rutinarios y otro más capaz para el trabajo complejo.

El contexto sigue siendo tan importante como la infraestructura. Describir con claridad *qué* quieres desarrollar, *por qué* y *cómo* influye mucho en el resultado.

## Más opciones para explorar

Has completado el flujo principal. También puedes probar algunas otras funciones de CLI:

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para hablar sobre un problema y obtener otra perspectiva.
- `/fleet` para coordinar tareas independientes en paralelo.
- `/worktree` para aislar una tarea.
- `/delegate` para enviar una tarea a Copilot cloud agent.

## Siguientes pasos

La mejor forma de mejorar con cualquier herramienta es seguir usándola. Utilízala para código de producción, proyectos personales o esa pequeña aplicación que llevas años pensando en crear. Comparte lo aprendido con el equipo y aprende de sus experiencias. Como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller de Copilot cloud agent][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
