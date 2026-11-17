---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisa el trabajo

Durante este taller has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario y añadir funcionalidades. Le pediste que añadiera documentación al código, desarrollara una función de juegos relacionados para que el equipo de diseño pudiera iterar sobre ella e implementara mejoras de accesibilidad, incluidos modos de alto contraste y claro. Revisarás los cambios de código y, si es necesario, darás indicaciones a Copilot para mejorarlos.

### Escenario

Los fundamentos del diseño de software y DevOps no cambian al añadir IA generativa. Siempre hay que revisar el código generado y seguir el proceso habitual de DevOps. Antes de habilitar la revisión para el resto del equipo, revisa las propuestas de GitHub Copilot para la documentación, los juegos relacionados y la accesibilidad.

## Seguridad y agente de GitHub Copilot en la nube

Como el agente de Copilot en la nube realiza tareas de forma asíncrona y sin supervisión, se han establecido restricciones de seguridad:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que usa para su código.
- El agente en la nube se ejecuta en GitHub Actions, donde crea un entorno independiente y efímero para trabajar.
- Los flujos de trabajo de GitHub Actions requieren la aprobación de una persona antes de ejecutarse.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores MCP.

## Revisa la documentación generada

Empieza por la primera solicitud de incorporación de cambios (PR) que generó el agente de GitHub Copilot en la nube: añadir documentación al código. Usa la interfaz habitual de solicitudes de GitHub.com.

> [!NOTE]
> Es posible que aparezca una advertencia que indique que el firewall bloquea a GitHub Copilot. Es **lo esperado**, ya que el acceso a recursos externos, incluidas las llamadas a servidores MCP externos, está limitado de forma predeterminada. Si quieres, puedes [personalizar o deshabilitar el firewall del agente de Copilot en la nube][agent-firewall].

1. Vuelve al repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes.
3. Abre la solicitud cuyo título sea parecido a **Add missing documentation**.

> [!NOTE]
> Si Copilot sigue trabajando, la solicitud tendrá la marca **[WIP]**. Espera a que termine; puede tardar unos minutos.

4. Cuando la solicitud esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que incluye los nuevos comentarios TSDoc y otra documentación. Los cambios exactos pueden variar.

   Busca comentarios TSDoc, convenciones de TypeScript y encabezados de comentarios. Estas indicaciones proceden de los archivos de instrucciones que revisaste al principio del Ejercicio 2.

6. Cuando hayas revisado las actualizaciones y estés conforme, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Busca un indicador que señale que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Los flujos deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían completarse correctamente. El proceso puede tardar unos minutos.

## Solicita cambios a GitHub Copilot

La colaboración con Copilot en una solicitud no es unidireccional. Puedes mencionarlo en comentarios de la solicitud o en comentarios insertados en el código, igual que harías con otra persona del equipo. Copilot verá los comentarios e iniciará otra sesión para resolverlos. Como los resultados no son deterministas, no hay un prompt único que debas usar. Puedes pedirle, por ejemplo:

- que añada encabezados breves al principio de cada archivo de código para explicar su contenido.
- que añada comentarios TSDoc a archivos TypeScript y Astro.
- que cree un README con una descripción de la estructura de la aplicación Astro.

1. Añade un comentario para solicitar cambios en la documentación generada y menciona a **@copilot**, como harías con cualquier usuario. Puedes usar una de las ideas anteriores u otra petición relacionada con la documentación del código base.
2. Selecciona **View Session** para observar cómo Copilot trabaja. Verás que inicia una sesión nueva para realizar los cambios.
3. Selecciona **Back to pull request** para volver a la solicitud.

   ![Volver a la solicitud de incorporación de cambios](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine, aparecerá una confirmación nueva en la solicitud.
5. Selecciona **Files changed** y revisa los cambios.

Puedes seguir iterando hasta que estés conforme. Después, puedes marcar la solicitud como lista para revisión y combinarla en la rama principal.

![Marcar la solicitud como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Vuelve a la solicitud que Copilot generó para mostrar juegos relacionados en la página de detalles.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la solicitud con un título parecido a **Show related games on the game details page**.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado los cambios y estés conforme, vuelve a **Conversation** y desplázate hacia abajo.
6. Busca un indicador que señale que hay flujos de trabajo pendientes de aprobación.
7. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

8. Los flujos deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían completarse correctamente. El proceso puede tardar unos minutos.
9. **Opcional:** puedes cambiar a esta rama en el codespace y probar manualmente la funcionalidad de juegos relacionados. Abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo, **copilot/fix-8**:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot ha creado la funcionalidad de juegos relacionados. Como antes, puedes iterar con el agente en la nube para solicitar cambios. Por ejemplo, puedes pedirle que ajuste el número de juegos relacionados o que añada encabezados y comentarios TSDoc. Recuerda que esta tarea se asignó **antes** de actualizar las instrucciones personalizadas. Para solicitar cambios, añade otro comentario en la pestaña **Conversation**; Copilot lo verá e iniciará una sesión nueva.

## Revisa las mejoras de accesibilidad

Por último, revisa las mejoras de accesibilidad implementadas con el agente personalizado. La solicitud debe incluir el modo de alto contraste que asignaste en el Ejercicio 3 y el modo claro que solicitaste desde Mission control en el Ejercicio 4.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la solicitud con un título parecido a **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot sigue trabajando, la solicitud tendrá la marca **[WIP]**. Espera a que termine; puede tardar unos minutos.

4. Selecciona **Files changed** para revisar el código generado.
5. Revisa la implementación y presta atención a:
   - los componentes de interfaz para alternar entre modos.
   - el uso del almacenamiento local para conservar las preferencias.
   - los cambios de hojas de estilo en cascada (CSS) o de estilos para los modos de alto contraste y claro.
   - los atributos de accesibilidad (etiquetas de Aplicaciones de Internet Enriquecidas Accesibles (ARIA), navegación con teclado, etc.).
   - el código JavaScript o TypeScript que gestiona el cambio de modo.
6. Cuando hayas revisado los cambios y estés conforme, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Busca un indicador que señale que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Los flujos deberían aparecer en la sección de comprobaciones de la solicitud. Si todo va bien, deberían completarse correctamente. El proceso puede tardar unos minutos.
10. **Opcional:** puedes cambiar a esta rama en el codespace y probar manualmente las mejoras de accesibilidad. Abre el terminal y ejecuta estos comandos; sustituye `<branch-name>` por el nombre de la rama creada por Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Después, inicia la aplicación y prueba los conmutadores de alto contraste y modo claro en el navegador. Confirma que funcionan y que las preferencias se conservan al volver a cargar la página.

El agente personalizado de accesibilidad ayudó a Copilot a implementar estas mejoras siguiendo prácticas recomendadas de accesibilidad. Si detectas problemas o posibles mejoras, menciona a **@copilot** en un comentario y solicita los cambios, como hiciste con las otras solicitudes.

## Ejercicio opcional: sigue delegando

El agente en la nube funciona mejor cuando le asignas elementos reales del backlog y puedes ocuparte de otras tareas. Para crear ese hábito, registra más incidencias en el repositorio y asígnaselas a Copilot. Algunas ideas:

- Crear un formulario para expresar interés en un juego en la página de detalles.
- Implementar paginación en la página de la lista de juegos.
- Añadir validación de entradas y gestión de errores a los helpers de acceso a datos.

## Resumen

Has completado el entorno del agente en la nube. En estos ejercicios:

- **Has inspeccionado los archivos de instrucciones personalizadas del repositorio** para observar su efecto en el trabajo del agente.
- **Has asignado incidencias al agente de Copilot en la nube** y has observado cómo prepara el entorno, planifica y trabaja de forma asíncrona.
- **Has creado y usado un agente personalizado** para la accesibilidad y has añadido modos de alto contraste y claro.
- **Has usado la página de agentes de Copilot como centro de control** para supervisar y dirigir la sesión de accesibilidad mientras estaba en curso.
- **Has revisado e iterado sobre las solicitudes del agente en la nube**, has mencionado a `@copilot` para solicitar cambios y has aprobado flujos de trabajo.

## Repaso y siguientes pasos

Has completado el entorno del agente en la nube. Los otros entornos complementan lo que has practicado:

- 🖥️ **[Entorno de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración con MCP directamente desde el IDE.
- 💻 **[Entorno de CLI](../../cli/)**: entrega desde el terminal dos cambios revisados con los modos Plan y Autopilot, habilidades de agente, un agente de QA personalizado, Playwright MCP, Agent Merge y el puente opcional `/delegate` al agente en la nube.

En tu propio repositorio, puedes probar estas ideas:

- Asignar al agente en la nube una incidencia de refactorización o cobertura de pruebas.
- Crear un agente personalizado para otro ámbito.
- Configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de trabajo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el firewall del agente de Copilot en la nube][agent-firewall]

---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
