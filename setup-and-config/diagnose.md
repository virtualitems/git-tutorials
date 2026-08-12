---
title: "git diagnose"
source: "https://git-scm.com/docs/git-diagnose"
section: "setup-and-config"
status: "source-audited"
version: "2.55.0"
---

# `git diagnose`

Este caso usa `git diagnose` para generar un archivo con datos de diagnóstico del repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
mkdir diagnostico
git diagnose --mode=stats --output-directory=diagnostico
```

La invocación `git diagnose --mode=stats --output-directory=diagnostico` ejecuta esta operación: generar un archivo con datos de diagnóstico del repositorio. Después, una consulta posterior muestra el valor efectivo o la información generada.

## Sintaxis y formas de invocación

```text
git diagnose [(-o | --output-directory) <path>] [(-s | --suffix) <format>]
	       [--mode=<mode>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git diagnose [(-o | --output-directory) <path>] [(-s | --suffix) <format>]
                    [--mode=<mode>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diagnose -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-o` y `--output-directory`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

#### Ejemplo con `--output-directory`

```bash
git diagnose --output-directory=archivo.txt --mode=stats
printf 'exit=%s\n' "$?"
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-s` y `--suffix`

Define suffix para esta ejecución de `git diagnose`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify a strftime format suffix for the filename`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--suffix`

```bash
git diagnose --suffix=oneline --mode=stats --output-directory=diagnostico
printf 'exit=%s\n' "$?"
```

En esta forma, `oneline` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--mode`

Define mode para esta ejecución de `git diagnose`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the content of the diagnostic archive`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diagnose --mode=valor --output-directory=diagnostico
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git help`](../setup-and-config/help.md)
- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git version`](../setup-and-config/version.md)

## Fuente

- [git-diagnose - Generate a zip archive of diagnostic information](https://git-scm.com/docs/git-diagnose)
