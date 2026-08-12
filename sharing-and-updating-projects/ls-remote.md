---
title: "git ls-remote"
source: "https://git-scm.com/docs/git-ls-remote"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git ls-remote`

Este caso usa `git ls-remote` para enumerar referencias anunciadas por un repositorio remoto. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git ls-remote anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en enumerar referencias anunciadas por un repositorio remoto.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git ls-remote --heads origin
```

La invocación `git ls-remote --heads origin` ejecuta esta operación: enumerar referencias anunciadas por un repositorio remoto. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git ls-remote [--branches] [--tags] [--refs] [--upload-pack=<exec>]
	      [-q | --quiet] [--exit-code] [--get-url] [--sort=<key>]
	      [--symref] [<repository> [<patterns>…]]
```

### Uso verificado con `git version 2.51.1`

```text
git ls-remote [--branches] [--tags] [--refs] [--upload-pack=<exec>]
                     [-q | --quiet] [--exit-code] [--get-url] [--sort=<key>]
                     [--symref] [<repository> [<patterns>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git ls-remote -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

enumerar referencias anunciadas por un repositorio remoto. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git ls-remote a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git ls-remote con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--branches` y `-b`

Incluye o selecciona ramas según la operación.  La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `--branches`

```bash
git ls-remote --branches --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `-b`

```bash
git ls-remote -b --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--tags` y `-t`

Incluye o selecciona etiquetas según la operación.  La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `--tags`

```bash
git ls-remote --tags --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `-t`

```bash
git ls-remote -t --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--refs`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git ls-remote --refs --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Activa upload pack durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `path of git-upload-pack on the remote host`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git ls-remote`, upload pack modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --upload-pack=valor --heads origin
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git ls-remote -q --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--quiet`

```bash
git ls-remote --quiet --heads origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--exit-code`

Activa exit code durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exit with exit code 2 if no matching refs are found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git ls-remote`, exit code modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --exit-code --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--get-url`

Activa get url durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `take url.<base>.insteadOf into account`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git ls-remote`, get url modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --get-url --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

En `git ls-remote`, ordenar modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --sort=user.name --heads origin
git branch -vv
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--symref`

Incluye symref en la salida o cambia cómo `git ls-remote` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show underlying ref in addition to the object pointed by it`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git ls-remote --symref --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante enumerar referencias anunciadas por un repositorio remoto. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git ls-remote`, server option modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-o`

```bash
git ls-remote -o valor --heads origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--server-option`

```bash
git ls-remote --server-option=valor --heads origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-branches`

Desactiva para esta invocación el comportamiento que habilita `--branches`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git ls-remote --no-branches --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git ls-remote --no-tags --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-refs`

Desactiva para esta invocación el comportamiento que habilita `--refs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git ls-remote --no-refs --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-upload-pack`

Desactiva para esta invocación el comportamiento que habilita `--upload-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git ls-remote`, desactivar upload pack modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --no-upload-pack --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git ls-remote --no-quiet --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exit-code`

Desactiva para esta invocación el comportamiento que habilita `--exit-code`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git ls-remote`, desactivar exit code modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --no-exit-code --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-get-url`

Desactiva para esta invocación el comportamiento que habilita `--get-url`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git ls-remote`, desactivar get url modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --no-get-url --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sort`

Desactiva para esta invocación el comportamiento que habilita `--sort`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git ls-remote`, desactivar ordenar modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --no-sort --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-symref`

Desactiva para esta invocación el comportamiento que habilita `--symref`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git ls-remote --no-symref --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-server-option`

Desactiva para esta invocación el comportamiento que habilita `--server-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git ls-remote`, desactivar server option modifica la forma en que se ejecuta enumerar referencias anunciadas por un repositorio remoto. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git ls-remote --no-server-option --heads origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git ls-remote` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-ls-remote - List references in a remote repository](https://git-scm.com/docs/git-ls-remote)
