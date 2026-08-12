---
title: "git prune"
source: "https://git-scm.com/docs/git-prune"
section: "administration"
status: "option-expanded"
---

# `git prune`

Este caso usa `git prune` para eliminar objetos sueltos que ningún objeto alcanzable necesita. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git prune comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en eliminar objetos sueltos que ningún objeto alcanzable necesita.

Puede persistir el estado implicado por esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git prune --dry-run
```

La invocación `git prune --dry-run` ejecuta esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…]
```

### Uso verificado con `git version 2.51.1`

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git prune -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

eliminar objetos sueltos que ningún objeto alcanzable necesita. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git prune a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git prune con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla simular ejecución. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-n`

```bash
git prune -n
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--dry-run`

```bash
git prune --dry-run
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla mostrar detalle. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-v`

```bash
git prune -v --dry-run
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--verbose`

```bash
git prune --verbose --dry-run
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git prune --progress --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire`

Aplica una fecha, duración o política de vencimiento.

La opción controla expire. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git prune --expire=2026-01-15 --dry-run
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción limita o amplía el conjunto sobre el que se ejecuta eliminar objetos sueltos que ningún objeto alcanzable necesita. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git prune --exclude-promisor-objects --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git prune --no-progress --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-expire`

Desactiva para esta invocación el comportamiento que habilita `--expire`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar expire. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git prune --no-expire --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar simular ejecución. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git prune --no-dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar mostrar detalle. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar objetos sueltos que ningún objeto alcanzable necesita puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git prune --no-verbose --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exclude-promisor-objects`

Desactiva para esta invocación el comportamiento que habilita `--exclude-promisor-objects`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta eliminar objetos sueltos que ningún objeto alcanzable necesita. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git prune --no-exclude-promisor-objects --dry-run
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git prune` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git reflog`](../administration/reflog.md)
- [`git pack-refs`](../administration/pack-refs.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [git-prune - Prune all unreachable objects from the object database](https://git-scm.com/docs/git-prune)
