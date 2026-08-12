---
title: "git filter-branch"
source: "https://git-scm.com/docs/git-filter-branch"
section: "administration"
status: "option-expanded"
---

# `git filter-branch`

Este caso usa `git filter-branch` para reescribir ramas mediante filtros sobre cada commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git filter-branch comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en reescribir ramas mediante filtros sobre cada commit.

Puede persistir el estado implicado por esta operación: reescribir ramas mediante filtros sobre cada commit. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git filter-branch --tree-filter 'rm -f secreto.txt' -- --all
```

La invocación `git filter-branch --tree-filter 'rm -f secreto.txt' -- --all` ejecuta esta operación: reescribir ramas mediante filtros sobre cada commit. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git filter-branch [--setup <command>] [--subdirectory-filter <directory>]
	[--env-filter <command>] [--tree-filter <command>]
	[--index-filter <command>] [--parent-filter <command>]
	[--msg-filter <command>] [--commit-filter <command>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git filter-branch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

reescribir ramas mediante filtros sobre cada commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git filter-branch a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git filter-branch con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--setup`

Activa setup durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git filter-branch`, setup modifica la forma en que se ejecuta reescribir ramas mediante filtros sobre cada commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git filter-branch --setup --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--subdirectory-filter`

Activa subdirectory filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --subdirectory-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--env-filter`

Activa env filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --env-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tree-filter`

Activa tree filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-filter`

Activa índice filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --index-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--parent-filter`

Activa parent filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --parent-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--msg-filter`

Activa msg filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --msg-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit-filter`

Activa commit filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta reescribir ramas mediante filtros sobre cada commit. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git filter-branch --commit-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git filter-branch` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: reescribir ramas mediante filtros sobre cada commit. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git fsck`](../administration/fsck.md)
- [`git count-objects`](../administration/count-objects.md)
- [`git gc`](../administration/gc.md)

## Fuente

- [git-filter-branch - Rewrite branches](https://git-scm.com/docs/git-filter-branch)
