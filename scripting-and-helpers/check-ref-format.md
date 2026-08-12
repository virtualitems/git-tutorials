---
title: "git check-ref-format"
source: "https://git-scm.com/docs/git-check-ref-format"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git check-ref-format`

Este caso usa `git check-ref-format` para validar la sintaxis de un nombre de referencia.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git check-ref-format 'refs/heads/tema-portada'
```

La invocación `git check-ref-format 'refs/heads/tema-portada'` ejecuta esta operación: validar la sintaxis de un nombre de referencia. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git check-ref-format [--normalize]
       [--[no-]allow-onelevel] [--refspec-pattern]
       <refname>
git check-ref-format --branch <branchname-shorthand>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git check-ref-format [--normalize] [<options>] <refname>
   or: git check-ref-format --branch <branchname-shorthand>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git check-ref-format -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--normalize`

Activa normalize durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git check-ref-format --normalize 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

### `--allow-onelevel`

Activa permitir onelevel durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git check-ref-format --allow-onelevel 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

### `--refspec-pattern`

Activa refspec pattern durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git check-ref-format --refspec-pattern 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git check-ref-format --branch 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git column`](../scripting-and-helpers/column.md)
- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)
- [`git credential`](../scripting-and-helpers/credential.md)

## Fuente

- [git-check-ref-format - Ensures that a reference name is well formed](https://git-scm.com/docs/git-check-ref-format)
