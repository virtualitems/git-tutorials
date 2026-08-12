---
title: "git get-tar-commit-id"
source: "https://git-scm.com/docs/git-get-tar-commit-id"
section: "plumbing-read"
status: "option-expanded"
---

# `git get-tar-commit-id`

Este caso usa `git get-tar-commit-id` para extraer el identificador incluido por git archive en un tar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git get-tar-commit-id consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en extraer el identificador incluido por git archive en un tar.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git archive HEAD | git get-tar-commit-id
```

La invocación `git get-tar-commit-id` ejecuta esta operación: extraer el identificador incluido por git archive en un tar. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git get-tar-commit-id
```

### Uso verificado con `git version 2.51.1`

```text
git get-tar-commit-id
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git get-tar-commit-id -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

extraer el identificador incluido por git archive en un tar. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git get-tar-commit-id a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git get-tar-commit-id con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-h`

Activa h durante extraer el identificador incluido por git archive en un tar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git get-tar-commit-id`, h modifica la forma en que se ejecuta extraer el identificador incluido por git archive en un tar. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git get-tar-commit-id -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git get-tar-commit-id` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git ls-files`](../plumbing-read/ls-files.md)
- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)

## Fuente

- [git-get-tar-commit-id - Extract commit ID from an archive created using git-archive](https://git-scm.com/docs/git-get-tar-commit-id)
