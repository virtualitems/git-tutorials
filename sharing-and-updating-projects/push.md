---
title: "git push"
source: "https://git-scm.com/docs/git-push"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git push`

Este caso usa `git push` para actualizar referencias de un repositorio remoto y enviar sus objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git push anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en actualizar referencias de un repositorio remoto y enviar sus objetos.

Puede persistir el estado implicado por esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git push -u origin tema-portada
```

La invocación `git push -u origin tema-portada` ejecuta esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git push [--all | --branches | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	 [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-q | --quiet] [-v | --verbose]
	 [-u | --set-upstream] [-o <string> | --push-option=<string>]
	 [--[no-]signed | --signed=(true|false|if-asked)]
```

### Uso verificado con `git version 2.51.1`

```text
git push [<options>] [<repository> [<refspec>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git push -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

actualizar referencias de un repositorio remoto y enviar sus objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git push a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git push con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --all -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branches`

Incluye o selecciona ramas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --branches -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mirror`

Activa espejo durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mirror all refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --mirror -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --tags -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--follow-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --follow-tags -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --atomic -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

#### Ejemplo con `-n`

```bash
git push -n -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--dry-run`

```bash
git push --dry-run -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--receive-pack`

Activa receive pack durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git push`, receive pack modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --receive-pack=valor -u origin tema-portada
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--repo`

Activa repo durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git push`, repo modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --repo=valor -u origin tema-portada
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git push -f -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--force`

```bash
git push --force -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-d` y `--delete`

Elimina el elemento seleccionado.  La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla eliminar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-d`

```bash
git push -d -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--delete`

```bash
git push --delete -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

La opción controla podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --prune -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git push -q -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--quiet`

```bash
git push --quiet -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git push -v -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--verbose`

```bash
git push --verbose -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-u` y `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/status`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-u`

```bash
git push -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--set-upstream`

```bash
git push --set-upstream origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-o` y `--push-option`

Activa push option durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git push`, push option modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-o`

```bash
git push -o valor -u origin tema-portada
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--push-option`

```bash
git push --push-option=valor -u origin tema-portada
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--signed`

Activa firmado durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign the push`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git push`, firmado modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --signed=valor -u origin tema-portada
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git push --porcelain -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-with-lease`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección with lease. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --force-with-lease=main -u origin tema-portada
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-if-includes`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección if includes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --force-if-includes -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --recurse-submodules=valor -u origin tema-portada
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thin`

Define thin para esta ejecución de `git push`. En Git 2.51.1, la ayuda corta expresa el contrato como `use thin pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git push`, thin modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --thin -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exec`

Activa exec durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git push`, exec modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --exec=valor -u origin tema-portada
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --progress -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --no-verify -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --verify -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-4` y `--ipv4`

Limita actualizar referencias de un repositorio remoto y enviar sus objetos al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-4`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git push`, ipv4 modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-4`

```bash
git push -4 -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv4`

```bash
git push --ipv4 -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-6` y `--ipv6`

Limita actualizar referencias de un repositorio remoto y enviar sus objetos al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-6`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git push`, ipv6 modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-6`

```bash
git push -6 -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv6`

```bash
git push --ipv6 -u origin tema-portada
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --no-all -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-branches`

Desactiva para esta invocación el comportamiento que habilita `--branches`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --no-branches -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mirror`

Desactiva para esta invocación el comportamiento que habilita `--mirror`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --no-mirror -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --no-tags -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-follow-tags`

Desactiva para esta invocación el comportamiento que habilita `--follow-tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git push --no-follow-tags -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-atomic`

Desactiva para esta invocación el comportamiento que habilita `--atomic`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --no-atomic -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --no-dry-run -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-receive-pack`

Desactiva para esta invocación el comportamiento que habilita `--receive-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar receive pack modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-receive-pack -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-repo`

Desactiva para esta invocación el comportamiento que habilita `--repo`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar repo modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-repo -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-force -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-delete`

Desactiva para esta invocación el comportamiento que habilita `--delete`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar eliminar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-delete -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva para esta invocación el comportamiento que habilita `--prune`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-prune -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git push --no-quiet -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git push --no-verbose -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-set-upstream`

Desactiva para esta invocación el comportamiento que habilita `--set-upstream`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git push --no-set-upstream origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-push-option`

Desactiva para esta invocación el comportamiento que habilita `--push-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar push option modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-push-option -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed`

Desactiva para esta invocación el comportamiento que habilita `--signed`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar firmado modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-signed -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-porcelain`

Desactiva para esta invocación el comportamiento que habilita `--porcelain`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git push --no-porcelain -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-with-lease`

Desactiva para esta invocación el comportamiento que habilita `--force-with-lease`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección with lease. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-force-with-lease -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-if-includes`

Desactiva para esta invocación el comportamiento que habilita `--force-if-includes`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección if includes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-force-if-includes -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git push --no-recurse-submodules -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thin`

Desactiva para esta invocación el comportamiento que habilita `--thin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar thin modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-thin -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exec`

Desactiva para esta invocación el comportamiento que habilita `--exec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git push`, desactivar exec modifica la forma en que se ejecuta actualizar referencias de un repositorio remoto y enviar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git push --no-exec -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias de un repositorio remoto y enviar sus objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git push --no-progress -u origin tema-portada
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git push` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)

## Fuente

- [git-push - Update remote refs along with associated objects](https://git-scm.com/docs/git-push)
