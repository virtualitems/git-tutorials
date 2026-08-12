---
title: "git gc"
source: "https://git-scm.com/docs/git-gc"
section: "administration"
status: "option-expanded"
---

# `git gc`

Este caso usa `git gc` para compactar el almacenamiento y retirar datos que ya pueden podarse. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git gc comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en compactar el almacenamiento y retirar datos que ya pueden podarse.

Puede persistir el estado implicado por esta operación: compactar el almacenamiento y retirar datos que ya pueden podarse. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v
git gc
git count-objects -v
```

La invocación `git gc` ejecuta esta operación: compactar el almacenamiento y retirar datos que ya pueden podarse. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git gc [--aggressive] [--auto] [--[no-]detach] [--quiet] [--prune=<date> | --no-prune] [--force] [--keep-largest-pack]
```

### Uso verificado con `git version 2.51.1`

```text
git gc [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git gc -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

compactar el almacenamiento y retirar datos que ya pueden podarse. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git gc a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git gc con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--aggressive`

Activa aggressive durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `be more thorough (increased runtime)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git gc`, aggressive modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --aggressive
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto`

Activa auto durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable auto-gc mode`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git gc`, auto modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --auto
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

En `git gc`, HEAD separado modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --detach
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet` y `-q`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `--quiet`

```bash
git gc --quiet
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `-q`

```bash
git gc -q
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

La opción controla podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --prune=2026-01-15
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva el comportamiento `prune` para esta invocación.

La opción controla desactivar podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --no-prune
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --force
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-largest-pack`

Activa conservar largest pack durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repack all other packs except the largest pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git gc --keep-largest-pack
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Activa cruft durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack unreferenced objects separately`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git gc`, cruft modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --cruft
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-cruft-size`

Establece un límite numérico para la selección o el recorrido.

En `git gc`, máximo cruft size modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --max-cruft-size=5
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire-to`

Aplica una fecha, duración o política de vencimiento.

La opción controla expire to. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --expire-to=docs
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-aggressive`

Desactiva para esta invocación el comportamiento que habilita `--aggressive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git gc`, desactivar aggressive modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --no-aggressive
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto`

Desactiva para esta invocación el comportamiento que habilita `--auto`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git gc`, desactivar auto modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --no-auto
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-detach`

Desactiva para esta invocación el comportamiento que habilita `--detach`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git gc`, desactivar HEAD separado modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --no-detach
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git gc --no-quiet
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --no-force
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-largest-pack`

Desactiva para esta invocación el comportamiento que habilita `--keep-largest-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git gc --no-keep-largest-pack
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cruft`

Desactiva para esta invocación el comportamiento que habilita `--cruft`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git gc`, desactivar cruft modifica la forma en que se ejecuta compactar el almacenamiento y retirar datos que ya pueden podarse. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git gc --no-cruft
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-expire-to`

Desactiva para esta invocación el comportamiento que habilita `--expire-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar expire to. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque compactar el almacenamiento y retirar datos que ya pueden podarse puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git gc --no-expire-to
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git gc` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: compactar el almacenamiento y retirar datos que ya pueden podarse. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git maintenance`](../administration/maintenance.md)
- [`git fsck`](../administration/fsck.md)
- [`git pack-refs`](../administration/pack-refs.md)

## Fuente

- [git-gc - Cleanup unnecessary files and optimize the local repository](https://git-scm.com/docs/git-gc)
