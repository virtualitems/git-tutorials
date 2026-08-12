---
title: "git merge-base"
source: "https://git-scm.com/docs/git-merge-base"
section: "plumbing-read"
status: "option-expanded"
---

# `git merge-base`

Este caso usa `git merge-base` para calcular ancestros comunes para una fusión. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git merge-base consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en calcular ancestros comunes para una fusión.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
base=$(git merge-base main tema-portada)
git show --oneline --no-patch "$base"
```

La invocación `git merge-base` ejecuta esta operación: calcular ancestros comunes para una fusión. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git merge-base [-a | --all] <commit> <commit>…
git merge-base [-a | --all] --octopus <commit>…
git merge-base --is-ancestor <commit> <commit>
git merge-base --independent <commit>…
```

### Uso verificado con `git version 2.51.1`

```text
git merge-base [-a | --all] <commit> <commit>...
   or: git merge-base [-a | --all] --octopus <commit>...
   or: git merge-base --is-ancestor <commit> <commit>
   or: git merge-base --independent <commit>...
   or: git merge-base --fork-point <ref> [<commit>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-base -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

calcular ancestros comunes para una fusión. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git merge-base a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git merge-base con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.  La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-a`

```bash
git merge-base -a
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--all`

```bash
git merge-base --all
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--octopus`

Activa octopus durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find ancestors for a single n-way merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-base`, octopus modifica la forma en que se ejecuta calcular ancestros comunes para una fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-base --octopus
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--is-ancestor`

Activa is ancestor durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `is the first one ancestor of the other?`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-base`, is ancestor modifica la forma en que se ejecuta calcular ancestros comunes para una fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-base --is-ancestor
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--independent`

Incluye independent en la salida o cambia cómo `git merge-base` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `list revs not reachable from others`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-base`, independent modifica la forma en que se ejecuta calcular ancestros comunes para una fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-base --independent
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fork-point`

Activa fork point durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find where <commit> forked from reflog of <ref>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-base`, fork point modifica la forma en que se ejecuta calcular ancestros comunes para una fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-base --fork-point
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge-base --no-all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-base` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El objeto no existe

Comprueba esta causa: El identificador no resuelve o no está disponible en un clon parcial. Valida el hash y la política de descarga.

### La salida se separa mal

Comprueba esta causa: Un nombre contiene espacios o saltos de línea. Usa terminación NUL cuando la función la admita.

### El recorrido incluye más commits

Comprueba esta causa: El rango expresa alcanzabilidad y no una lista literal. Comprueba extremos positivos y negativos del rango.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git name-rev`](../plumbing-read/name-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)
- [`git pack-redundant`](../plumbing-read/pack-redundant.md)

## Fuente

- [git-merge-base - Find as good common ancestors as possible for a merge](https://git-scm.com/docs/git-merge-base)
