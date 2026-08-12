---
title: "git filter-branch"
source: "https://git-scm.com/docs/git-filter-branch"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git filter-branch`

Este caso usa `git filter-branch` para reescribir ramas mediante filtros sobre cada commit.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git filter-branch --tree-filter 'rm -f secreto.txt' -- --all
```

La invocación `git filter-branch --tree-filter 'rm -f secreto.txt' -- --all` ejecuta esta operación: reescribir ramas mediante filtros sobre cada commit. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git filter-branch [--setup <command>] [--subdirectory-filter <directory>]
	[--env-filter <command>] [--tree-filter <command>]
	[--index-filter <command>] [--parent-filter <command>]
	[--msg-filter <command>] [--commit-filter <command>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git filter-branch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--setup`

Activa setup durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --setup --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--subdirectory-filter`

Activa subdirectory filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --subdirectory-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--env-filter`

Activa env filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --env-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tree-filter`

Activa tree filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-filter`

Activa índice filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --index-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--parent-filter`

Activa parent filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --parent-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--msg-filter`

Activa msg filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --msg-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit-filter`

Activa commit filtro durante reescribir ramas mediante filtros sobre cada commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git filter-branch --commit-filter --tree-filter 'rm -f secreto.txt' -- --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git fsck`](../administration/fsck.md)
- [`git count-objects`](../administration/count-objects.md)
- [`git gc`](../administration/gc.md)

## Fuente

- [git-filter-branch - Rewrite branches](https://git-scm.com/docs/git-filter-branch)
