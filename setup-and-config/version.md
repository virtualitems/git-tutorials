---
title: "git version"
source: "https://git-scm.com/docs/git-version"
section: "setup-and-config"
status: "reviewed"
version: "2.55.0"
---

# `git version`

`git version` escribe la versión instalada de Git. Con `--build-options` añade datos de compilación útiles para un informe de diagnóstico.

## Sintaxis

```text
git version [--build-options]
git --version [--build-options]
```

Git convierte internamente `git --version` en `git version`, por lo que ambas formas aceptan la misma opción.

## Consultar la versión

```bash
git version
```

La salida tiene esta forma:

```text
git version 2.55.0
```

La versión real depende de la instalación. El comando no necesita un repositorio y no modifica archivos ni configuración.

Un script puede extraer el identificador sin depender de la configuración del usuario:

```bash
git --version
printf 'exit=%s\n' "$?"
```

Un código cero indica que Git reconoció la orden. Analiza la salida completa si necesitas distinguir versiones de desarrollo o builds de un distribuidor; no asumas que el valor contiene solo tres números.

## Opción `--build-options`

`--build-options` muestra la versión, la arquitectura de CPU, el tamaño de `long` y `size_t`, el shell configurado y las bibliotecas usadas para SHA-1 y SHA-256. Los campos presentes dependen de cómo se compiló Git.

```bash
git version --build-options
```

Una salida posible es:

```text
git version 2.55.0
cpu: x86_64
sizeof-long: 8
sizeof-size_t: 8
shell-path: /bin/sh
```

No compares toda la salida con una cadena fija: otro sistema puede usar otra arquitectura, shell o implementación criptográfica. Conserva el resultado completo al adjuntarlo a un `git bugreport`.

## Diagnóstico

Si el shell no encuentra `git`, comprueba la variable `PATH` y la instalación antes de inspeccionar un repositorio. Si la versión obtenida no es la esperada, localiza el ejecutable efectivo con `Get-Command git` en PowerShell o `command -v git` en un shell POSIX.

Una opción documentada en este proyecto puede faltar en una instalación anterior. Compara `git --version` con la versión objetivo indicada en el [README](../README.md#alcance-y-convenciones) y consulta `git <comando> --help-all` en la máquina que ejecutará el flujo.

## Páginas relacionadas

- [`git help`](help.md)
- [`git bugreport`](bugreport.md)
- [Convenciones de la CLI](../guides/gitcli.md)

## Fuente

- [git-version 2.55.0 — información de versión](https://git-scm.com/docs/git-version/2.55.0)
