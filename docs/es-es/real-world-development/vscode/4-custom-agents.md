---
title: "Ejercicio 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de inteligencia artificial (IA) especializados para tareas o áreas concretas del flujo de trabajo de desarrollo. Al definir agentes en archivos Markdown de la carpeta `.github/agents` del repositorio, puedes proporcionar instrucciones, prácticas recomendadas, patrones de programación y conocimientos específicos que ayuden a Copilot a realizar ciertos tipos de trabajo con mayor eficacia. Los equipos pueden plasmar sus conocimientos en agentes reutilizables: un agente de accesibilidad que aplique las [Pautas de Accesibilidad para el Contenido Web (WCAG)][wcag], uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones coherentes.

Los agentes personalizados se definen en archivos Markdown de la carpeta `.github/agents` del proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML que incluye al menos `name` y `description`, seguido de un prompt Markdown que define el comportamiento, los conocimientos y las instrucciones del agente.

### Agentes personalizados y habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] se solapan en algunos aspectos: ambos se definen principalmente mediante archivos Markdown e indican a una IA cómo realizar tareas. La forma más sencilla de distinguirlos es que un **agente personalizado** es el trabajador y las **habilidades** son las herramientas.

Los agentes personalizados tienen su propia ventana de contexto y pueden coordinar habilidades e incluso otros agentes. En este ejercicio, el agente personalizado de accesibilidad revisará y actualizará el sitio de acuerdo con las directrices de accesibilidad; para ello, podría recurrir a habilidades como un flujo de trabajo de solicitudes de incorporación de cambios o una habilidad que ejecute y gestione pruebas.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Como con cualquier herramienta de IA, prueba e itera para encontrar lo que funciona en tus entornos y escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys se compromete a que todas las personas puedan usar su plataforma de financiación colectiva, independientemente de sus capacidades visuales o preferencias. Comentarios recientes indican que a algunos usuarios les cuesta leer el tema oscuro actual debido al contraste insuficiente entre el texto y el fondo. Para abordar este problema de accesibilidad, el equipo de diseño ha solicitado un modo de alto contraste que los usuarios puedan activar y desactivar.

Como la accesibilidad es fundamental, quieres implementar esta mejora cuanto antes. Para ello, usarás un agente personalizado.

En este ejercicio:

- revisarás un agente personalizado de accesibilidad existente.
- usarás el agente de accesibilidad en Copilot Chat para implementar un modo de alto contraste.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado de accesibilidad. Revisa su contenido para entender cómo orientará a Copilot.

Vuelve a tu codespace, abre un terminal y cambia a una rama nueva basada en `main` para el trabajo de accesibilidad. Así mantendrás separada la solicitud de incorporación de cambios de filtrado del Ejercicio 3.

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. Abre `.github/agents/accessibility.md`.
2. Fíjate en los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios para los agentes personalizados.

3. Lee las secciones siguientes, que describen:
   - las responsabilidades principales al generar código para un sitio web accesible.
   - las prácticas recomendadas de accesibilidad.
   - ejemplos de código en lenguaje de marcado de hipertexto (HTML), hojas de estilo en cascada (CSS) y JavaScript.
   - errores y problemas habituales.

## Usa el agente personalizado en Copilot Chat

VS Code muestra todos los agentes personalizados definidos en `.github/agents` en el selector de agentes situado en la parte inferior de la vista Copilot Chat. Puedes seleccionar un agente personalizado para limitar la sesión de chat a sus instrucciones y herramientas.

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los ejercicios, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso indica cuál debes usar.

1. En el selector de agentes de la vista Chat, selecciona **Agent** si aún no está seleccionado.

   ![Captura de pantalla del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona el selector de agentes de la parte inferior de la vista Chat, que muestra el agente activo (de forma predeterminada, **default**).
3. Selecciona **Accessibility agent** en la lista de agentes disponibles.
4. Envía este prompt al agente de accesibilidad:

   ```plaintext
   Añade un modo de alto contraste al sitio. Debe haber un conmutador para que el usuario pueda activar el alto contraste, y la preferencia debe persistir al volver a cargar la página mediante el almacenamiento local del navegador.
   ```

5. Copilot Chat explorará el código base, propondrá cambios y editará los archivos del proyecto. Cada edición aparecerá en el chat con la ruta del archivo y las diferencias para que puedas revisarla.
6. A medida que se apliquen los cambios, el indicador **Files changed** se actualizará para mostrar los archivos modificados por el agente.

> [!NOTE]
> El proceso puede tardar varios minutos. Copilot está haciendo cambios reales en el repositorio: editará componentes Astro, CSS y pruebas relacionadas, si las hay.

En el siguiente ejercicio revisarás y dirigirás el trabajo mientras está en curso.

## Resumen y siguientes pasos

En este ejercicio has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes de IA especializados en tareas y áreas concretas. Permiten plasmar los conocimientos y estándares del equipo en agentes reutilizables que orientan el trabajo de Copilot.

Has explorado estos conceptos:

- cómo se definen los agentes personalizados.
- cómo usar un agente personalizado en el modo de agente de Copilot Chat.

A continuación, [supervisarás y dirigirás el trabajo del agente][next-lesson]: revisarás los cambios mientras se realizan y añadirás un conmutador de modo claro a la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados de awesome-copilot][awesome-copilot-agents]

---

| [← Ejercicio anterior: Probar la funcionalidad con el servidor MCP de Playwright][previous-lesson] | [Siguiente ejercicio: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
