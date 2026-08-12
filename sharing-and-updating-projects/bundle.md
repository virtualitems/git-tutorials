---
title: "git bundle"
source: "https://git-scm.com/docs/git-bundle"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git bundle`

Este caso usa `git bundle` para transportar objetos y referencias dentro de un solo archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git bundle anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en transportar objetos y referencias dentro de un solo archivo.

Puede persistir el estado implicado por esta operación: transportar objetos y referencias dentro de un solo archivo. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git bundle create entrega.bundle main
git bundle verify entrega.bundle
git clone entrega.bundle copia
```

La invocación `git bundle create entrega.bundle main` ejecuta esta operación: transportar objetos y referencias dentro de un solo archivo. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git bundle create [-q | --quiet | --progress]
		    [--version=<version>] <file> <git-rev-list-args>
git bundle verify [-q | --quiet] <file>
git bundle list-heads <file> [<refname>…]
```

### Uso verificado con `git version 2.51.1`

```text
git bundle create [-q | --quiet | --progress]
                         [--version=<version>] <file> <git-rev-list-args>
   or: git bundle verify [-q | --quiet] <file>
   or: git bundle list-heads <file> [<refname>...]
   or: git bundle unbundle [--progress] <file> [<refname>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bundle -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

transportar objetos y referencias dentro de un solo archivo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git bundle a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git bundle con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q`

Activa q durante transportar objetos y referencias dentro de un solo archivo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git bundle`, q modifica la forma en que se ejecuta transportar objetos y referencias dentro de un solo archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bundle -q create entrega.bundle main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bundle` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git bundle --quiet create entrega.bundle main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bundle` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

En `git bundle`, progreso modifica la forma en que se ejecuta transportar objetos y referencias dentro de un solo archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bundle --progress create entrega.bundle main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bundle` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--version`

Muestra la versión y termina.

En `git bundle`, versión modifica la forma en que se ejecuta transportar objetos y referencias dentro de un solo archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bundle --version
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bundle` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: transportar objetos y referencias dentro de un solo archivo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)

## Fuente

- [git-bundle - Move objects and refs by archive](https://git-scm.com/docs/git-bundle)
