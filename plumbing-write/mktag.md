---
title: "git mktag"
source: "https://git-scm.com/docs/git-mktag"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git mktag`

Este caso usa `git mktag` para validar y crear un objeto de etiqueta anotada.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git cat-file tag v1.0 > etiqueta.txt
git mktag < etiqueta.txt
```

La invocación `git mktag < etiqueta.txt` ejecuta esta operación: validar y crear un objeto de etiqueta anotada. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git mktag
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mktag
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mktag -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--strict`

Activa strict durante validar y crear un objeto de etiqueta anotada. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable more strict checking`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mktag --strict < etiqueta.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strict`

Desactiva para esta invocación el comportamiento que habilita `--strict`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git mktag --no-strict < etiqueta.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git mktree`](../plumbing-write/mktree.md)
- [`git merge-index`](../plumbing-write/merge-index.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)

## Fuente

- [git-mktag - Creates a tag object with extra validation](https://git-scm.com/docs/git-mktag)
