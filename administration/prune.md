---
title: "git prune"
source: "https://git-scm.com/docs/git-prune"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git prune`

Este caso usa `git prune` para eliminar objetos sueltos que ningún objeto alcanzable necesita.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git prune --dry-run
```

La invocación `git prune --dry-run` ejecuta esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git prune -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git prune --dry-run
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git prune --verbose --dry-run
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git prune --progress --dry-run
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire`

Aplica una fecha, duración o política de vencimiento.

```bash
git prune --expire=2026-01-15 --dry-run
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git prune --exclude-promisor-objects --dry-run
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git reflog`](../administration/reflog.md)
- [`git pack-refs`](../administration/pack-refs.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [git-prune - Prune all unreachable objects from the object database](https://git-scm.com/docs/git-prune)
