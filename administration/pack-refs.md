---
title: "git pack-refs"
source: "https://git-scm.com/docs/git-pack-refs"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git pack-refs`

Este caso usa `git pack-refs` para compactar referencias sueltas dentro del archivo packed-refs.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git show-ref --heads
git pack-refs --all --prune
```

La invocación `git pack-refs --all --prune` ejecuta esta operación: compactar referencias sueltas dentro del archivo packed-refs. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git pack-refs [--all] [--no-prune] [--auto] [--include <pattern>] [--exclude <pattern>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git pack-refs [--all] [--no-prune] [--auto] [--include <pattern>] [--exclude <pattern>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pack-refs -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git pack-refs --all --prune
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva el comportamiento `prune` para esta invocación.

```bash
git pack-refs --no-prune --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto`

Activa auto durante compactar referencias sueltas dentro del archivo packed-refs. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `auto-pack refs as needed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-refs --auto --all --prune
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git pack-refs --include=TODO --all --prune
git count-objects -vH
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git pack-refs --exclude=TODO --all --prune
git count-objects -vH
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

```bash
git pack-refs --prune --all
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-include`

Desactiva para esta invocación el comportamiento que habilita `--include`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pack-refs --no-include --all --prune
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exclude`

Desactiva para esta invocación el comportamiento que habilita `--exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pack-refs --no-exclude --all --prune
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git prune`](../administration/prune.md)
- [`git maintenance`](../administration/maintenance.md)
- [`git reflog`](../administration/reflog.md)

## Fuente

- [git-pack-refs - Pack heads and tags for efficient repository access](https://git-scm.com/docs/git-pack-refs)
