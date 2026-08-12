---
title: "git replace"
source: "https://git-scm.com/docs/git-replace"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git replace`

Este caso usa `git replace` para sustituir un objeto por otro durante el recorrido del repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
original=$(git rev-parse HEAD~1)
sustituto=$(git rev-parse HEAD)
git replace "$original" "$sustituto"
```

La invocación `git replace "$original" "$sustituto"` ejecuta esta operación: sustituir un objeto por otro durante el recorrido del repositorio. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git replace [-f] <object> <replacement>
git replace [-f] --edit <object>
git replace [-f] --graft <commit> [<parent>…]
git replace [-f] --convert-graft-file
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git replace [-f] <object> <replacement>
   or: git replace [-f] --edit <object>
   or: git replace [-f] --graft <commit> [<parent>...]
   or: git replace [-f] --convert-graft-file
   or: git replace -d <object>...
   or: git replace [--format=<format>] [-l [<pattern>]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git replace -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git replace --force "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git replace --edit "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--graft` y `-g`

Activa graft durante sustituir un objeto por otro durante el recorrido del repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `change a commit's parents`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--graft`

```bash
git replace --graft "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--convert-graft-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git replace` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git replace --convert-graft-file "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d` y `--delete`

Elimina el elemento seleccionado.

#### Ejemplo con `--delete`

```bash
git replace --delete "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--format`

Define los campos y separadores de la salida.

```bash
git replace --format=oneline "$original" "$sustituto"
git count-objects -vH
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--list`

Incluye información adicional en la salida.

#### Ejemplo con `--list`

```bash
git replace --list "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--raw`

Impide raw durante esta invocación de `git replace`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not pretty-print contents for --edit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git replace --raw "$original" "$sustituto"
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`scalar`](../administration/scalar.md)
- [`git repack`](../administration/repack.md)
- [`git reflog`](../administration/reflog.md)

## Fuente

- [git-replace - Create, list, delete refs to replace objects](https://git-scm.com/docs/git-replace)
