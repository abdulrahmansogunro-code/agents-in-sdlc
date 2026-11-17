---
title: "Lección 5 - Personalizar y usar una habilidad quality-checks"
description: "Explora la habilidad quality-checks existente, personaliza el formato del informe y úsala para validar el filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Programar no consiste únicamente en escribir código. Ya hemos comprobado manualmente que funciona y hemos usado archivos de instrucciones para garantizar que cumple los estándares. Pero ¿qué ocurre con las pruebas, el lint y las demás partes de la integración continua (CI)?

Las **habilidades de agente** son adecuadas para estas tareas. Ayudan a Copilot a entender cómo realizar correctamente operaciones como estas.

En esta lección:

- explorarás la habilidad `quality-checks` existente.
- personalizarás el formato de los resultados.
- volverás a cargar la habilidad y la ejecutarás.

## Escenario

Tailspin Toys usa la habilidad `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las habilidades de agente reúnen instrucciones reutilizables para tareas, scripts ejecutables y recursos de apoyo que un agente carga cuando los necesita. Una habilidad consiste principalmente en una carpeta con su nombre y un archivo Markdown `SKILL.md`. El archivo contiene un frontmatter con el nombre y la descripción de la habilidad, una descripción general de sus funciones y directrices sobre cuándo usarla. La carpeta también puede incluir subcarpetas con scripts y otros recursos.

> [!NOTE]
> Las subcarpetas y los archivos adicionales son opcionales. La habilidad `quality-checks` de Tailspin Toys solo contiene `SKILL.md` porque utiliza los comandos existentes del proyecto.

Las habilidades pueden estar en la carpeta `.github/skills` del proyecto para que el equipo las comparta y reutilice, o en la carpeta global de habilidades del usuario, `~/.copilot/skills`.

## Explora la habilidad

Explora la habilidad `quality-checks` que creó el equipo de Tailspin Toys para ejecutar pruebas unitarias, lint y comprobaciones de tipos.

1. Vuelve a tu codespace. En el editor de Codespaces, abre `.github/skills/quality-checks/SKILL.md`.
2. Lee los campos `name` y `description` de la parte superior. La descripción ayuda a Copilot a determinar cuándo debe usar la habilidad.
3. Lee las instrucciones y observa cómo guían a Copilot durante las pruebas y el lint.
4. Comprueba que la habilidad aún no contiene una sección de formato para el informe de resultados.

## Ejecuta la habilidad antes de cambiarla

Puedes llamar a las habilidades directamente desde Copilot CLI o pedirlas en lenguaje natural. Pide a Copilot que ejecute las tres comprobaciones de la habilidad.

1. Vuelve a la conversación de filtrado en modo Interactive.
2. Usa este prompt:

   ```plaintext
   Ejecuta la habilidad quality-checks para las pruebas unitarias, el lint y las comprobaciones de tipos.
   ```

3. Lee el informe que aparece al final.

## Personaliza el informe

Mejora el informe para que indique qué se ejecutó, si terminó correctamente y qué comunicaron las herramientas. Actualiza la habilidad para generarlo.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade esta sección al final del archivo:

   ```markdown
   ## Formato de salida de resultados

   Al terminar, informa de cada comando ejecutado e indica si se completó correctamente, falló o quedó bloqueado. Incluye el número de pruebas, la duración, los errores, las advertencias y otras métricas solo si la herramienta las proporciona. Indica el siguiente paso para cada fallo o bloqueo y nunca describas una comprobación omitida o incompleta como superada.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la habilidad actualizada

Ahora comprueba el resultado. Copilot CLI puede volver a cargar las habilidades editadas sin reiniciar la conversación.

1. Escribe:

   ```plaintext
   /skills reload
   ```

2. Usa exactamente el mismo prompt de antes:

   ```plaintext
   Ejecuta la habilidad quality-checks para las pruebas unitarias, el lint y las comprobaciones de tipos.
   ```

3. Lee el informe y compáralo con el primero.

## Resumen y siguientes pasos

Has personalizado y usado una habilidad de agente existente. En esta lección:

- has explorado la habilidad `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- has personalizado el formato de los resultados.
- has vuelto a cargar y ejecutado la habilidad.

Este cambio acompañará al filtrado en la solicitud de incorporación de cambios de la funcionalidad. A continuación, permitirás que Copilot interactúe directamente con el sitio [mediante el servidor del Model Context Protocol (MCP) de Playwright][next-lesson].

## Más ejemplos de habilidades

Estos ejemplos de la comunidad son referencias, no tareas adicionales:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de trabajo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y un script de exportación incluido: `drawio`][drawio-example]
- [Pruebas del navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
