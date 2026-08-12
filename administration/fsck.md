---
title: "git fsck"
source: "https://git-scm.com/docs/git-fsck"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git fsck`

Este caso usa `git fsck` para comprobar conectividad y validez de los objetos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git fsck --full
```

La invocación `git fsck --full` ejecuta esta operación: comprobar conectividad y validez de los objetos. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
	 [--[no-]full] [--strict] [--verbose] [--lost-found]
	 [--[no-]dangling] [--[no-]progress] [--connectivity-only]
	 [--[no-]name-objects] [--[no-]references] [<object>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
                [--[no-]full] [--strict] [--verbose] [--lost-found]
                [--[no-]dangling] [--[no-]progress] [--connectivity-only]
                [--[no-]name-objects] [--[no-]references] [<object>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fsck -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git fsck --tags --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--root`

Activa root durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `report root nodes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --root --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unreachable`

Incluye unreachable en la salida o cambia cómo `git fsck` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --unreachable --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cache`

Activa cache durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make index objects head nodes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --cache --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reflogs`

Desactiva el comportamiento `reflogs` para esta invocación.

```bash
git fsck --no-reflogs --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--full`

Activa full durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `also consider packs and alternate objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable more strict checking`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --strict --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git fsck --verbose --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--lost-found`

Escribe o registra lost found como parte de comprobar conectividad y validez de los objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `write dangling objects in .git/lost-found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --lost-found --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dangling`

Incluye dangling en la salida o cambia cómo `git fsck` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show dangling objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --dangling --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git fsck --progress --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--connectivity-only`

Limita comprobar conectividad y validez de los objetos al alcance identificado por connectivity only. En Git 2.51.1, la ayuda corta expresa el contrato como `check only connectivity`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --connectivity-only --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git fsck --name-objects --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--references`

Comprueba references antes de aceptar el resultado de `git fsck`. En Git 2.51.1, la ayuda corta expresa el contrato como `check reference database consistency`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --references --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reflogs`

Activa reflogs durante comprobar conectividad y validez de los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make reflogs head nodes (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fsck --reflogs --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dangling`

Desactiva para esta invocación el comportamiento que habilita `--dangling`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fsck --no-dangling --full
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git gc`](../administration/gc.md)
- [`git filter-branch`](../administration/filter-branch.md)
- [`git maintenance`](../administration/maintenance.md)

## Fuente

- [git-fsck - Verifies the connectivity and validity of the objects in the database](https://git-scm.com/docs/git-fsck)
