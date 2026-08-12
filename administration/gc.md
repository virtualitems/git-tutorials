---
title: "git gc"
source: "https://git-scm.com/docs/git-gc"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git gc`

Este caso usa `git gc` para compactar el almacenamiento y retirar datos que ya pueden podarse.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v
git gc
git count-objects -v
```

La invocación `git gc` ejecuta esta operación: compactar el almacenamiento y retirar datos que ya pueden podarse. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git gc [--aggressive] [--auto] [--[no-]detach] [--quiet] [--prune=<date> | --no-prune] [--force] [--keep-largest-pack]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git gc [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git gc -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--aggressive`

Activa aggressive durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `be more thorough (increased runtime)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git gc --aggressive
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto`

Activa auto durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable auto-gc mode`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git gc --auto
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

```bash
git gc --detach
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet` y `-q`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git gc --quiet
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

```bash
git gc --prune=2026-01-15
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva el comportamiento `prune` para esta invocación.

```bash
git gc --no-prune
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

```bash
git gc --force
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-largest-pack`

Activa conservar largest pack durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repack all other packs except the largest pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git gc --keep-largest-pack
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Activa cruft durante compactar el almacenamiento y retirar datos que ya pueden podarse. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack unreferenced objects separately`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git gc --cruft
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-cruft-size`

Establece un límite numérico para la selección o el recorrido.

```bash
git gc --max-cruft-size=5
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire-to`

Aplica una fecha, duración o política de vencimiento.

```bash
git gc --expire-to=docs
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git maintenance`](../administration/maintenance.md)
- [`git fsck`](../administration/fsck.md)
- [`git pack-refs`](../administration/pack-refs.md)

## Fuente

- [git-gc - Cleanup unnecessary files and optimize the local repository](https://git-scm.com/docs/git-gc)
