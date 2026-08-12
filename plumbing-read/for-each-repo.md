---
title: "git for-each-repo"
source: "https://git-scm.com/docs/git-for-each-repo"
section: "plumbing-read"
status: "option-expanded"
---

# `git for-each-repo`

Este caso usa `git for-each-repo` para ejecutar un comando Git en repositorios enumerados por configuración. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git for-each-repo consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en ejecutar un comando Git en repositorios enumerados por configuración.

La orden iterada decide qué cambia en cada repositorio; el contenedor no limita ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git config --global --add repos.proyectos ~/codigo/biblioteca
git for-each-repo --config=repos.proyectos status --short
```

La invocación `git for-each-repo --config=repos.proyectos status --short` ejecuta esta operación: ejecutar un comando Git en repositorios enumerados por configuración. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git for-each-repo --config=<config> [--] <arguments>
```

### Uso verificado con `git version 2.51.1`

```text
git for-each-repo --config=<config> [--] <arguments>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git for-each-repo -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

ejecutar un comando Git en repositorios enumerados por configuración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git for-each-repo a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git for-each-repo con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--config`

Incluye config en la salida o cambia cómo `git for-each-repo` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `config key storing a list of repository paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git for-each-repo`, config modifica la forma en que se ejecuta ejecutar un comando Git en repositorios enumerados por configuración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-repo --config=valor status --short
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-going`

Activa conservar going durante ejecutar un comando Git en repositorios enumerados por configuración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep going even if command fails in a repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git for-each-repo`, conservar going modifica la forma en que se ejecuta ejecutar un comando Git en repositorios enumerados por configuración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-repo --keep-going --config=repos.proyectos status --short
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-repo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-config`

Desactiva para esta invocación el comportamiento que habilita `--config`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-repo`, desactivar config modifica la forma en que se ejecuta ejecutar un comando Git en repositorios enumerados por configuración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-repo --no-config status --short
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-repo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-going`

Desactiva para esta invocación el comportamiento que habilita `--keep-going`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-repo`, desactivar conservar going modifica la forma en que se ejecuta ejecutar un comando Git en repositorios enumerados por configuración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-repo --no-keep-going --config=repos.proyectos status --short
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-repo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El objeto no existe

Comprueba esta causa: El identificador no resuelve o no está disponible en un clon parcial. Valida el hash y la política de descarga.

### La salida se separa mal

Comprueba esta causa: Un nombre contiene espacios o saltos de línea. Usa terminación NUL cuando la función la admita.

### El recorrido incluye más commits

Comprueba esta causa: El rango expresa alcanzabilidad y no una lista literal. Comprueba extremos positivos y negativos del rango.

## Automatización y recuperación

Persistencia: La orden iterada decide qué cambia en cada repositorio; el contenedor no limita ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)
- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)

## Fuente

- [git-for-each-repo - Run a Git command on a list of repositories](https://git-scm.com/docs/git-for-each-repo)
