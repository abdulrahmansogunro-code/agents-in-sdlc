---
title: "Lección 9 - Comandos de barra de GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar trabajo opcionalmente a un agente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier herramienta de CLI, GitHub Copilot CLI incluye muchos comandos de barra para interactuar con ella. Estos comandos permiten acceder a funciones avanzadas, información interna y opciones de configuración adicionales. Ya has usado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora explorarás otros comandos útiles.

En esta lección:

- usarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- usarás `/model` para explorar los modelos disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar árboles de trabajo y delegar tareas al agente en la nube.

## Escenario

Has terminado el flujo principal de CLI. Ahora explorarás otras funciones: gestionar el contexto, cambiar de modelo, compartir sesiones y delegar trabajo opcionalmente a [Copilot cloud agent][about-cloud-agent].

## Explora el contexto de Copilot CLI

En tareas amplias o complejas puedes alcanzar el límite de la ventana de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando es necesario, y puedes inspeccionar o compactar el contexto tú mismo con comandos de barra.

1. Vuelve a tu codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y la distribución del contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio disponible.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Puede que no haya cambiado mucho si la conversación ya era breve.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto cuando la ventana se llena. Usa `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` si vas a cambiar a una tarea no relacionada y quieres iniciar una conversación nueva.

## Elige el modelo

Los modelos tienen distintas ventajas y cada desarrollador puede tener sus propias preferencias. Copilot CLI permite mostrar y seleccionar el modelo que quieres usar.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información sobre su uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Colaborar y compartir lo aprendido ayuda a todo el equipo a mejorar el uso de las herramientas de IA. El comando `/share` permite exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartirla o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` de la versión instalada.
2. Si quieres compartir la sesión, elige el destino adecuado, como `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo a alguien o publicarlo. Las exportaciones pueden incluir prompts, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de la conversación que el equipo no tenga previsto compartir.

## Opcional: amplía el trabajo o delégalo

El flujo principal del taller ha terminado. Copilot CLI también tiene comandos para tareas más amplias:

- `/fleet` puede dividir tareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un árbol de trabajo de Git aislado para una tarea distinta.
- `/delegate` puede enviar una tarea a Copilot cloud agent, que trabaja de forma asíncrona y puede abrir una solicitud de incorporación de cambios.

Estos comandos son opcionales, ya que pueden crear árboles de trabajo adicionales o trabajo remoto. Antes de probarlos, inicia una tarea nueva y bien delimitada, y revisa el resultado con tu flujo habitual. Si quieres profundizar en el trabajo asíncrono de los agentes, continúa con el [taller de agentes en la nube][cloud-workshop].

## Resumen y siguientes pasos

Los comandos de barra de Copilot CLI permiten configurarlo, compartir sesiones y ver qué ocurre internamente. En esta lección:

- has usado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- has usado `/model` para explorar los modelos disponibles.
- has aprendido cómo `/share` puede exportar o compartir una sesión.
- has explorado comandos opcionales para trabajar en paralelo, usar árboles de trabajo y delegar tareas al agente en la nube.

Copilot CLI incluye muchos más comandos de barra. Para terminar el recorrido, [repasarás lo aprendido][next-lesson] y descubrirás los siguientes pasos.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca de Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
