---
title: "Lección 8 - Crear y combinar la PR de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la actualización de la habilidad, el perfil QA y las pruebas; después, crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación del filtrado, las actualizaciones de instrucciones y de la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una sola rama. Es hora de revisarlos juntos y abrir una solicitud de incorporación de cambios. Ya has combinado personalmente la solicitud de incorporación de cambios (PR) de valoraciones por estrellas; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente separaríamos la funcionalidad, las actualizaciones de instrucciones y de la habilidad y el agente QA en varias PR. Para agilizar el taller, has mantenido todo el flujo de filtrado y calidad en una sesión y una rama, y todo ese trabajo se incluirá en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- examinarás la PR completa de la funcionalidad y las pruebas de verificación.
- autorizarás Agent Merge solo después de la revisión y confirmarás que la PR está combinada.

## Escenario

A lo largo del flujo de filtrado, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR y mantener la autorización para combinar bajo el control del desarrollador.

## Introducción a Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de cambios en la aplicación GitHub Copilot. Al habilitarlo, la sesión de la aplicación lee la solicitud, resuelve los bloqueos —corrige comprobaciones de integración continua (CI) fallidas, responde a comentarios de revisión y reorganiza la rama cuando es necesario— y la combina en cuanto GitHub lo permite. Se ejecuta en segundo plano, continúa tras reiniciar la aplicación y se desactiva cuando se combina la solicitud.

Hasta ahora has seleccionado **Merge pull request** personalmente. Agent Merge puede asumir esa responsabilidad, pero su capacidad de editar código y combinar sigue necesitando tu autorización explícita. Revisa sus acciones permitidas y el trabajo antes de conceder permiso para combinar.

## Usa Agent Merge para gestionar la PR

Con todo el código creado y revisado, deja que Agent Merge gestione el proceso de la solicitud.

1. Usa el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El botón cambiará a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Elegir la opción del menú desplegable por sí sola no lo inicia.

Agent Merge empezará a trabajar. Hará lo siguiente:

- Crear la solicitud de incorporación de cambios con un título y una descripción.
- Si has iniciado la sesión desde una incidencia, incluir una referencia a ella en el cuerpo de la descripción.
- Reorganizar la rama o gestionar posibles conflictos de combinación con la rama de destino.
- Supervisar el proceso de integración continua para comprobar que se superan todas las comprobaciones.
- Supervisar la solicitud para detectar comentarios de otros desarrolladores o de la revisión de código de Copilot, y realizar cambios para resolverlos.
- Combinar automáticamente la solicitud, si se lo autorizas, cuando todo se haya completado correctamente.

Ahora autorizarás a Agent Merge a combinar la solicitud cuando se hayan superado todas las comprobaciones.

5. Revisa las diferencias de la solicitud y las pruebas de verificación antes de conceder permiso para combinar.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que **Merge pull request** está marcado.
8. Pide explícitamente al agente que combine la solicitud:

   ```plaintext
   Combina la solicitud cuando se hayan superado todas las comprobaciones y aprobaciones obligatorias. No omitas las protecciones del repositorio.
   ```

9. Sigue el progreso y resuelve los bloqueos indicados. Antes de continuar, confirma que el estado de la solicitud es **Merged**. Tener habilitado el permiso de combinación o un agente en ejecución no confirma que la combinación se haya completado.

> [!IMPORTANT]
> Agent Merge no elude las protecciones del repositorio ni los permisos ausentes. Resuelve esos bloqueos antes de continuar.

## Resumen y pasos siguientes

Has automatizado varias partes del proceso de desarrollo, como la generación, las pruebas y la validación de código, y ahora también el proceso de solicitud de incorporación de cambios. En concreto:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- has examinado la PR completa de la funcionalidad y las pruebas de verificación.
- has autorizado Agent Merge solo después de la revisión y has confirmado que la PR estaba combinada.

A continuación, [utilizarás un lienzo existente y crearás uno de clasificación][next-lesson] para explorar una forma más completa de examinar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Gestionar incidencias y solicitudes de incorporación de cambios con la aplicación GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app