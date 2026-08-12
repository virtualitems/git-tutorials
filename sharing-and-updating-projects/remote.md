---
title: "git remote"
source: "https://git-scm.com/docs/git-remote"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git remote`

Este caso usa `git remote` para crear y administrar nombres para repositorios remotos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git remote anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en crear y administrar nombres para repositorios remotos.

Puede persistir el estado implicado por esta operación: crear y administrar nombres para repositorios remotos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Remotos y refspecs

Un remoto asigna un nombre, como `origin`, a una o más URL y a reglas de descarga. La URL elige transporte y ubicación. Un refspec asigna una referencia de origen a una referencia de destino.

```bash
git remote add origin https://example.test/proyecto.git
git remote -v
git config --get-all remote.origin.fetch
```

La segunda orden muestra las URL de fetch y push. La tercera muestra el refspec de descarga. Comprueba estos valores antes de ejecutar fetch, pull o push.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git remote add origin https://example.test/equipo/biblioteca.git
git remote -v
```

La invocación `git remote add origin https://example.test/equipo/biblioteca.git` ejecuta esta operación: crear y administrar nombres para repositorios remotos. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>
git remote rename [--[no-]progress] <old> <new>
git remote remove <name>
```

### Uso verificado con `git version 2.51.1`

```text
git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename [--[no-]progress] <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git remote -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear y administrar nombres para repositorios remotos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git remote a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git remote con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git remote -v add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--verbose`

```bash
git remote --verbose add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-t`

Activa t durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, t modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -t add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, m modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -m add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, f modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -f add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta crear y administrar nombres para repositorios remotos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git remote --tags add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mirror`

Activa espejo durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, espejo modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --mirror add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

En `git remote`, progreso modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --progress add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva el comportamiento `tags` para esta invocación.

La opción limita o amplía el conjunto sobre el que se ejecuta crear y administrar nombres para repositorios remotos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git remote --no-tags add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, a modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -a add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto`

Activa auto durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, auto modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --auto add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, d modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -d add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delete`

Elimina el elemento seleccionado.

La opción controla eliminar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear y administrar nombres para repositorios remotos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git remote --delete add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, n modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -n add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git remote --dry-run add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, p modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote -p add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

La opción controla podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear y administrar nombres para repositorios remotos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git remote --prune add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add`

Permite crear o escribir el elemento seleccionado.

En `git remote`, add modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --add add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--push`

Activa push durante crear y administrar nombres para repositorios remotos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git remote`, push modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --push add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta crear y administrar nombres para repositorios remotos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git remote --all add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git remote --no-verbose add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git remote`, desactivar progreso modifica la forma en que se ejecuta crear y administrar nombres para repositorios remotos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git remote --no-progress add origin https://example.test/equipo/biblioteca.git
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear y administrar nombres para repositorios remotos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git push`](../sharing-and-updating-projects/push.md)
- [`git submodule`](../sharing-and-updating-projects/submodule.md)

## Fuente

- [git-remote - Manage set of tracked repositories](https://git-scm.com/docs/git-remote)
