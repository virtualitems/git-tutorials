---
title: "gitcli"
source: "https://git-scm.com/docs/gitcli"
section: "guides"
status: "option-expanded"
---

# `gitcli`

Este caso usa `gitcli` para interpretar opciones, revisiones y rutas en la línea de comandos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **orden de opciones**, **opciones globales**, **separador `--`**, **revisiones y pathspecs**, **citas y expansión del shell**.

## Responsabilidad y efecto

gitcli define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en interpretar opciones, revisiones y rutas en la línea de comandos.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Convenciones de la CLI

Una invocación comienza con `git`, continúa con opciones globales, nombra una orden y termina con los argumentos de esa orden. `git -C ruta status` cambia el directorio antes de ejecutar `status`. `git -c clave=valor orden` aplica una configuración solo durante esa invocación. Las opciones de la orden se colocan después de su nombre.

```bash
git -C ../proyecto -c color.ui=false status --short
```

El shell procesa comillas, variables y globos antes de que Git reciba los argumentos. Usa comillas cuando Git deba interpretar el patrón. Usa una lista terminada en NUL cuando un nombre pueda contener espacios o saltos de línea.

## Pathspecs

Un pathspec selecciona rutas. `docs/` limita la operación a ese directorio. `'*.md'` permite que Git aplique el patrón en el alcance de la orden. El separador `--` termina las opciones y evita que una ruta iniciada por guion se interprete como una opción.

```bash
printf 'dato\n' > ./-entrada.txt
git add -- ./-entrada.txt
git status --short
```

La ruta pertenece al índice después de `git add`. Sin `--`, el analizador podría tratar `-entrada.txt` como una opción.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git log main..tema -- docs/
git restore --source=HEAD -- README.md
```

La invocación `gitcli` ejecuta esta operación: interpretar opciones, revisiones y rutas en la línea de comandos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git log main..tema -- docs/
git restore --source=HEAD -- README.md
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

interpretar opciones, revisiones y rutas en la línea de comandos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### orden de opciones

Aplicar las reglas de orden de opciones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### opciones globales

Aplicar las reglas de opciones globales. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### separador `--`

Aplicar las reglas de separador `--`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### revisiones y pathspecs

Aplicar las reglas de revisiones y pathspecs. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### citas y expansión del shell

Aplicar las reglas de citas y expansión del shell. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Opciones globales

Las opciones globales se colocan después de `git` y antes de la orden.

```bash
git -C ruta status
```

Compara `git -C ruta status` con la ejecución dentro de la ruta. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Fin de opciones

`--` impide que una ruta iniciada por guion se trate como opción.

Crea una ruta `-dato` y consúltala con `-- -dato`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Expansión del shell

Un glob sin comillas lo expande el shell; entre comillas puede llegar a Git como pathspec.

Compara `*.md` con `"*.md"` en dos directorios. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Revisiones

Una posición que espera revisión acepta nombres de referencia y expresiones de alcance.

```bash
git rev-parse --verify
```

Resuelve el argumento con `git rev-parse --verify`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pathspecs

Un pathspec selecciona rutas y admite firmas mágicas cuando la orden las soporta.

```bash
git ls-files -- archivo.txt
```

Usa `git ls-files -- <pathspec>` para observar la selección. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--source`

Activa source durante interpretar opciones, revisiones y rutas en la línea de comandos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `gitcli`, source modifica la forma en que se ejecuta interpretar opciones, revisiones y rutas en la línea de comandos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git restore --source=HEAD -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La regla no se aplica

Comprueba esta causa: El patrón, alcance o precedencia no coincide. Consulta la regla efectiva y el archivo que la definió.

### Una revisión se interpreta como ruta

Comprueba esta causa: El nombre es ambiguo. Separa revisiones y rutas con `--`.

### El resultado cambia entre equipos

Comprueba esta causa: La regla vive en configuración no compartida. Decide qué parte debe versionarse en el repositorio.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`githooks`](../guides/githooks.md)
- [`gitattributes`](../guides/gitattributes.md)
- [`gitignore`](../guides/gitignore.md)

## Fuente

- [gitcli - Git command-line interface and conventions](https://git-scm.com/docs/gitcli)
