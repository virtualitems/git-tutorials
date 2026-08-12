---
title: "git count-objects"
source: "https://git-scm.com/docs/git-count-objects"
section: "administration"
status: "option-expanded"
---

# `git count-objects`

Este caso usa `git count-objects` para medir objetos sueltos, packs y espacio ocupado. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git count-objects comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en medir objetos sueltos, packs y espacio ocupado.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v -H
```

La invocación `git count-objects -v -H` ejecuta esta operación: medir objetos sueltos, packs y espacio ocupado. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git count-objects [-v] [-H | --human-readable]
```

### Uso verificado con `git version 2.51.1`

```text
git count-objects [-v] [-H | --human-readable]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git count-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

medir objetos sueltos, packs y espacio ocupado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git count-objects a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git count-objects con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git count-objects -v -H
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--verbose`

```bash
git count-objects --verbose -H
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-H` y `--human-readable`

Incluye human readable en la salida o cambia cómo `git count-objects` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print sizes in human readable format`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-H`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-H`

```bash
git count-objects -H -v
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--human-readable`

```bash
git count-objects --human-readable -v
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-human-readable`

Desactiva para esta invocación el comportamiento que habilita `--human-readable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git count-objects --no-human-readable -v
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git count-objects --no-verbose -H
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git count-objects` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git filter-branch`](../administration/filter-branch.md)
- [`git clean`](../administration/clean.md)
- [`git fsck`](../administration/fsck.md)

## Fuente

- [git-count-objects - Count unpacked number of objects and their disk consumption](https://git-scm.com/docs/git-count-objects)
