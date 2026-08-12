---
title: "git clean"
source: "https://git-scm.com/docs/git-clean"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git clean`

Este caso usa `git clean` para eliminar archivos que Git no sigue.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git clean -nd
git clean -fd
```

La invocación `git clean -nd` ejecuta esta operación: eliminar archivos que Git no sigue. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git clean -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-d`

Retira d del alcance que procesa `git clean`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove whole directories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clean -d -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git clean --force -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-i` y `--interactive`

Abre una selección interactiva antes de aplicar la operación.

#### Ejemplo con `--interactive`

```bash
git clean --interactive -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git clean --dry-run -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git clean --quiet -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-e` y `--exclude`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--exclude`

```bash
git clean --exclude=TODO -nd
git count-objects -vH
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-x`

Retira x del alcance que procesa `git clean`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove ignored files, too`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clean -x -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X`

Limita eliminar archivos que Git no sigue al alcance identificado por X. En Git 2.51.1, la ayuda corta expresa el contrato como `remove only ignored files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clean -X -nd
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git count-objects`](../administration/count-objects.md)
- [`git backfill`](../administration/backfill.md)
- [`git filter-branch`](../administration/filter-branch.md)

## Fuente

- [git-clean - Remove untracked files from the working tree](https://git-scm.com/docs/git-clean)
