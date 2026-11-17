---
title: "Ejercicio 1 - Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Requisitos previos][previous-lesson] · [Siguiente ejercicio: Modo de agente →][next-lesson]

El contexto es fundamental cuando se trabaja con inteligencia artificial generativa. Si una tarea debe realizarse de una forma concreta o hay información de fondo que Copilot debe conocer, asegúrate de que tenga acceso a ella. Hay varias formas de compartir contexto específico con Copilot. Una de las principales son los [archivos de instrucciones][instruction-files], que proporcionan directrices para generar código.

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto del proyecto, las directrices de programación y los estándares de documentación mediante las instrucciones personalizadas del repositorio y las instrucciones específicas de rutas.
- generarás la primera parte de la capa de datos para el filtrado (un helper de editores) con las instrucciones actuales.
- añadirás un nuevo estándar para todo el repositorio a `.github/copilot-instructions.md`.
- volverás a enviar el mismo prompt y observarás cómo el código generado incorpora el nuevo estándar.
- confirmarás los cambios de las instrucciones y el filtrado en `main` para que Copilot pueda utilizar las nuevas directrices en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede no seguir todos los estándares establecidos. Copilot no es determinista. El objetivo del ejercicio es observar la tendencia del cambio después de actualizar las instrucciones, no obtener exactamente el mismo resultado carácter por carácter.

## Archivos de instrucciones

### Escenario

Como cualquier empresa de desarrollo, Tailspin Toys tiene directrices y requisitos para sus prácticas de desarrollo:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario debe usar un tema oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Al principio de cada archivo debe haber un bloque de comentarios que describa su propósito.

Los archivos de instrucciones permiten proporcionar a Copilot la información necesaria para que realice las tareas de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que entienda mejor el estilo de programación y los requisitos. Permiten orientar sus sugerencias y fragmentos de código con las convenciones, las bibliotecas y los comentarios que prefieras. Puedes crear instrucciones para todo el repositorio o para tipos concretos de archivos y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un archivo único que se envía a Copilot para **todas** las solicitudes del repositorio. Debe contener información del proyecto pertinente para la mayoría de las solicitudes, como la pila tecnológica, una descripción general de lo que se desarrolla, las prácticas recomendadas y otras directrices generales.
- Los archivos `.github/instructions/*.instructions.md`, que se crean para tareas o tipos de archivo concretos. Permiten establecer directrices para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz o un conjunto de pruebas unitarias.

> [!NOTE]
> En un entorno de desarrollo integrado (IDE), los archivos de instrucciones solo se usan para generar código con Copilot Chat, no para completar código ni para las sugerencias del siguiente cambio.
>
> Copilot Chat, Copilot CLI y el agente de Copilot en la nube usan los archivos de instrucciones del repositorio y los archivos `*.instructions.md` con frontmatter `applyTo` para generar código.
>
> Copilot también [admite archivos de instrucciones en otros formatos][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

Los ejemplos del proyecto muestran un enfoque representativo para crear archivos de instrucciones:

- Mantén `copilot-instructions.md` centrado en directrices del proyecto, como una descripción de lo que se desarrolla, la estructura del proyecto y los estándares generales de programación.
- Usa archivos `*.instructions.md` para proporcionar directrices específicas de tipos de archivo (pruebas unitarias, componentes Astro o la capa de datos) o tareas concretas.
- Escribe en lenguaje natural. Las directrices deben ser claras e incluir ejemplos del aspecto que debe y no debe tener el código.

No hay una única manera correcta de crear archivos de instrucciones ni de usar la IA. La experimentación te ayudará a averiguar qué funciona mejor en tu proyecto.

> [!TIP]
> Todo proyecto que use GitHub Copilot debería tener una colección sólida de archivos de instrucciones. Al explorar los archivos de este proyecto, verás instrucciones para varias tareas, como las [actualizaciones de la interfaz de usuario][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada superficie ofrece una opción distinta, como **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI. El ejercicio de cada superficie lo indicará cuando sea pertinente.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas del proyecto

Dedica un momento a leer los archivos de instrucciones incluidos en este repositorio: hay un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para tareas diferentes. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Explora el archivo y fíjate en la breve descripción del proyecto y en secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, observa también las directrices anidadas de **GitHub Actions Workflows**. Se aplican a cualquier interacción con Copilot.
3. Abre la carpeta `.github/instructions` y explora su contenido. Hay instrucciones para archivos Astro, la capa de datos de Drizzle, pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. Fíjate en el campo `applyTo` de la parte superior, que establece un patrón glob relativo a la raíz del repositorio. En este caso, coincide con cualquier archivo de prueba TypeScript, como los que siguen el patrón `**/*.test.ts`.
5. Observa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Así puedes dividir conjuntos de instrucciones grandes en otros más pequeños y reutilizables, y enlazar ejemplos. Las rutas son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero aún no exige documentación dentro del código. En los pasos siguientes añadirás reglas para los comentarios TSDoc y los encabezados de comentarios de los archivos.

## Crea una rama para los cambios

Crea una rama para los cambios siguiendo las prácticas recomendadas.

1. Vuelve al codespace del ejercicio anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama nueva y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Usa Copilot Chat antes de actualizar las instrucciones

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso indica cuál debes usar.

Para observar el efecto de las instrucciones personalizadas, empieza enviando un prompt con el archivo de instrucciones actual. Más adelante, lo actualizarás y volverás a enviar el mismo prompt para comparar el resultado.

1. Cierra las pestañas abiertas del editor de ejercicios anteriores para que Copilot solo reciba el contexto que necesitas.
2. Abre `src/lib/publishers.ts` para indicar a Copilot dónde debe ubicarse el helper.
3. En el selector de agentes de la vista Chat, selecciona **Agent** para que Copilot pueda modificar archivos.

   ![Captura de pantalla del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este prompt:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un helper de acceso a datos que devuelva una lista de todos los editores, con su nombre e id. Aplica los cambios a los archivos.
   ```

5. Copilot explora el proyecto y aplica cambios, a menudo tanto al archivo del helper como a sus pruebas.
6. Observa que el helper propuesto es una función con tipos que recibe un cliente `db` como primer argumento y devuelve una matriz con tipos de editores. Esto se debe a las convenciones de la capa de datos de `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
7. Observa que el código propuesto **no incluye** comentarios TSDoc ni un encabezado de comentario a nivel de archivo.

> [!CAUTION]
> Como Copilot no es determinista, puede que añada comentarios de documentación aunque no se lo pidas. No pasa nada: el objetivo es observar la mejora de coherencia después de actualizar las instrucciones.

## Añade un estándar para todo el repositorio

Como se ha explicado, `.github/copilot-instructions.md` proporciona información del proyecto a Copilot. Añade el estándar para mejorar las sugerencias de código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Localiza la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Observa que describe los estándares de programación del proyecto, pero aún no incluye una regla para la documentación en el código.
3. Debajo de los estándares existentes, añade estas líneas Markdown para indicar a Copilot que incluya encabezados de comentario en los archivos y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como viste en el ejercicio anterior, los archivos de instrucciones pueden estar en el nivel del repositorio (`.github/copilot-instructions.md`) para proporcionar directrices generales o en archivos `*.instructions.md` para lenguajes, tipos de archivo y tareas concretos. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla de comentarios de documentación que acabas de añadir.

## Vuelve a enviar el prompt y observa el cambio

1. Vuelve a Copilot Chat y selecciona **New Chat** para borrar el contexto de la conversación.
2. Vuelve a seleccionar `src/lib/publishers.ts` para que Copilot se centre en el archivo correcto.
3. Envía el **mismo prompt** de antes:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un helper de acceso a datos que devuelva una lista de todos los editores, con su nombre e id. Aplica los cambios a los archivos.
   ```

4. Observa que ahora el archivo propuesto empieza con un bloque de comentarios parecido al siguiente:

   ```typescript
   /**
    * Helpers de acceso a datos de editores para la plataforma de financiación
    * colectiva de Tailspin Toys.
    * Proporciona funciones para recuperar información de editores de la base de datos.
    */
   ```

5. Observa que la función propuesta incluye ahora un comentario TSDoc parecido al siguiente:

   ```typescript
   /**
    * Devuelve una lista de todos los editores con su id y nombre.
    *
    * @param db - Cliente de base de datos Drizzle.
    * @returns Una promesa que se resuelve en una matriz de objetos de editores.
    */
   ```

Has orientado a Copilot para que siga un estándar nuevo y lo aplique al código real sobre el que se trabajará en el siguiente ejercicio.

## Confirma las instrucciones y publica la rama

Los archivos de instrucciones se gestionan con el mismo control de código fuente que cualquier otro recurso del repositorio. Confirma los cambios y publica la rama.

1. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Desde el terminal, ejecuta `git status` para confirmar que están presentes las actualizaciones de instrucciones y del helper:

   ```bash
   git status
   ```

3. Prepara y confirma la actualización de instrucciones y todos los archivos modificados por Copilot para el helper:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra otros cambios relacionados, como pruebas, añade también esos archivos.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Publica la rama en el repositorio:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Después de publicar la rama, crea una solicitud de incorporación de cambios y vincúlala a la incidencia del backlog sobre los estándares de documentación. Copilot puede buscar la incidencia, crear una solicitud que la cierre y, después, combinarla usando las herramientas de GitHub conectadas al proyecto.

> [!NOTE]
> En este ejercicio Copilot actuará por primera vez en GitHub. La plantilla del proyecto ya conecta las herramientas de GitHub al espacio de trabajo, así que no hay que configurarlas. La primera vez que Copilot use una herramienta, VS Code podría pedirte que inicies sesión en GitHub. Sigue las instrucciones para permitirlo. En un ejercicio posterior aprenderás cómo funciona esta conexión mediante Model Context Protocol (MCP).

1. Abre Copilot Chat en el codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista Copilot Chat y confirma que **Agent** está seleccionado en el selector de agentes.
3. Pide a Copilot que busque la incidencia relacionada con la actualización de los archivos de instrucciones y que cree una solicitud desde la rama actual. Indícale que describa tanto la actualización de las instrucciones como la base del helper de editores:

   ```plaintext
   Busca la incidencia relacionada con la actualización del archivo de instrucciones. Crea una solicitud de incorporación de cambios desde la rama actual, indica que cierra esa incidencia y menciona que también hemos añadido la base del helper de editores para el próximo trabajo de filtrado.
   ```

4. Copilot buscará la incidencia y creará la solicitud.
5. Si Copilot te pide **Allow** para realizar acciones de GitHub en tu nombre, revisa el comando y selecciona **Allow** si estás de acuerdo.
6. Cuando se cree la solicitud, pide a Copilot que la combine y vuelva a `main` local con este prompt:

   ```plaintext
   Combina la solicitud de incorporación de cambios en main. Después, vuelve localmente a main y ejecuta git pull para actualizar el código.
   ```

7. Si Copilot te pide **Allow** para realizar acciones de GitHub y ejecutar comandos de shell en tu nombre, revisa el comando y selecciona **Allow** si estás de acuerdo.

¡Has creado y combinado una solicitud de incorporación de cambios con GitHub Copilot!

## Resumen y siguientes pasos

Has explorado cómo Copilot obtiene el contexto de los archivos de instrucciones del proyecto y has usado Copilot Chat en VS Code para:

- enviar un prompt de generación de código y observar el resultado con las instrucciones *existentes*.
- añadir un nuevo estándar para todo el repositorio a `.github/copilot-instructions.md`.
- volver a enviar el mismo prompt y observar cómo el código propuesto aplica el estándar nuevo.
- confirmar en `main` la actualización de instrucciones y la base del helper para que el siguiente ejercicio pueda continuar el trabajo.

A continuación, aplicarás esas instrucciones en el [modo de agente][next-lesson] mientras Copilot añade una funcionalidad en varios archivos.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personalizadas personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
