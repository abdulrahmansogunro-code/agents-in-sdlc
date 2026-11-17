---
title: "Ejercicio 5 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] |
|:--|

En el modo de agente, GitHub Copilot trabaja de forma autónoma: explora el código base, propone cambios, edita archivos y ejecuta comandos. Como trabaja en tu equipo en tiempo real, Copilot Chat en VS Code te muestra cada llamada a una herramienta y cada edición a medida que se producen. Puedes revisar cada diferencia, aceptar o rechazar cambios concretos y dirigir la conversación con prompts de seguimiento para refinar o ampliar el trabajo sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos en los archivos.
- dirigirás al agente durante la sesión para añadir un conmutador de modo claro junto al de alto contraste.

## Escenario

El agente personalizado de accesibilidad que utilizaste en el [Ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita también un modo claro para las personas a quienes les resulte demasiado oscuro el tema predeterminado. En lugar de iniciar otra conversación, dirigirás la sesión existente para ampliar el trabajo.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Cada edición aparece en línea en el chat con las diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat desde el Ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver cada llamada a una herramienta. Aparecerán lecturas y ediciones de archivos y los comandos de terminal que solicita ejecutar.
3. Cuando el agente proponga editar un archivo, aparecerán las diferencias en línea:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertir el cambio y permitir que el agente vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed** en la parte superior del chat para ver todos los archivos modificados por el agente durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta solicita permiso (por ejemplo, para ejecutar un comando de terminal), el agente se detendrá y mostrará una solicitud **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que el agente termine de implementar el modo de alto contraste. Deberías ver un mensaje final que resuma los cambios.

## Dirige al agente para añadir el modo claro

Una vez implementado el modo de alto contraste, ampliarás la misma conversación para añadir un conmutador de modo claro. Como continuarás en la misma sesión de chat, el agente conservará el contexto del trabajo anterior, incluidos los componentes modificados, el enfoque de estilo y el patrón de almacenamiento local.

1. En la entrada de Copilot Chat, envía este prompt de seguimiento:

   ```plaintext
   ¡Buen trabajo! Ahora añade un conmutador de modo claro junto al de alto contraste. El modo claro debe seguir el mismo patrón: conservarse mediante el almacenamiento local y estar disponible en la misma zona de la interfaz. El usuario debe poder activar el alto contraste y el modo claro de forma independiente.
   ```

2. El agente continuará desde el punto en que se quedó, explorará los cambios anteriores y propondrá modificaciones para el modo claro.
3. Revisa cada cambio nuevo a medida que se aplique, como hiciste con el modo de alto contraste. Usa **Keep** o **Undo** para cada diferencia.
4. Si el agente sigue un enfoque que no quieres —por ejemplo, si intenta reorganizar la interfaz de los conmutadores—, detenlo con el botón **Stop** junto a la entrada del chat y envía un mensaje de seguimiento para aclarar lo que necesitas.

> [!TIP]
> Dirigir una sesión en curso es más rápido que empezar de nuevo. Usa prompts de seguimiento para pedir ajustes («simplifica el CSS; usa variables CSS en lugar de duplicar selectores»), corregir el rumbo («no añadas un tercer conmutador; integra el modo claro en el panel de configuración existente») o ampliar el alcance («añade también métodos abreviados de teclado para ambos conmutadores»).

## Revisa los cambios

Antes de confirmar el trabajo, revisa rápidamente todos los archivos que ha modificado el agente.

1. Abre la vista **Source Control** en VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en los componentes Astro, los estilos y las pruebas relacionadas.
3. Abre algunos archivos modificados y revisa las diferencias. Confirma que se han aplicado las prácticas de accesibilidad del agente personalizado: atributos de Aplicaciones de Internet Enriquecidas Accesibles (ARIA), navegación con teclado, HTML semántico y persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel Source Control. Los publicarás en [el siguiente ejercicio][next-lesson].

## Resumen y siguientes pasos

Has usado el modo de agente de Copilot Chat para supervisar y dirigir una sesión en curso: has revisado cada edición, aceptado o rechazado cambios y enviado prompts de seguimiento para ampliar el trabajo sin perder contexto.

En este ejercicio:

- has supervisado el trabajo de un agente en tiempo real.
- has aceptado y rechazado ediciones de archivos concretas.
- has dirigido una sesión en curso mediante prompts de seguimiento.

En [el siguiente ejercicio][next-lesson] publicarás el trabajo de accesibilidad en una solicitud de incorporación de cambios y revisarás los cambios del agente personalizado local que has usado durante el taller.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Usar el modo de agente][agent-mode]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
