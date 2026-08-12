---
title: "git unpack-file"
source: "https://git-scm.com/docs/git-unpack-file"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git unpack-file`

Este caso usa `git unpack-file` para crear un archivo temporal con el contenido de un blob.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
blob=$(git rev-parse HEAD:README.md)
temporal=$(git unpack-file "$blob")
printf '%s\n' "$temporal"
```

La invocación `git unpack-file` ejecuta esta operación: crear un archivo temporal con el contenido de un blob. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git unpack-file <blob>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git unpack-file <blob>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git unpack-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante crear un archivo temporal con el contenido de un blob. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git unpack-file -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git var`](../plumbing-read/var.md)
- [`git show-ref`](../plumbing-read/show-ref.md)
- [`git verify-pack`](../plumbing-read/verify-pack.md)

## Fuente

- [git-unpack-file - Creates a temporary file with a blob’s contents](https://git-scm.com/docs/git-unpack-file)
