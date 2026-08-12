---
title: "git submodule"
source: "https://git-scm.com/docs/git-submodule"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git submodule`

Este caso usa `git submodule` para administrar repositorios incluidos dentro de otro repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git submodule anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en administrar repositorios incluidos dentro de otro repositorio.

Puede persistir el estado implicado por esta operación: administrar repositorios incluidos dentro de otro repositorio. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git submodule add https://example.com/equipo/tema.git temas/base
git submodule update --init --recursive
```

La invocación `git submodule add https://example.com/equipo/tema.git temas/base` ejecuta esta operación: administrar repositorios incluidos dentro de otro repositorio. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git submodule [--quiet] [--cached]
git submodule [--quiet] add [<options>] [--] <repository> [<path>]
git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…]
git submodule [--quiet] init [--] [<path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git submodule [--quiet] [--cached]
   or: git submodule [--quiet] add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--] <repository> [<path>]
   or: git submodule [--quiet] status [--cached] [--recursive] [--] [<path>...]
   or: git submodule [--quiet] init [--] [<path>...]
   or: git submodule [--quiet] deinit [-f|--force] (--all| [--] <path>...)
   or: git submodule [--quiet] update [--init [--filter=<filter-spec>]] [--remote] [-N|--no-fetch] [-f|--force] [--checkout|--merge|--rebase] [--[no-]recommend-shallow] [--reference <repository>] [--recursive] [--[no-]single-branch] [--] [<path>...]
   or: git submodule [--quiet] set-branch (--default|--branch <branch>) [--] <path>
   or: git submodule [--quiet] set-url [--] <path> <newurl>
   or: git submodule [--quiet] summary [--cached|--files] [--summary-limit <n>] [commit] [--] [<path>...]
   or: git submodule [--quiet] foreach [--recursive] <command>
   or: git submodule [--quiet] sync [--recursive] [--] [<path>...]
   or: git submodule [--quiet] absorbgitdirs [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git submodule -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

administrar repositorios incluidos dentro de otro repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git submodule a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git submodule con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git submodule --quiet add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

En `git submodule`, índice modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --cached add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

En `git submodule`, recursión modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --recursive add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b`

Activa b durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, b modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule -b add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, f modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule -f add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque administrar repositorios incluidos dentro de otro repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git submodule --force add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name`

Activa nombre durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, nombre modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --name add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reference`

Activa reference durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, reference modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --reference add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --all add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--init`

Activa init durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, init modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --init add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --filter add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remote`

Activa remote durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, remote modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --remote add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-N`

Activa N durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, N modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule -N add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fetch`

Desactiva el comportamiento `fetch` para esta invocación.

En `git submodule`, desactivar fetch modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --no-fetch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--checkout`

Activa checkout durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git submodule --checkout add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merge`

Activa merge durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, merge modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --merge add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rebase`

Activa rebase durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, rebase modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --rebase add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recommend-shallow`

Activa recommend historial shallow durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --recommend-shallow add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --single-branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--default`

Activa default durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git submodule`, default modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --default add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--files`

Activa files durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git submodule` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git submodule --files add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary-limit`

Establece un límite numérico para la selección o el recorrido.

En `git submodule`, summary limit modifica la forma en que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git submodule --summary-limit add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recommend-shallow`

Desactiva para esta invocación el comportamiento que habilita `--recommend-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --no-recommend-shallow add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-single-branch`

Desactiva para esta invocación el comportamiento que habilita `--single-branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta administrar repositorios incluidos dentro de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git submodule --no-single-branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git submodule` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: administrar repositorios incluidos dentro de otro repositorio. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-submodule - Initialize, update or inspect submodules](https://git-scm.com/docs/git-submodule)
