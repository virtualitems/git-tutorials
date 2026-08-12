---
title: "git reflog"
source: "https://git-scm.com/docs/git-reflog"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git reflog`

Este caso usa `git reflog` para consultar y administrar el registro de cambios de referencias.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git reflog --date=iso
git show HEAD@{1}
```

La invocación `git reflog --date=iso` ejecuta esta operación: consultar y administrar el registro de cambios de referencias. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git reflog [show] [<log-options>] [<ref>]
git reflog list
git reflog exists <ref>
git reflog write <ref> <old-oid> <new-oid> <message>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git reflog [show] [<log-options>] [<ref>]
   or: git reflog list
   or: git reflog exists <ref>
   or: git reflog write <ref> <old-oid> <new-oid> <message>
   or: git reflog delete [--rewrite] [--updateref]
                         [--dry-run | -n] [--verbose] <ref>@{<specifier>}...
   or: git reflog drop [--all [--single-worktree] | <refs>...]
   or: git reflog expire [--expire=<time>] [--expire-unreachable=<time>]
                         [--rewrite] [--updateref] [--stale-fix]
                         [--dry-run | -n] [--verbose] [--all [--single-worktree] | <refs>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git reflog -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--rewrite`

Activa rewrite durante consultar y administrar el registro de cambios de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git reflog --rewrite --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--updateref`

Activa updateref durante consultar y administrar el registro de cambios de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git reflog --updateref --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git reflog --dry-run --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante consultar y administrar el registro de cambios de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git reflog -n --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git reflog --verbose --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git reflog --all --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--single-worktree`

Activa single área de trabajo durante consultar y administrar el registro de cambios de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git reflog --single-worktree --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire`

Aplica una fecha, duración o política de vencimiento.

```bash
git reflog --expire --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire-unreachable`

Aplica una fecha, duración o política de vencimiento.

```bash
git reflog --expire-unreachable --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stale-fix`

Activa stale fix durante consultar y administrar el registro de cambios de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git reflog --stale-fix --date=iso
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git repack`](../administration/repack.md)
- [`git prune`](../administration/prune.md)
- [`git replace`](../administration/replace.md)

## Fuente

- [git-reflog - Manage reflog information](https://git-scm.com/docs/git-reflog)
