---
title: "Ejercicio 1 - Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Requisitos previos][previous-lesson] · [Siguiente ejercicio: Agente de GitHub Copilot en la nube →][next-lesson]

El contexto es fundamental cuando se trabaja con inteligencia artificial generativa. Si una tarea debe realizarse de una forma concreta, o hay información de fondo que Copilot debe conocer, asegúrate de que tenga acceso a ella. Los [archivos de instrucciones][instruction-files] proporcionan esa orientación para que Copilot entienda no solo *qué* quieres que haga, sino también *cómo*.

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto del proyecto, las directrices de programación y los estándares de documentación mediante las instrucciones personalizadas del repositorio y las instrucciones específicas de rutas.
- añadirás un nuevo estándar para todo el repositorio a `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los entornos de VS Code y CLI, aquí no ejecutarás un prompt para comparar el resultado antes y después. El agente de Copilot en la nube trabaja de forma asíncrona en incidencias de GitHub, por lo que es más difícil demostrar el efecto en tiempo real. Verás la influencia del archivo de instrucciones más adelante, al revisar las solicitudes de incorporación de cambios del agente.

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

- `.github/copilot-instructions.md`, un archivo único que se envía a Copilot para **todas** las solicitudes del repositorio. Debe contener información del proyecto pertinente para la mayoría de las solicitudes de chat o CLI, como la pila tecnológica, una descripción general de lo que se está desarrollando, las prácticas recomendadas y otras directrices generales.
- Los archivos `.github/instructions/*.instructions.md`, que se crean para tareas o tipos de archivo concretos. Permiten establecer directrices para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz o un conjunto de pruebas unitarias.

> [!NOTE]
> En un IDE, los archivos de instrucciones solo se usan para generar código con Copilot Chat, no para completar código ni para las sugerencias del siguiente cambio.
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

## Añade un estándar para todo el repositorio

Ahora añadirás una regla general para que la documentación se incluya en el código mediante comentarios TSDoc y un encabezado de comentario a nivel de archivo. El agente en la nube la aplicará a las incidencias que le asignes más adelante.

Antes de editar, crea una rama. El agente en la nube leerá las instrucciones de la rama de destino de la incidencia, pero confirmar los cambios en una rama propia mantiene ordenado el trabajo.

1. Desde el terminal del codespace, crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como se ha explicado, `.github/copilot-instructions.md` proporciona información del proyecto a Copilot. Añade el estándar para mejorar las sugerencias de código.

2. Vuelve a abrir `.github/copilot-instructions.md`.
3. Localiza la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Observa que describe los estándares de programación del proyecto, pero aún no incluye una regla para la documentación en el código.
4. Debajo de los estándares existentes, añade estas líneas Markdown para indicar a Copilot que incluya encabezados de comentario en los archivos y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. Guarda `copilot-instructions.md`.

> [!TIP]
> Como viste en el ejercicio anterior, los archivos de instrucciones pueden estar en el nivel del repositorio (`.github/copilot-instructions.md`) para proporcionar directrices generales o en archivos `*.instructions.md` para lenguajes, tipos de archivo y tareas concretos. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla de comentarios de documentación que acabas de añadir.

## Confirma, publica y combina la actualización de instrucciones

El agente en la nube lee los archivos de instrucciones de la rama a la que se dirige la incidencia. En el siguiente ejercicio, Copilot partirá de `main` cuando le asignes una incidencia, así que los cambios en las instrucciones deben llegar a `main` para que el agente pueda usarlos.

1. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Publica la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una solicitud de incorporación de cambios de `custom-instructions-cloud` a `main` y combínala. El agente en la nube leerá las instrucciones cuando trabaje en las incidencias que le asignes en el siguiente ejercicio.

> [!TIP]
> Si prefieres trabajar directamente en `main` durante este taller, puedes omitir la rama y confirmar los cambios directamente en `main`. El paso de la rama refleja el flujo que seguirías en un proyecto real.

## Resumen y siguientes pasos

Has explorado cómo Copilot obtiene el contexto de los archivos de instrucciones del proyecto y has añadido un estándar general a `.github/copilot-instructions.md`. Verás cómo se aplica en las solicitudes de incorporación de cambios que genere el agente en la nube durante el resto de este entorno.

A continuación, [asignarás tu primera incidencia al agente de GitHub Copilot en la nube][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
