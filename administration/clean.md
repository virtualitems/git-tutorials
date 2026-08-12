---
title: "git clean"
source: "https://git-scm.com/docs/git-clean"
section: "administration"
status: "option-expanded"
---

# `git clean`

Este caso usa `git clean` para eliminar archivos que Git no sigue. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git clean comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en eliminar archivos que Git no sigue.

Puede persistir el estado implicado por esta operación: eliminar archivos que Git no sigue. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git clean -nd
git clean -fd
```

La invocación `git clean -nd` ejecuta esta operación: eliminar archivos que Git no sigue. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>…]
```

### Uso verificado con `git version 2.51.1`

```text
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git clean -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

eliminar archivos que Git no sigue. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git clean a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git clean con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-d`

Retira d del alcance que procesa `git clean`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove whole directories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla d. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clean -d -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git clean -f -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--force`

```bash
git clean --force -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-i` y `--interactive`

Abre una selección interactiva antes de aplicar la operación.  La misma línea de ayuda también acepta `-i`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clean`, selección interactiva modifica la forma en que se ejecuta eliminar archivos que Git no sigue. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-i`

```bash
git clean -i -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--interactive`

```bash
git clean --interactive -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

#### Ejemplo con `-n`

```bash
git clean -n -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--dry-run`

```bash
git clean --dry-run -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla reducir mensajes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-q`

```bash
git clean -q -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--quiet`

```bash
git clean --quiet -nd
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-e` y `--exclude`

Excluye elementos que cumplan la condición indicada.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta eliminar archivos que Git no sigue. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-e`

```bash
git clean -e TODO -nd
git count-objects -vH
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--exclude`

```bash
git clean --exclude=TODO -nd
git count-objects -vH
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-x`

Retira x del alcance que procesa `git clean`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove ignored files, too`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla x. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clean -x -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X`

Limita eliminar archivos que Git no sigue al alcance identificado por X. En Git 2.51.1, la ayuda corta expresa el contrato como `remove only ignored files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla X. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clean -X -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar reducir mensajes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clean --no-quiet -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clean --no-dry-run -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque eliminar archivos que Git no sigue puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clean --no-force -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-interactive`

Desactiva para esta invocación el comportamiento que habilita `--interactive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clean`, desactivar selección interactiva modifica la forma en que se ejecuta eliminar archivos que Git no sigue. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clean --no-interactive -nd
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clean` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: eliminar archivos que Git no sigue. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git count-objects`](../administration/count-objects.md)
- [`git backfill`](../administration/backfill.md)
- [`git filter-branch`](../administration/filter-branch.md)

## Fuente

- [git-clean - Remove untracked files from the working tree](https://git-scm.com/docs/git-clean)
