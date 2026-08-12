---
title: "git replay"
source: "https://git-scm.com/docs/git-replay"
section: "patching"
status: "source-audited"
version: "2.55.0"
---

# `git replay`

Este caso usa `git replay` para reproducir commits sobre una base y comunicar el cambio de referencias.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git replay --onto=main main..tema-portada
```

La invocación `git replay --onto=main main..tema-portada` ejecuta esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Después, el diff y el historial muestran si cambiaron archivos, índice o commits.

## Sintaxis y formas de invocación

```text
(EXPERIMENTAL!) git replay ([--contained] --onto=<newbase> | --advance=<branch> | --revert=<branch>)
			     [--ref=<ref>] [--ref-action=<mode>] <revision-range>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
(EXPERIMENTAL!) git replay ([--contained] --onto <newbase> | --advance <branch>) <revision-range>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git replay -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--contained`

Activa contained durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `advance all branches contained in revision-range`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git replay --contained --onto=main main..tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--onto`

Activa onto durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `replay onto given commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git replay --onto=valor main..tema-portada
git status --short
```

### `--advance`

Activa advance durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make replay advance given branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git replay --advance=main --onto=main main..tema-portada
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--revert`

Activa revert durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git replay --revert --onto=main main..tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git replay --ref --onto=main main..tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref-action`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git replay --ref-action --onto=main main..tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git revert`](../patching/revert.md)
- [`git rebase`](../patching/rebase.md)
- [`git cherry-pick`](../patching/cherry-pick.md)

## Fuente

- [git-replay - EXPERIMENTAL: Replay commits on a new base, works with bare repos too](https://git-scm.com/docs/git-replay)
