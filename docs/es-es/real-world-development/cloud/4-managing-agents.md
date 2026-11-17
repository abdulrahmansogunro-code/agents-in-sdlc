---
title: "Ejercicio 4 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los dos ejercicios anteriores pediste al agente de Copilot en la nube que se encargara de tres tareas diferentes para mejorar la experiencia de usuario y añadir funcionalidad. Aunque el agente trabaja de forma asíncrona y autónoma, sigue siendo importante supervisar estas tareas.

Puedes gestionar las tareas asignadas al agente mediante varias herramientas, incluida la [página de agentes][agents-page] de GitHub.com. Desde este centro de control puedes ver todas las tareas de los agentes que tienen solicitudes de incorporación de cambios abiertas, explorar las operaciones realizadas e incluso dirigir una sesión que esté en curso.

En este ejercicio:

- explorarás la página de agentes para supervisar las tareas del agente en la nube.
- dirigirás una sesión en curso para solicitar funcionalidad adicional.

## Escenario

Después de asignar al agente la creación de un modo de alto contraste, el equipo se dio cuenta de que también sería un buen momento para añadir un modo claro. Como ya se estaba trabajando en actualizar los estilos del sitio y añadir la función de alternar modos, parecía lógico incluirlo. Dirigirás el trabajo del agente para que añada el modo claro además del alto contraste.

## Revisa las tareas del agente en la nube

Consulta el estado actual de todas las tareas asignadas al agente de Copilot en la nube.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas del panel principal y del panel izquierdo. Deberías ver las tareas que has asignado a Copilot, entre ellas:
   - actualizar la documentación del código base.
   - generar API para modificar juegos.
   - añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en curso y revisa las acciones que ha realizado Copilot. Pueden incluir:
   - obtener el código del repositorio.
   - crear el entorno de trabajo de Copilot.
   - configurar servidores MCP.
   - realizar distintas acciones para completar la tarea asignada.

> [!NOTE]
> Los pasos exactos de la lista varían en función del estado del trabajo de Copilot y del enfoque que haya seguido.

4. Observa también el panel de solicitudes de incorporación de cambios que aparece a la derecha. Desde ahí puedes consultar la solicitud y los archivos modificados para supervisar el trabajo.

## Dirige el agente en la nube

Ahora que has visto las tareas activas, pide a Copilot que añada el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto depende del nombre que haya elegido Copilot y del estado del trabajo.

   ![Sesión de accesibilidad en Mission control](../../../_images/ex6-accessibility-session.png)

2. Supervisa la sesión durante unos minutos hasta que indique que ha terminado la configuración y ha empezado a trabajar. Lo sabrás cuando empiecen a aparecer mensajes parecidos a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   Mientras trabajamos en el modo de alto contraste, añadamos también un modo claro. Debe haber un conmutador para este modo, de forma que los usuarios puedan seleccionar el modo de visualización que prefieran.
   ```

   ![Captura de pantalla de la tarea del agente en la nube en la página de agentes, con el cuadro de diálogo para dirigir la sesión activa de Copilot resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Observa cómo Copilot confirma que lo ha recibido y lo incorpora al flujo de trabajo.

## Deja que Copilot trabaje

Copilot continuará con la tarea actualizada. Incorporará la nueva solicitud al flujo cuando termine el paso en el que estaba trabajando al recibir el mensaje.

Como antes, el proceso tardará varios minutos. Es un buen momento para hacer una pausa y reflexionar sobre lo que has aprendido y explorado hasta ahora.

## Resumen y siguientes pasos

En este ejercicio has explorado la página de agentes de Copilot, el centro de control para supervisar y dirigir las tareas del agente de GitHub Copilot en la nube. Puedes realizar el seguimiento de tareas activas y completadas, revisar el trabajo e incluso redirigir las tareas en curso para ajustar su alcance o añadir indicaciones.

Has explorado estos conceptos:

- has usado Mission control y la página de agentes para supervisar las tareas del agente en la nube.
- has redirigido una sesión en curso para solicitar funcionalidad adicional.

Mientras Copilot termina el trabajo sobre la accesibilidad, puedes [iterar sobre las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
