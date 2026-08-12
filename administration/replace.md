---
title: "git replace"
source: "https://git-scm.com/docs/git-replace"
section: "administration"
status: "option-expanded"
---

# `git replace`

Este caso usa `git replace` para sustituir un objeto por otro durante el recorrido del repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git replace comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en sustituir un objeto por otro durante el recorrido del repositorio.

Puede persistir el estado implicado por esta operación: sustituir un objeto por otro durante el recorrido del repositorio. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
original=$(git rev-parse HEAD~1)
sustituto=$(git rev-parse HEAD)
git replace "$original" "$sustituto"
```

La invocación `git replace "$original" "$sustituto"` ejecuta esta operación: sustituir un objeto por otro durante el recorrido del repositorio. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git replace [-f] <object> <replacement>
git replace [-f] --edit <object>
git replace [-f] --graft <commit> [<parent>…]
git replace [-f] --convert-graft-file
```

### Uso verificado con `git version 2.51.1`

```text
git replace [-f] <object> <replacement>
   or: git replace [-f] --edit <object>
   or: git replace [-f] --graft <commit> [<parent>...]
   or: git replace [-f] --convert-graft-file
   or: git replace -d <object>...
   or: git replace [--format=<format>] [-l [<pattern>]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git replace -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

sustituir un objeto por otro durante el recorrido del repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git replace a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git replace con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque sustituir un objeto por otro durante el recorrido del repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git replace -f "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--force`

```bash
git replace --force "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git replace`, edición modifica la forma en que se ejecuta sustituir un objeto por otro durante el recorrido del repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--edit`

```bash
git replace --edit "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `-e`

```bash
git replace -e "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--graft` y `-g`

Activa graft durante sustituir un objeto por otro durante el recorrido del repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `change a commit's parents`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-g`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git replace`, graft modifica la forma en que se ejecuta sustituir un objeto por otro durante el recorrido del repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--graft`

```bash
git replace --graft "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `-g`

```bash
git replace -g "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--convert-graft-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git replace` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git replace --convert-graft-file "$original" "$sustituto"
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d` y `--delete`

Elimina el elemento seleccionado.  La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla eliminar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque sustituir un objeto por otro durante el recorrido del repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-d`

```bash
git replace -d "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--delete`

```bash
git replace --delete "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--format`

Define los campos y separadores de la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git replace --format=oneline "$original" "$sustituto"
git count-objects -vH
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--list`

Incluye información adicional en la salida.  La misma línea de ayuda también acepta `-l`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git replace`, list modifica la forma en que se ejecuta sustituir un objeto por otro durante el recorrido del repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-l`

```bash
git replace -l "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--list`

```bash
git replace --list "$original" "$sustituto"
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--raw`

Impide raw durante esta invocación de `git replace`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not pretty-print contents for --edit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git replace --raw "$original" "$sustituto"
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-format`

Desactiva para esta invocación el comportamiento que habilita `--format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git replace --no-format "$original" "$sustituto"
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque sustituir un objeto por otro durante el recorrido del repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git replace --no-force "$original" "$sustituto"
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-raw`

Desactiva para esta invocación el comportamiento que habilita `--raw`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git replace --no-raw "$original" "$sustituto"
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replace` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: sustituir un objeto por otro durante el recorrido del repositorio. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`scalar`](../administration/scalar.md)
- [`git repack`](../administration/repack.md)
- [`git reflog`](../administration/reflog.md)

## Fuente

- [git-replace - Create, list, delete refs to replace objects](https://git-scm.com/docs/git-replace)
